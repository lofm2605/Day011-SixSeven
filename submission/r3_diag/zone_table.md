# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 4 | 0 | 2 | 1 | 4 | SPURIOUS (1) |
| mid | 13 | 4 | 0 | 3 | 7 | MISSING (3) |
| edge | 0 | 0 | 0 | 0 | 1 | — |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: **mid** là nơi L gãy nhiều nhất — 4 missing trên 13 vật reference (đều ở 265065: R3 do sai class L6, R5 Bike, R6 và R7 Pedestrian), và M cũng thừa nhiều nhất ở mid (7 box `M_only`). Ở **center**, L có 2 spurious (265065 L5 — nghi reference thiếu; L6 — sai class Car/Truck) và M thừa 4 box (chủ yếu rider tách riêng). **edge** gần như không có vật trong slice này (n_ref = 0; chỉ 1 box M thừa là hàng hóa trên nóc xe tải).
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: lỗi của L không do méo fisheye mà do **vật nhỏ, đứng sát nhau ở lề đường** (người đứng cạnh xe tay ga, người bị che một phần) trong một frame đông (265065: 4/4 lỗi missing); cả 2 frame còn lại L khớp R 100 %. Lỗi thuộc tính truncated (3 box) là hiểu nhầm R05, không liên quan zone. Lỗi của M chủ yếu do **class COCO không khớp taxonomy lab**: không có ThreeWheeler (gọi thành Car/Truck) và tách rider thành Pedestrian. Giới hạn: chỉ 3 frame, một camera, 17 vật reference, gần như không có vật ở edge — không đủ để kết luận L hay M yếu ở edge, cũng không suy ra cho camera khác; teaching reference cũng có thể thiếu (265065 L5).
