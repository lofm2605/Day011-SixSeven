# Thành viên và phân vai — Day11 SVM 360 Fisheye

## 1. Thông tin nhóm

- Khóa/lớp: 2B-D304
- Tên nhóm: SixSeven
- Repo Public: https://github.com/lofm2605/Day011-SixSeven
- Máy giữ hồ sơ chính / người quản lý: Lam
- Slice chung lấy từ mode.json: **B4-mid** (adasind_249480.jpg, adasind_261480.jpg, adasind_265065.jpg)
- Tên định danh vai A dùng cho --self: Khoi
- Lệnh đã chạy: `python lab11.py mode --members Cuong,Khoi,Lam --self Khoi`
- Đại diện nộp (vai C): Lam
- Commit chốt bài: commit cuối cùng trên `main` chứa `submission/manifest.json` có `failed_gates: []` (SHA gửi qua kênh lớp khi nộp)

## 2. Ba vai chính

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Lê Minh Khôi | 2A202602163 | Khoi | Parking/C0/slice, self-QC, lock, rework | Parking 3 parking_line + 1 free_space (e99ebd9); C0 lock B81F-32C1 (28ed17e); r1_craft B4-mid lock 2AA4-1FBB (225cb65); self-QC 9 mục + 3 finding r1_craft (b70644b, 137e275); rework P5 v2 lock 605F-D50D (79f9873): L6 Car→Truck, thêm R5 Bike + R6 Pedestrian, sửa 3 truncated; xác nhận exit ticket (a693a7e) |
| B · QA độc lập | Lê Hùng Cường | 2A202602218 | Cuong | Review trước reference, finding QA, kiểm lại ca sửa | QA mù B4-mid: qa_review.md 4 nhận xét (3 × R05 truncated, 1 × R04 pickup→Car), 4 finding r2_qa, 3 ảnh bằng chứng (9cd56a2); kiểm lại ca sửa P5 — 4/4 nhận xét QA + 2 ca thiếu đã sửa đúng, đã ký trong qa_review.md; kiểm 46_gold_set_plan; xác nhận exit ticket (a693a7e) |
| C · Chẩn đoán & điều phối | Vũ Tùng Lâm | 2A202602181 | Lam | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp | mode/doctor/TEAMMATES (e7e8c24, 516fc17); sửa .gitattributes giữ mã khóa (121490d); sensor_context, 45_sampling_plan, 46_gold_set_plan (7b14b49); P4: chạy reference/compare/local-quality/model/iou-sweep, 22 dòng r3_diag + calib, decision log 7 mục, zone table (48f1c73); P5: R7 → E5, rework delta (3f2eb7a); P6: error card, guideline patch R05a, 2 escalation ticket, review plan, exit ticket, check exit 0 (a693a7e) |

Bảng này xác định vai của nhóm. Vòng QA tự sinh trong team.json thuộc quy trình nhiều hồ sơ của CLI; nhóm dùng một slice chung (B4-mid) và quy trình A → B → C đã nêu trong hướng dẫn.

### Quyền sửa file (mỗi file một người tại một thời điểm)

| File / thư mục | Người sửa | Thời điểm |
|---|---|---|
| Task CVAT, `parking/`, `p1_calib/annotations.xml`, `r1_craft/`, `rework/` | A | P0–P2, P5 |
| `findings.csv` — dòng `r1_craft` | A | Cuối P2 |
| `r2_qa/qa_review.md`, `screenshots/` | B | P3, P5 |
| `findings.csv` — dòng `r2_qa` | B | Sau khi A lock |
| `r3_diag/`, `findings.csv` dòng `r3_diag`, `40_decision_log.csv` | C | P4, sau khi B chốt QA |
| `00_setup/`, `10_*`, `20_*`, `30_*`, `45_*`, `46_*`, `50_*`, `TEAMMATES.md` | C | Suốt buổi |

## 3. Bàn giao theo pha

