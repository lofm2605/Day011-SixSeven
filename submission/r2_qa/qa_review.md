# QA review · B4-mid
 Reviewer: Lê Hùng Cường (B).
 Chủ nhãn: Lê Minh Khôi (A).
 Slice: B4-mid.
 Mã khóa: 2AA4-1FBB (lần đầu ghi 8B21-B72D: cùng nội dung XML, mã khác do git trên Windows đổi xuống dòng LF→CRLF; đã sửa bằng .gitattributes, commit 121490d).

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_261480.jpg | L2 | R05 | ThreeWheeler `truncated=true` nhưng box (x 93.0-131.2) nằm giữa khung, không chạm vòng kính/biên; theo R05 cần xác nhận trên ảnh gốc có bị cắt không. Ảnh: `screenshots/qa_261480_L2_L3_truncated.png`. |
| adasind_261480.jpg | L3 | R05 | ThreeWheeler `truncated=true`, box (x 71.4-96.2) gần mép trái nhưng chưa chạm x=0; xác nhận có thực sự bị vòng kính cắt không. Ảnh: `screenshots/qa_261480_L2_L3_truncated.png`. |
| adasind_265065.jpg | L5 | R05 | Bike `truncated=true` nhưng box (x 422.5-458.8) nằm giữa khung, không chạm biên; nghi chưa đạt R05, cần đối chiếu ảnh gốc. Ảnh: `screenshots/qa_265065_L5_truncated_L6_pickup.png`. |
| adasind_265065.jpg | L6 | R04 | Xe tải con (pickup/xe tải nhỏ) đang bị đánh nhầm là Car; theo R04 nhóm này thuộc Truck. Ảnh: `screenshots/qa_265065_L5_truncated_L6_pickup.png`. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.

Ảnh bối cảnh (không kèm nhận xét lỗi): `screenshots/qa_261480_L7_ThreeWheeler.png` — L7 ThreeWheeler ở 261480, dùng để đối chiếu class với các ThreeWheeler L2/L3 cùng frame.

## Kiểm lại sau rework (P5)

Bản kiểm: `submission/rework/annotations-v2.xml`, mã khóa **605F-D50D** (lock2.txt khớp file). Kiểm theo ảnh gốc + rule; chỉ số L trong bản v2 đánh lại theo thứ tự XML nên khác bản r1_craft.

| Ca QA ban đầu (r1_craft) | Bản v2 | Kết quả kiểm lại |
|---|---|---|
| 261480 L2 ThreeWheeler `truncated=true` (R05) | v2 L1: truncated=false, occluded=true | ✅ Đã sửa. Box không chạm vòng kính/biên; khớp R6 (IoU 0.81) |
| 261480 L3 ThreeWheeler `truncated=true` (R05) | v2 L4: truncated=false, occluded=true | ✅ Đã sửa. Khớp R5 (IoU 0.78), R5 cũng occluded |
| 265065 L5 Bike `truncated=true` (R05) | v2 L8: truncated=false, occluded=true | ✅ Đã sửa thuộc tính. Box vẫn giữ (xe máy cạnh biển XEROX) theo quyết định D4 — escalate, không phải lỗi của A |
| 265065 L6 Car → Truck (R04) | v2 L6: Truck | ✅ Đã sửa. Khớp R3 Truck (IoU 0.84) |

Các ca thêm từ chẩn đoán P4 (D3):

| Ca | Bản v2 | Kết quả kiểm lại |
|---|---|---|
| 265065 thiếu R5 Bike | v2 L7 Bike | ✅ Đã thêm. Khớp R5 (IoU 0.56) — box hơi thấp hơn phần trên xe khoảng 12 px, chấp nhận (P2, không rework thêm) |
| 265065 thiếu R6 Pedestrian | v2 L9 Pedestrian | ✅ Đã thêm, tách riêng khỏi xe theo R03. Khớp R6 (IoU 0.65) |
| 265065 R7 Pedestrian | không thêm | ⏸ Theo D7: vật mờ, chưa chắc là người → E5_unresolved, không phải thiếu sót của rework |

Quan sát mới:
- 265065 v2 L1 Pedestrian (x 283–299, y 765–813, cao 48 px, sau xe tải) là box **mới**, không có trong R và M, đang bị tính spurious ở zone center. Trên ảnh có hình người áo sáng nhưng mờ. Cần A xác nhận đây là người thật (→ giữ, ghi E0 nghi reference thiếu) hay đặt nhầm (→ xóa và khóa lại).

Kết luận: 4/4 nhận xét QA ban đầu và 2/2 ca thiếu được giao đã sửa đúng; còn mở 1 ca mới (v2 L1) chờ A trả lời.

- [X] Cường (B) xác nhận đã đọc và đồng ý kết quả kiểm lại: Cuong
