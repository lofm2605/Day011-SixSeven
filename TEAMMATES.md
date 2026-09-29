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
- Commit chốt bài: [SHA hoặc URL commit]

## 2. Ba vai chính

| Vai | Họ và tên | MSSV | Tên định danh trong mode | Trách nhiệm | Bằng chứng đóng góp |
|---|---|---|---|---|---|
| A · Gán nhãn | Lê Minh Khôi | 2A202602163 | Khoi | Parking/C0/slice, self-QC, lock, rework | Parking 3 parking_line + 1 free_space (e99ebd9); C0 lock B81F-32C1 (28ed17e); r1_craft B4-mid lock 2AA4-1FBB (225cb65); self-QC 9 mục + 3 finding r1_craft (b70644b, 137e275); rework P5: [Điền] |
| B · QA độc lập | Lê Hùng Cường | 2A202602218 | Cuong | Review trước reference, finding QA, kiểm lại ca sửa | QA mù B4-mid: qa_review.md 4 nhận xét (3 × R05 truncated, 1 × R04 pickup→Car), 4 finding r2_qa, 3 ảnh bằng chứng (9cd56a2); kiểm lại ca sửa P5: [Điền] |
| C · Chẩn đoán & điều phối | Vũ Tùng Lâm | 2A202602181 | Lam | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp | mode/doctor/TEAMMATES (e7e8c24, 516fc17); sửa .gitattributes giữ mã khóa (121490d); sensor_context, 45_sampling_plan, 46_gold_set_plan (7b14b49); chẩn đoán P4–P6 và nộp: [Điền] |

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
| P3 · Chốt QA mù | B → C, A | r2_qa/qa_review.md, qa_overlay.html, 4 dòng r2_qa, 3 ảnh screenshots/ — commit 9cd56a2, sửa hình thức 9e9c8df | C kiểm: đủ 3 frame, mỗi nhận xét có frame/object_ref/rule_id và ảnh; findings qua `triage`; chưa mở reference/model B4-mid | Chờ B xác nhận "QA đã chốt" trước khi C chạy P4 |
| P4 · Quyết định sửa | C → A, B | [finding, decision log, commit] | [Điền] | [Điền] |
| P5 · Kiểm bản sửa | A → B → C | [v2, lock2, review kiểm lại, delta] | [Điền] | [Điền] |
| P6 · Chốt nộp | A, B → C | [manifest, commit chốt] | [Điền] | [Điền] |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: [Điền sau P4 — dự kiến 265065 L6: B cho là pickup → Truck (R04), A giải thích lựa chọn Car; bằng chứng screenshots/qa_265065_L5_truncated_L6_pickup.png]
- Ca còn mở: 4 nhận xét QA (261480 L2, L3; 265065 L5 — R05 truncated; 265065 L6 — R04) và dòng calib C0 L1 chờ phân xử ở P4; người theo dõi: Lâm (C).
- Đóng góp của A/B/C vào kế hoạch và exit ticket: [Điền phần việc thực tế]
- Công cụ hỗ trợ: A không dùng công cụ pre-label ngoài; nhãn r1_craft làm trong CVAT từ prefill của lab (lock ghi prefill_kept 1, new 14).
- Thay đổi phân công nếu có: không đổi vai. Ngoại lệ nhỏ: C sửa hình thức r2_qa/qa_review.md (mã khóa, chính tả tên, đặt tên và dẫn ảnh bằng chứng) theo đồng ý của B, commit 9e9c8df; nội dung nhận xét của B giữ nguyên.

## 5. Xác nhận trước khi nộp

- [ ] A xác nhận nhãn và export đúng phiên bản: [Tên / bằng chứng]
- [ ] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: [Tên / bằng chứng]
- [ ] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: [Tên / bằng chứng]
- [ ] manifest.json tại commit chốt có failed_gates rỗng.
- [ ] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [ ] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.