| Mốc | Người giao → nhận | File / commit / mã khóa | Người nhận đã kiểm gì? | Trạng thái / vướng mắc |
|---|---|---|---|---|
| P0 · Chốt môi trường và vai | C → A, B | mode.json (slice B4-mid), doctor.txt, team.json — commit e7e8c24; TEAMMATES.md — commit 516fc17 | A/B nhận slice B4-mid; doctor không còn ✗ (CVAT 2.75.0, cảnh báo khác 2.74.x không ảnh hưởng lộ trình offline) | Xong. Lúc đầu làm trên nhánh `123`, đã gộp về `main`; từ đó chỉ dùng `main` |
| P1 · Hiệu chuẩn C0 | A → C, B | p1_calib/annotations.xml, lock.txt — mã B81F-32C1, commit 28ed17e | C mở reference sau lock (lock_before_reveal: true); compare: 6/6 vật reference khớp, 1 box thừa L1 center | Dòng calib L1 trong findings.csv chờ phân xử ở P4 |
| P2 · Khóa bản đầu | A → B, C | r1_craft/annotations.xml, lock.txt, selfqc.md — slice B4-mid, mã 2AA4-1FBB, commit 225cb65 (selfqc cập nhật b70644b, 137e275) | C kiểm lock còn nguyên (intact_lock OK 2AA4-1FBB); B chạy `qa` trên bản đã khóa | Self-QC còn 3 cảnh báo truncated (261480 L2, L3; 265065 L5) — không relock, ghi thành finding r1_craft. Git trên Windows đổi LF→CRLF làm mã tính ra 8B21-B72D; sửa bằng .gitattributes (121490d), nội dung XML không đổi |
| P3 · Chốt QA mù | B → C, A | r2_qa/qa_review.md, qa_overlay.html, 4 dòng r2_qa, 3 ảnh screenshots/ — commit 9cd56a2, sửa hình thức 9e9c8df | C kiểm: đủ 3 frame, mỗi nhận xét có frame/object_ref/rule_id và ảnh; findings qua `triage`; chưa mở reference/model B4-mid | Xong — B xác nhận "QA đã chốt" trước khi C mở reference/model |
| P4 · Quyết định sửa | C → A, B | findings.csv (22 dòng r3_diag + calib), 40_decision_log.csv D1–D6, r3_diag/ — commit 48f1c73 | A/B pull và duyệt decision log; `triage` báo Findings hợp lệ | Xong. Giao A rework: 265065 L6→Truck, thêm R5/R6/R7, sửa 3 truncated; escalate D4 (reference nghi thiếu 265065 L5) và D5 (model ThreeWheeler) |
| P5 · Kiểm bản sửa | A → B → C | rework/annotations-v2.xml, lock2.txt mã 605F-D50D (79f9873); qa_review.md phần kiểm lại (a693a7e); delta.md (3f2eb7a) | B kiểm lại từng ca và ký xác nhận; C kiểm lock2 khớp file; delta: mid missing 4→1, matched 9→12 | Xong. R7 không thêm (D7, E5_unresolved). Box Pedestrian mới v2 L1 (265065, x 283–299) là người thật → giữ, E0, gộp ticket 1 (D8) |
| P6 · Chốt nộp | A, B → C | 10_error_card, 20_guideline_patch, 30_escalation_ticket, 45_review_plan, 50_exit_ticket, manifest.json — commit a693a7e; TEAMMATES — commit cuối | Cả ba xác nhận exit ticket; B kiểm gold plan; `check` exit 0, failed_gates rỗng | Xong về hình thức; C gửi link repo + SHA commit cuối qua kênh lớp |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: 265065 L6 — B nêu ở QA là xe tải nhỏ bị gán Car (R04); A giải thích lựa chọn ban đầu; C đối chiếu ảnh, R3 và M1 đều Truck → sửa thành Truck ở rework (decision log D1, finding r3_diag L6, ảnh screenshots/qa_265065_L5_truncated_L6_pickup.png). Ca thứ hai: 265065 L5 — giữ box, sửa thuộc tính, escalate nghi reference thiếu (D4, ticket 1).
- Ca còn mở: (1) 265065 R7 — vật mờ, chưa chắc là người → E5_unresolved (D7), phép kiểm tiếp: frame liền kề/hỏi người quản lý reference; (2) hai escalation (ticket 1 → qa, ticket 2 → ai_team) chờ phản hồi. Người theo dõi: Lâm (C).
- Đóng góp của A/B/C vào kế hoạch và exit ticket: Lâm (C) soạn sensor_context, 45_sampling_plan, 46_gold_set_plan, 45_review_plan và câu trả lời exit ticket; Cường (B) kiểm 46_gold_set_plan và cung cấp nhận xét R05/R04 cho exit ticket; Khôi (A) cung cấp ca 265065 L5 và kết quả rework; cả ba đã đọc và tick xác nhận exit ticket.
- Công cụ hỗ trợ: A không dùng công cụ pre-label ngoài; nhãn r1_craft làm trong CVAT từ prefill của lab (lock ghi prefill_kept 1, new 14). C dùng trợ lý AI (Claude Code) để hỗ trợ đọc báo cáo, soạn nháp findings/decision log/các file kế hoạch và kiểm hồ sơ; nhóm đã đọc lại, đối chiếu ảnh và xác nhận nội dung.
- Thay đổi phân công nếu có: không đổi vai. Ngoại lệ nhỏ: C sửa hình thức r2_qa/qa_review.md (mã khóa, chính tả tên, đặt tên và dẫn ảnh bằng chứng) theo đồng ý của B, commit 9e9c8df; nội dung nhận xét của B giữ nguyên.

## 5. Xác nhận trước khi nộp

- [X] A xác nhận nhãn và export đúng phiên bản: Lê Minh Khôi — r1_craft lock 2AA4-1FBB, rework lock2 605F-D50D
- [x] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: Lê Hùng Cường — r2_qa/qa_review.md (QA 9cd56a2 trước khi mở reference 48f1c73; ký phần kiểm lại P5)
- [x] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: Vũ Tùng Lâm — local_quality.json khớp sha256 r1_craft; intact_lock OK cho calib/r1_craft/rework; `check` exit 0
- [x] manifest.json tại commit chốt có failed_gates rỗng.
- [x] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [X] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.
