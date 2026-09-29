# QA review · B4-mid
 Reviewer: Lê Hùng Cường (B).
 Chủ nhãn: Lê Mình Khôi (A).
 Mã khóa: 8B21-B72D

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_261480.jpg | L2 | R05 | ThreeWheeler `truncated=true` nhưng box (x 93.0-131.2) nằm giữa khung, không chạm vòng kính/biên; theo R05 cần xác nhận trên ảnh gốc có bị cắt không. |
| adasind_261480.jpg | L3 | R05 | ThreeWheeler `truncated=true`, box (x 71.4-96.2) gần mép trái nhưng chưa chạm x=0; xác nhận có thực sự bị vòng kính cắt không. |
| adasind_265065.jpg | L5 | R05 | Bike `truncated=true` nhưng box (x 422.5-458.8) nằm giữa khung, không chạm biên; nghi chưa đạt R05, cần đối chiếu ảnh gốc. |
| adasind_265065.jpg | L6 | R04 | Xe tải con (pickup/xe tải nhỏ) đang bị đánh nhầm là Car; theo R04 nhóm này thuộc Truck. |

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.