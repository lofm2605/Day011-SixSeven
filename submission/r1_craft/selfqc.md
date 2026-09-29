# Tự soát

- adasind_261480.jpg L2: truncated khác dự kiến
- adasind_261480.jpg L3: truncated khác dự kiến
- adasind_265065.jpg L5: truncated khác dự kiến
- Tên task thiếu raw_fisheye

## Checklist thủ công
- [x] Phạm vi H=40 và vật cần vẽ
- [x] lens_border và ego_body
- [x] Class sáu nhãn
- [x] Rider và Bike
- [x] Geometry trên ảnh fisheye gốc
- [x] truncated và occluded
- [x] Vật thiếu hoặc box trùng
- [x] ignore_region có reason
- [x] Tên task raw_fisheye và export CVAT 1.1

*Ghi chú soát*: 3 box truncated (261480 L2, L3; 265065 L5) đã khóa theo quan sát ảnh gốc, chưa sửa; đã ghi nhận thành 3 finding r1_craft để chuyển Role B (QA) xác nhận độc lập. Tên task export ban đầu thiếu raw_fisheye do chuỗi đặt tên trên CVAT nhưng labels và dữ liệu đối tượng hoàn toàn chuẩn xác.

## Fill ratio (K12)
- adasind_249480.jpg box 2 mid: 0.803
- adasind_261480.jpg box 1 mid: 0.803
- adasind_261480.jpg box 4 mid: 0.715
- adasind_265065.jpg box 1 mid: 0.633
