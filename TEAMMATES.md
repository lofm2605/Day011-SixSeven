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
| A · Gán nhãn | [Lê Minh Khôi] | [2A202602163] | Khoi | Parking/C0/slice, self-QC, lock, rework | [Link file/commit và mô tả phần đã làm] |
| B · QA độc lập | [Lê Hùng Cường] | [2A20260218] | [Cuong] | Review trước reference, finding QA, kiểm lại ca sửa | [Link file/commit và mô tả phần đã làm] |
| C · Chẩn đoán & điều phối | [Vũ Tùng Lâm] | [2A202602181] | [Lam] | Báo cáo, phân xử, kế hoạch, tích hợp, check và nộp | [Link file/commit và mô tả phần đã làm] |

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
| P0 · Chốt môi trường và vai | C → A, B | mode.json (slice B4-mid), doctor.txt, TEAMMATES.md, commit [Điền] | [Điền] | [Điền] |
| P2 · Khóa bản đầu | A → B, C | [XML, lock.txt, slice, code, commit] | [Điền] | [Điền] |
| P3 · Chốt QA mù | B → C, A | [review, findings, ảnh, commit] | [Điền] | [Điền] |
| P4 · Quyết định sửa | C → A, B | [finding, decision log, commit] | [Điền] | [Điền] |
| P5 · Kiểm bản sửa | A → B → C | [v2, lock2, review kiểm lại, delta] | [Điền] | [Điền] |
| P6 · Chốt nộp | A, B → C | [manifest, commit chốt] | [Điền] | [Điền] |

## 4. Bất đồng và phối hợp

- Một ca đã phân xử: [Frame/object/rule; ý kiến A/B; bằng chứng; quyết định và link]
- Ca còn mở: [Nội dung, người theo dõi, phép kiểm tiếp theo; nếu không còn thì ghi rõ]
- Đóng góp của A/B/C vào kế hoạch và exit ticket: [Điền phần việc thực tế]
- Công cụ hỗ trợ: [Nếu A dùng notebooks/day11-prelabel-A-colab.ipynb để dựng nháp, ghi rõ đã báo Lab Coach và A đã soát/sửa từng box]
- Thay đổi phân công nếu có: [Thời điểm, lý do, người nhận; nếu không đổi thì ghi rõ]

## 5. Xác nhận trước khi nộp

- [ ] A xác nhận nhãn và export đúng phiên bản: [Tên / bằng chứng]
- [ ] B xác nhận đã QA độc lập trước reference và kiểm lại ca sửa: [Tên / bằng chứng]
- [ ] C xác nhận báo cáo đúng bản khóa, các file đầy đủ và check exit 0: [Tên / bằng chứng]
- [ ] manifest.json tại commit chốt có failed_gates rỗng.
- [ ] Repo nhóm Public, ảnh và các bằng chứng mở được.
- [ ] C đã push và gửi link repo nhóm + commit qua kênh lớp công bố.
