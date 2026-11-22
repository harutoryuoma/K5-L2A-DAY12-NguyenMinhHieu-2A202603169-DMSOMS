# Danh sách lớp v0 — Nguyễn Minh Hiếu · G1

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**
Xóa 2 dòng ví dụ trước khi nộp.

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` / `seatbelt` | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Xác định tài xế và tình trạng đeo dây an toàn; phát hiện trường hợp dây đeo sai vị trí nếu có đủ dấu hiệu. | **Có điều kiện**: dải dây có thể thấy trên NIR, nhưng bóng tối hoặc tay che khiến phải để `unknown`. |
| 2 | `face` / `eye_left`, `eye_right` | `open` / `closed` / `unknown` (mỗi mắt riêng) | Theo dõi trạng thái mắt theo chuỗi khung hình để hỗ trợ đánh giá mức độ tỉnh táo; không suy ra buồn ngủ từ một ảnh đơn lẻ. | **Có điều kiện**: vùng mí mắt có thể quan sát được; phản xạ kính hoặc vùng tối làm mất chi tiết. |
| 3 | `face` / `glasses` | `none` / `clear` / `sun` / `unknown` | Nhận biết kính để xử lý khác biệt về độ tin cậy khi đánh giá mắt và mốc mặt. | **Có điều kiện**: thấy gọng kính, nhưng NIR có thể làm kính râm trông trong suốt hoặc gây phản xạ. |
| 4 | `face` / `gaze_zone` | `road` / `mirror_l` / `mirror_r` / `mirror_c` / `cluster` / `center` / `lap` / `other` | Xác định vùng chú ý của tài xế để phát hiện tình huống nhìn lệch khỏi hướng lái trong chuỗi thời gian. | **Có điều kiện**: suy từ hướng đầu và mắt; ảnh tối hoặc kính che làm khó xác định chính xác. |
| 5 | `face13` | 13 điểm: 8 mốc mắt, 1 chóp mũi, 4 mốc miệng; cờ `occluded` / `outside` | Ước lượng hình học khuôn mặt, hỗ trợ phân tích hướng đầu và trạng thái vùng mắt/miệng. | **Có điều kiện**: NIR thường còn đường nét mặt nhưng mốc bị che/chói không được tự đặt cho đủ. |
| 6 | `hand` / `on_wheel` | `whose`: `driver` / `passenger`; `side`: `left` / `right`; `on_wheel`: `yes` / `no` / `unknown` | Theo dõi vị trí tay và việc chạm vô lăng; phục vụ đánh giá tương tác với hệ thống lái. | **Có điều kiện**: hình tay có thể thấy rõ; bóng tối hoặc che khuất khiến `on_wheel = unknown`. |
| 7 | `phone` / `state` | `held` / `mounted` / `lap` (chỉ khi xác nhận có điện thoại) | Phát hiện điện thoại và trạng thái sử dụng, hỗ trợ phân tích hoạt động gây xao nhãng. | **Có điều kiện**: cần thấy một phần hình dạng máy; không gán chai, kính hoặc vật tối không rõ là `phone`. |
| 8 | `face` (bounding box) | Có box / không có box nếu mặt không đủ nhìn thấy | Định vị vùng mặt để các mô-đun mắt, gaze và keypoint xử lý đúng khu vực. | **Có điều kiện**: vẽ khi thấy đủ đặc điểm khuôn mặt; quá tối hoặc che gần hết thì không ép gán. |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` | Có box / không có box | Xác định có người chiếm vị trí ghế sau; làm nền cho tính năng nhắc người còn trong xe. | **Có** nếu hình người nhìn rõ; IR-sim giữ hình dáng, nhưng có thể mất chi tiết trong vùng tối. |
| 2 | `person.seat` | `rear_left` / `rear_middle` / `rear_right` | Xác định đúng vị trí người trong xe để phân biệt ghế có người và ghế trống. | **Có điều kiện**: chủ yếu dựa vào vị trí trong cabin, không dựa vào màu. Trái ảnh là `rear_right`. |
| 3 | `person.seatbelt` | `not_worn` / `unknown` trong bộ SVIRO | Xác định người ngồi có thể hiện dây an toàn hay không; dữ liệu bài lab này không cung cấp ví dụ `worn_correct`. | **Có điều kiện**: chỉ ghi `not_worn` khi thấy rõ không có dây; không chắc thì `unknown`. |
| 4 | `face` | Có box / không có box | Hỗ trợ nhận biết vùng mặt của người lớn, phân biệt hình người với đồ vật hoặc ghế trong cabin. | **Có điều kiện**: IR-sim có thể giữ hình dáng mặt, nhưng thiếu màu và có vùng thiếu sáng. |
| 5 | `child_seat` / `occupied` | `occupied = no` / `unknown` | Phát hiện ghế trẻ em và đánh giá ghế có đang trống hay khó xác định; hỗ trợ giám sát cấu hình khoang hành khách. | **Có** qua đường viền ghế; **không chắc** trạng thái bên trong khi tối hoặc bị che. |
| 6 | `infant_seat` / `facing` | `rear` / `front` | Phát hiện nôi/ghế em bé dạng xách và chiều quay để biết vị trí lắp đặt. | **Có điều kiện**: nhận qua cấu trúc nôi/tay xách, nhưng hướng quay có thể khó phân biệt nếu bị che. |
| 7 | `object` / `type` | `bag` / `box` / `cup` / `other` | Nhận biết đồ vật để tránh nhầm ghế có đồ vật thành ghế có người, hỗ trợ cảnh báo đồ đạc bỏ quên. | **Có điều kiện**: hình dạng và vị trí có thể thấy, nhưng thiếu thông tin màu; chọn `other` khi không đủ bằng chứng. |
| 8 | `object.seat` | `rear_left` / `rear_middle` / `rear_right` | Xác định đồ vật nằm trên ghế nào, giúp phân biệt trạng thái từng vị trí ghế. | **Có điều kiện**: vị trí thường xác định được nhưng vật lớn bắc qua ranh giới ghế có thể gây mơ hồ. |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: Nếu tài xế đang tháo kính và kính còn ở rất gần mặt, chưa rõ đã rời khỏi mặt hoàn toàn, face.glasses nên là none, clear hay unknown ở đúng khung chuyển tiếp? Guideline v1.0 giải thích kính đã cầm trên tay là none nhưng chưa xác định ranh giới chính xác cho trạng thái đang tháo.
- Khung ví dụ: D06.png (kính được đưa gần vùng mặt).
- Bạn tạm gán thế nào và vì sao: unknown nếu không chắc kính còn đeo hay đã tháo; chỉ đổi thành none khi nhìn rõ kính đã rời mặt. Ghi chú để coach xác nhận.
2. Câu hỏi: Nếu một đồ vật lớn nằm trên vùng tiếp giáp hai ghế phía sau, thuộc tính object.seat nên tính theo phần lớn diện tích, tâm của box hay vị trí vật thực sự đặt lên ghế? Guideline v1.0 quy định gọi ghế theo xe nhưng chưa quy định cách xử lý vật bắc qua hai ghế.
- Khung ví dụ: 05_rgb.png / S05_ir.png (kiểm tra vật lớn ở vùng ghế giữa).
- Bạn tạm gán thế nào và vì sao: 1.
   - chọn rear_middle nếu phần tựa chính của vật thuộc ghế giữa; nếu kiểm tra lại thấy vật thuộc ghế khác thì sửa theo ảnh. Ghi chú phần ranh giới mơ hồ và hỏi coach.
