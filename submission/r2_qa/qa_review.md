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
