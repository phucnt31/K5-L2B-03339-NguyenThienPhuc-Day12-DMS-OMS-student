# Tự đánh giá — Nguyễn Thiên Phúc · G05

## 1. Tự rà soát 4 cảnh

Nghỉ tay 1 phút, mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S02_rgb.png | child_seat | guess | Đã chọn occupied='yes' vì thấy có vật bên trong ghế, vi phạm guideline (child_seat chỉ nhận no/unknown) | Đã sửa |
| S04_rgb.png | frame_meta | wrong_class | Gán nhầm modality='ir' cho ảnh RGB (do copy tag từ ảnh ir) | Đã sửa |
| D01.png | object | extra | Vẽ box object cho chai/cốc trên tay tài xế (DMS không vẽ object) | Đã sửa |
| D05.png | face / face13 | flag | eye_left=unknown nhưng chưa bật cờ occluded cho điểm left_eye_* bị phản xạ | Đã sửa |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Gán thuộc tính `light = night` cho ảnh IR cabin (thay vì `unknown` cho ảnh dựng SVIRO) và vẽ thừa box `object` ở các khung hình DMS tài xế.

Vì sao mình mắc: Thấy ảnh hồng ngoại có nền tối đen nên theo cảm tính gán là ban đêm (`night`); đồng thời quen tay từ phần OMS nên khi thấy tài xế cầm vật thể đã vẽ thêm box `object`.

Lần sau tránh bằng cách: Đọc kỹ bảng phân định ở GUIDE §4.2 (DMS chỉ gán person, face, face13, hand, phone; không gán object); luôn nhớ quy tắc số 1: ảnh dựng mô phỏng hoặc không thấy nguồn sáng tự nhiên thì luôn đặt `light = unknown`.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó: Ở ảnh `S02_rgb.png`, mình gán `child_seat` với `occupied = yes`, trong khi bạn Nguyễn Khánh Trình gán `occupied = unknown`. Bạn Trình đúng vì GUIDE §4.1 và §4.8 quy định `child_seat` chỉ cho phép `no` hoặc `unknown` (tuyệt đối không có `yes` do dataset không có trẻ em ngồi; nếu có đồ vật đặt trong ghế trẻ em thì phải vẽ 2 box riêng `child_seat` và `object`). Mình học được rằng cần kiểm tra kỹ schema thuộc tính cho phép và không tự suy đoán giá trị theo trực giác.
