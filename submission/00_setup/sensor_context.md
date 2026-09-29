# Sensor context

Nguồn quan sát: 3 frame của slice chung B4-mid (adasind_249480, adasind_261480, adasind_265065) và bảng vòng kính
`assets/frames.csv`. Người soạn: Lâm (C); A/B đối chiếu lại trên ảnh.

- Rig: một camera fisheye duy nhất, ảnh dọc 1080×1920. Camera nhìn về phía trước theo hướng xe chạy, lệch về lề
  trái đường (thấy vạch giữa đường bên trái và lề/cửa hàng bên phải). Trong khung có chân người ngồi sau và bàn chân đi
  dép ở góc dưới trái, nên theo quan sát camera nhiều khả năng gắn trên một xe hai/ba bánh ở độ cao thấp, không phải
  ô tô. ADASIND không kèm tài liệu rig; vị trí gắn, độ cao, góc nghiêng ở đây chỉ là suy đoán từ ảnh.
- `ego_body`: phần thân/người trên xe ego thấy ở **góc dưới bên trái**, sát vòng kính (chân, dép, ống quần của
  người trên xe) trong cả 3 frame B4-mid; ở 249480 phần này kéo dài từ khoảng giữa bên trái xuống đáy vòng kính.
  Không thấy capo hay gương. Theo R07, mỗi frame có phần này cần một polygon `ignore_region` reason `ego_body`
  (bản r1_craft có 3 polygon ego_body cho 3 frame).
- Vòng kính: hình tròn lệch trái-giữa ảnh, tâm khoảng (430–565, 985–1035) px, bán kính 802–819 px (toàn bộ 48 frame:
  r 771–839 px). Đường kính (~1620 px) lớn hơn bề ngang ảnh nên vòng tròn bị **biên trái/phải cắt**; phần tối nằm ở
  trên (y < ~180–225) và dưới (y > ~1790–1850). Vùng trong vòng kính chiếm khoảng **76–78 % khung hình**; phần còn
  lại là `lens_border` (2 polygon import sẵn mỗi frame, R08).
- Giới hạn: chỉ có dữ liệu một camera ADASIND; không có thông số rig/calibration chính thức, không có timestamp
  đồng bộ với camera khác. Không dùng các số trên như calibration thật.
