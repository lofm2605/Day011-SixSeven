# Đề xuất gold set theo camera — tình huống giả lập

**Đầu bài:** 50.000 frame từ bốn camera SVM, ngân sách chọn 200 frame để review/gold. Đây là tình huống trên slide,
**không phải** 50.000 frame có trong repo. Phân bổ đúng 200 ở `45_sampling_plan.csv` cho bốn camera, mỗi camera có
normal và hard slice. “Gold set” ở đây là **kế hoạch tạo** reference sau kiểm chứng, không phải teaching reference
ADASIND hoặc nhãn bạn vừa vẽ. Nếu cần, dùng `notebooks/day11-svm360-colab.ipynb` để thử tổng phân bổ; notebook
không làm thay phần lý do.

| camera_id | Hard case cần chọn | Vì sao dễ sai | Annotation space / calibration cần giữ | Cách review trước khi gọi là gold |
|---|---|---|---|---|
| front | Giao thông đông, nhiều xe ba bánh, pickup/van, vật xa cao sát 40 px (30 hard / 25 normal) | Class dễ nhầm theo R04 (ở B4-mid, B thấy pickup bị gán Car — 265065 L6); vật nhỏ sát ngưỡng R01 dễ bị bỏ hoặc vẽ thừa | Ảnh fisheye gốc của front, vòng kính đo riêng cho camera front; ghi version calibration và rules_version khi gán nhãn | 2 người gán nhãn độc lập → reviewer thứ 3 soát class theo R04 và ngưỡng 40 px; bất đồng xử lý bằng ảnh + rule, chưa đủ bằng chứng thì E5 và giữ ngoài gold |
| rear | Lùi/đỗ xe, vật rất gần bị vòng kính cắt hoặc bị thân xe che (25 hard / 20 normal) | truncated vs occluded dễ lẫn (R05) — lỗi chính ở r1_craft (3 box truncated sai); ego_body lớn dễ làm box rơi vào ignore (R09) | Ảnh gốc rear, polygon lens_border và ego_body riêng của camera rear; không dùng lại polygon của camera khác | Reviewer độc lập kiểm riêng truncated (tính theo vòng kính) và occluded (nhìn ảnh); đối chiếu ego_body từng frame trước khi khóa |
| left | Xe máy vượt sát, rider/người dắt xe, vật ở zone edge bị kéo cong (30 hard / 20 normal) | Rider dễ tách thành Pedestrian + Bike sai R03; box ở edge dễ lệch vì biến dạng mạnh | Ảnh gốc left, vòng kính left; ghi rõ zone tính theo tâm vòng kính của chính camera left | Review theo checklist rider (R03) + geometry ở edge; lấy mẫu rải theo thời gian, không lấy nhiều frame liên tiếp cùng một xe |
| right | Xe to (bus/truck) đi qua chiếm nửa ảnh, nhiều vật chồng nhau, vùng seam với front (30 hard / 20 normal) | Box lớn ở edge dễ sai geometry và truncated; vật chồng nhau dễ thiếu hoặc trùng box | Ảnh gốc right, vòng kính right; timestamp để đối chiếu với front ở vùng seam | 2 người gán độc lập + reviewer; ca seam đánh dấu riêng, chỉ vào gold khi có policy seam đã duyệt (xem dưới) |

- Khi nào cần refresh gold set (đổi camera, calibration hoặc rule): khi thay/đổi vị trí camera hoặc ống kính (vòng
  kính và zone thay đổi); khi calibration cập nhật; khi `rules_version` tăng (ví dụ patch R04/R05 trong
  `20_guideline_patch.md`) — gán nhãn lại các frame bị ảnh hưởng bởi rule mới; và định kỳ khi dữ liệu mới khác phân
  bố cũ (đêm, mưa, khu vực mới).
- Một ca seam/cross-camera cần policy và evidence trước khi ghép hai box: một xe máy vượt ở góc trước-phải xuất hiện
  cùng lúc ở zone edge của camera front và zone mid của camera right với hai box khác nhau. Trước khi coi là một vật
  (ghép box hay cùng track ID) cần: timestamp đồng bộ của hai camera, calibration để chiếu hai box về cùng hệ tọa độ
  (vd BEV), và policy output đích (giữ cả hai box theo từng camera hay hợp nhất). Khi chưa có, giữ hai box riêng theo
  từng camera, không đánh DUPLICATE, ghi ca vào escalation cho người soát quyết định.
- Vì sao peer agreement hoặc quality report trên ảnh một camera chưa chứng minh gold set đúng cho cả bốn camera:
  số liệu của lab chỉ đến từ **một** camera ADASIND và 3 frame B4-mid; hai người đồng ý với nhau vẫn có thể cùng
  hiểu sai rule, và teaching reference cũng có thể sai. Mỗi camera có vòng kính, ego_body, góc nhìn và loại vật
  khác nhau, nên lỗi ở camera này không suy ra phân bố lỗi ở camera khác. Cần review độc lập và đo riêng trên từng
  camera trước khi gọi là gold.

Người soạn: Lâm (C). Người kiểm: [A/B điền tên sau khi đọc]. Sẽ bổ sung ví dụ lỗi cụ thể sau khi đọc báo cáo P4.
