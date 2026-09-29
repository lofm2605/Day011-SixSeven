# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | ATTRIBUTE | 1 |
| center | B4 | MISSING | 1 |
| center | B4 | SPURIOUS | 7 |
| center | B4 | WRONG_CLASS | 1 |
| center | C0 | SPURIOUS | 1 |
| edge | B4 | SPURIOUS | 1 |
| mid | B4 | ATTRIBUTE | 4 |
| mid | B4 | MISSING | 9 |
| mid | B4 | SPURIOUS | 7 |
| unknown | B4 | ATTRIBUTE | 3 |
| unknown | B4 | WRONG_CLASS | 1 |

## Top defects
- SPURIOUS: 16 (ví dụ frame adasind_019560.jpg)
- MISSING: 10 (ví dụ frame adasind_265065.jpg)
- ATTRIBUTE: 8 (ví dụ frame adasind_261480.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: bảng Top defects gộp cả lỗi của model — 16 SPURIOUS phần lớn là `M_only` (rider bị model tách thành Pedestrian, box trùng, hàng hóa trên nóc xe) → **E4_model_domain**, không phải lỗi người. Lỗi nổi bật nhất **của nhãn L** là **MISSING ở zone mid, frame 265065**: thiếu R5 Bike, R6 Pedestrian (người đứng cạnh xe tay ga) và sai class L6 Car/Truck (R3). Nguyên nhân là **E1_annotator_error**: vật nhỏ (54–60 px) đứng sát nhau ở lề đường đông, bị xe tải che một phần nên dễ bị bỏ qua; hai frame còn lại L khớp reference 100 %. Lỗi ATTRIBUTE (3 box `truncated=true` sai ở 261480 L2, L3; 265065 L5) cũng là E1 nhưng do hiểu nhầm R05: vật bị xe khác/biển che được đánh là truncated thay vì occluded.
- Cách sửa và ai nhận việc (`owner`): `annotator` (Khôi) đã rework ở P5 — thêm Bike/Pedestrian, đổi L6 thành Truck, sửa truncated → `delta.md`: mid missing 4 → 1, matched 9 → 12. Để không lặp lại: đề xuất làm rõ R05 trong `20_guideline_patch.md` (owner `guideline`) và thêm bước soát vùng lề đường đông vào self-QC. Lỗi class của model (ThreeWheeler → Car/Truck) escalate cho `ai_team` (`30_escalation_ticket.md`, Ticket 2). R7 (265065) chưa đủ bằng chứng → E5_unresolved, `qa` theo dõi.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `screenshots/qa_265065_L5_truncated_L6_pickup.png` (L6 xe tải thùng, L5 xe máy cạnh biển); `screenshots/qa_261480_L2_L3_truncated.png`; findings r3_diag 265065 `L6`, `R3+M1`, `R5+M7`, `R6+M6` (E1, R04/R01/R03) và 261480 `L2+R6`, `L3+R5`, `L7+R4` (E4, R04); `r3_diag/local_quality.md` (265065: TP 4, FP 2, FN 4; hai frame kia FP = FN = 0); `rework/delta.md`.
