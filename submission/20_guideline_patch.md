# Guideline patch

- **Rule mới đề xuất:** R05a — `truncated=true` **chỉ khi** box chạm biên ảnh (cạnh cách biên ≤ 2 px) hoặc có ít nhất một góc box nằm ngoài vòng kính của frame (tra `assets/frames.csv`). Vật bị xe khác, người, biển hiệu hay thân xe ego che một phần là `occluded=true`, **không** phải truncated. Nếu vật vừa bị vòng kính cắt vừa bị che thì bật cả hai. Người gán nhãn phải xử lý cảnh báo `truncated khác dự kiến` của `selfqc` trước khi khóa; muốn giữ khác cảnh báo thì ghi lý do trong self-QC.
- **Áp dụng cho:** attribute `truncated` và `occluded` của cả 6 class, mọi zone; đặc biệt vật nhỏ ở mid/center bị xe khác che (ThreeWheeler, Bike đỗ lề đường).
- **Vì sao luật hiện tại (`docs/02-rules-vi.md`) không đủ:** R05 nói truncated là “bị cắt bởi vòng kính hoặc biên” nhưng không cho phép kiểm cụ thể, nên ở B4-mid người gán nhãn đánh `truncated=true` cho 3 box nằm giữa khung chỉ vì bị vật khác che (261480 L2, L3; 265065 L5 — findings r1_craft/r2_qa, decision log D2). Self-QC đã cảnh báo nhưng không có luật nói phải xử lý cảnh báo đó. Truncated **được** so với reference (khác occluded, R11), nên hiểu sai ảnh hưởng trực tiếp tới báo cáo.
- **`rules_version` mới:** v1.0.0 → v1.1.0
- **Hiệu lực từ:** round gán nhãn tiếp theo (slice/lượt kế tiếp sau bài nộp này); không sửa ngược bản r1_craft đã khóa — các ca trong B4-mid đã xử lý ở rework v2.
