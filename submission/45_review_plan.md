# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_265065.jpg` — lề đường đông, zone mid/center | 4 MISSING của L (R3 do sai class, R5 Bike, R6/R7 Pedestrian), 1 WRONG_CLASS (L6 Car/Truck), 2 box chỉ L có (L5 xe máy đỗ, v2 L1 Pedestrian) | Chứa toàn bộ lỗi thiếu/thừa của L (hai frame kia khớp 100 %) và cả nghi ngờ reference thiếu (E0) lẫn ca chưa rõ (R7, E5) — review ở đây vừa sửa nhãn vừa kiểm reference | `screenshots/qa_265065_L5_truncated_L6_pickup.png`; findings r3_diag 265065; `r3_diag/local_quality_conflicts.csv`; decision log D1, D3, D4, D7; ticket 1 |
| `adasind_261480.jpg` — ThreeWheeler bị che, zone mid/center | 3 ATTRIBUTE (truncated sai ở L2, L3 và tương tự 265065 L5), 3 LR_noM do model gọi ThreeWheeler là Car/Truck, 4 box model thừa (rider, box trùng) | Lỗi hệ thống: cùng một hiểu nhầm R05 lặp lại và cùng một lỗi class của model — sửa luật/model sẽ sửa nhiều ca một lúc | `screenshots/qa_261480_L2_L3_truncated.png`, `qa_261480_L7_ThreeWheeler.png`; findings r3_diag `L2+R6`, `L3+R5`, `L7+R4`; `20_guideline_patch.md`; ticket 2 |

Giới hạn của kết luận từ ba frame ADASIND: chỉ 3 frame, một camera, 17 vật reference và **không có vật nào ở zone edge** — không đo được tỷ lệ lỗi, không so sánh được giữa zone, không suy ra cho frame/camera khác. Teaching reference cũng có thể sai (ticket 1), nên số FP/FN là tín hiệu để soi lại ảnh, không phải điểm chất lượng.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv` (kể cả tránh đếm nhiều frame liền nhau trong cùng cảnh
như nhiều ca độc lập), và vì sao kế hoạch đó chỉ giúp tìm ca cần soi, chưa đo được tỷ lệ lỗi: mỗi ô camera × normal/hard lấy rải theo thời gian và địa điểm (tối đa 1 frame mỗi khoảng 5 giây cùng cảnh; frame liền nhau cùng một xe tính là một ca); trước khi review, lập bảng đếm theo camera × điều kiện (ngày/đêm, đông/thưa, có ThreeWheeler, có rider, vật ở edge, vùng seam) để thấy ô nào chưa có ca và bổ sung. Các ô hard được chọn có chủ đích theo loại lỗi đã thấy ở B4-mid (thiếu vật nhỏ ở lề đường, truncated/occluded, class ThreeWheeler/pickup), nên mẫu **lệch về ca khó** — dùng để tìm và sửa lỗi, không phải mẫu ngẫu nhiên đại diện cho 50.000 frame; muốn ước lượng tỷ lệ lỗi cần thêm một mẫu ngẫu nhiên phân tầng riêng.
