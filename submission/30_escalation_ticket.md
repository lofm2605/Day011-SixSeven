# Escalation ticket

## Ticket 1

- **Frame:** `adasind_265065.jpg`, box L5 ở r1_craft (= L8 ở rework v2), [423, 781, 459, 828], zone center
- **Ảnh chụp:** `submission/screenshots/qa_265065_L5_truncated_L6_pickup.png`
- **Vấn đề:** xe máy đỗ cạnh biển XEROX, cao 47 px (≥ 40, R01), nhìn thấy trên ảnh gốc, bị biển che một phần. Nhãn của nhóm có box; **teaching reference và model đều không có** → báo cáo tính là SPURIOUS (findings r3_diag `L5`, E0_reference_defect; decision log D4). Cùng frame, ở rework v2 nhóm thêm Pedestrian L1 [283, 765, 299, 813] — người áo trắng đứng sau xe tải, cao 48 px, bị xe tải che một phần; R và M cũng không có (finding round rework `L1`, E0; decision log D8).
- **Expected impact:** nếu reference thiếu, precision của mọi người gán nhãn đúng trên frame này bị hạ oan; nếu dùng reference này làm gold, model sẽ học bỏ qua xe đỗ bị che một phần.
- **Owner:** `qa`
- **Recommendation:** người quản lý reference xem lại 265065 (L5 và vùng sau xe tải, x 283–299), quyết định thêm vào reference hay ghi lý do loại (ví dụ `unreadable`); cập nhật `rules_version` nếu cần luật cho xe đỗ bị che. Cho đến khi có quyết định, nhóm giữ box và không tính ca này là lỗi người gán.

## Ticket 2

- **Frame:** `adasind_261480.jpg` — L2+R6, L3+R5, L7+R4 (3 ThreeWheeler)
- **Ảnh chụp:** `submission/screenshots/qa_261480_L7_ThreeWheeler.png`, `submission/screenshots/qa_261480_L2_L3_truncated.png`
- **Vấn đề:** L và reference cùng là ThreeWheeler, model YOLO26m gọi thành Car (M6, M8, M10) và còn ra thêm box Truck trùng (M12) → 3 dòng `LR_noM` (E4_model_domain, action escalate; decision log D5). Model cũng tách rider thành Pedestrian ở 249480 (M2, M4) và 261480 (M2, M5).
- **Expected impact:** nếu dùng model làm pre-label, ThreeWheeler — class phổ biến trong dữ liệu này — sẽ bị gán sai class có hệ thống, và rider sinh box Pedestrian thừa, làm tăng công sửa và rủi ro sót lỗi ở QA.
- **Owner:** `ai_team`
- **Recommendation:** đánh giá model theo taxonomy 6 class của lab; bổ sung dữ liệu ThreeWheeler và hậu xử lý gộp rider vào Bike (R03) trước khi dùng làm pre-label; đo lại trên nhiều slice hơn — 3 frame chưa đủ để kết luận tỷ lệ lỗi.
