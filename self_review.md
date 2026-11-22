# Tự đánh giá — Nguyễn Minh Hiếu · G01

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S01_ir | Box `child_seat` / các vật trên ghế | `box` *(nghi vấn)* | So lại hộp với mép đối tượng trên ảnh IR và ghế tương ứng; đừng lấy vị trí ghế theo trái/phải của màn hình. Nếu không có lỗi, đổi thành `ok`. | **Đã sửa** |
| S05_ir | `child_seat.occupied` | `guess` *(nghi vấn)* | Nếu vùng bên trong ghế bị tối hoặc che, dùng `unknown` thay vì suy từ ảnh RGB. Xác nhận lại loại ghế và box trong CVAT. | **Đã sửa** |
| D01 | `face13` – điểm vùng mắt | `flag` *(nghi vấn)* | Kiểm tra các điểm bị phản xạ che: `occluded` nếu xác định được vị trí, `outside` nếu không thể xác định. Đối chiếu thứ tự mắt theo người khi ảnh xoay. | **Đã sửa** |
| D05 | `phone`, `hand`, `face13` | `box` *(nghi vấn)* | Chỉ giữ nhãn `phone` khi thấy cạnh/góc/màn hình điện thoại; ôm sát vật nhìn thấy và rà lại tay trái/phải. | **Đã sửa** |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: guess (đoán mò khi bị tối hoặc che)

Vì sao mình mắc: vì mình dựa vào bản RGB suy luận mà gán nhãn

Lần sau tránh bằng cách: Nếu vùng bên trong ghế bị tối hoặc che, dùng unknown thay vì suy từ ảnh RGB.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó: …
