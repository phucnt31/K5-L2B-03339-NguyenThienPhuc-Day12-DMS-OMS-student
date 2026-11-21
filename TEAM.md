# TEAM — Ngày 12

Mã bộ ảnh: **G05** · Hình thức: cá nhân

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Nguyễn Thiên Phúc | 03339 | có | Nguyễn Khánh Trình | 52 |

Ca hai bạn vẫn không thống nhất và đã hỏi coach (ghi tên ảnh + đối tượng):

- `D03.png` & `D05.png` - `face13 (mouth_right)`: Cờ `occluded` vs `outside` khi khóe miệng nằm sát mép hoặc bị khuất (Phúc đánh `outside` vì không thấy vị trí mốc; Trình đánh `occluded` vì vẫn ước lượng được vị trí tương đối theo giải phẫu mặt. Coach hướng dẫn: nếu mặt không bị cắt khỏi khung ảnh và ước lượng được vị trí thì ưu tiên `occluded`).
- `S04_rgb.png` & `S04_ir.png` - Phân loại ghế trẻ em: `infant_seat` (nôi xách) hay `child_seat` (ghế ngồi) do góc chụp chéo từ camera trước xe BMW X5. Coach hướng dẫn: nhìn quai xách nôi phía trên để phân biệt (có quai xách dạng vòm là `infant_seat`).

## Cá nhân

Mỗi người một mục, 1–2 dòng mỗi ý.

### Nguyễn Thiên Phúc - 03339
- Phần mình làm: Tự gán nhãn toàn bộ 22 ảnh cốt lõi (S01–S08 RGB/IR-sim và D01–D06 NIR). Tự kiểm tra bằng script cabin_check ở Checkpoint A, Checkpoint B và Final. Chạy lệnh diff đối chiếu với bạn Nguyễn Khánh Trình, rà soát 52 dòng bất đồng và thống nhất theo guideline.
- Điều mình học được hôm nay: Hiểu sâu sắc quy ước không gian cabin: gọi ghế theo xe (trái ảnh là `rear_right`) và gọi trái/phải giải phẫu theo người (trên ảnh Drive&Act xoay 90° thì mắt trái có y lớn hơn); phân biệt hiện tượng vật lý giữa ảnh NIR thật (chói kính, mắt phản xạ) và IR mô phỏng; tuân thủ nguyên tắc "không thấy thì ghi unknown" thay vì đoán.
