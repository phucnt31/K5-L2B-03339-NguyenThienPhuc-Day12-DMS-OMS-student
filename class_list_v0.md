# Danh sách lớp v0 — Nguyễn Thiên Phúc · G05

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `face` (box) | Mỗi khung hình một mặt tài xế | Định vị khuôn mặt làm vùng quan tâm (ROI) để cắt ảnh đầu vào cho mạng trích xuất điểm mốc và phân tích cảm xúc/trạng thái | Có (nhìn rõ biên dạng khuôn mặt trán đến cằm, tai đến tai) |
| 2 | `eye_left` / `eye_right` | `open`, `closed`, `unknown` | Tính tỉ lệ mở mí mắt (EAR - Eye Aspect Ratio), phát hiện trạng thái ngủ gật (micro-sleep) hoặc buồn ngủ khi nhắm mắt kéo dài | Có, trừ trường hợp tròng kính bị đốm phản xạ LED hồng ngoại che khuất (ghi `unknown`) |
| 3 | `gaze_zone` | `road`, `mirror_l`, `mirror_r`, `mirror_c`, `cluster`, `center`, `lap`, `other` | Xác định vùng chú ý thị giác; phát hiện xao nhãng khi tài xế nhìn lệch khỏi mặt đường phía trước (`road`) quá thời gian an toàn (nhìn xuống đùi `lap`, màn hình trung tâm `center`) | Có (kết hợp hướng con ngươi và góc quay đầu yaw/pitch của tài xế) |
| 4 | `glasses` | `none`, `clear`, `sun`, `unknown` | Điều chỉnh trọng số thuật toán nhận diện mắt khi có kính cản trở; hỗ trợ phát hiện kính râm cản trở tầm nhìn trong điều kiện thiếu sáng | Có (trên NIR kính râm có thể nhìn xuyên thấu như kính cận, cần chú ý gọng kính) |
| 5 | `hand` (box, `on_wheel`) | `whose`: driver/passenger · `side`: left/right · `on_wheel`: `yes`, `no`, `unknown` | Giám sát trạng thái chạm tay vào vô lăng (Hands-on/Hands-off detection) trong các cấp độ lái xe tự động (L2/L3) để yêu cầu tài xế tiếp quản điều khiển | Có (độ tương phản cao giữa da tay và vô lăng xe) |
| 6 | `phone` (box, `state`) | `state`: `held`, `mounted`, `lap` | Phát hiện vi phạm sử dụng điện thoại khi đang điều khiển phương tiện (áp tai gọi điện, cầm tay nhắn tin) gây nguy hiểm | Có (nhận diện qua hình khối chữ nhật phẳng và độ phản xạ đặc trưng của màn hình kính) |
| 7 | `face13` (skeleton) | 13 điểm: mí mắt, khóe mắt, khóe môi, mũi | Cung cấp điểm mốc hình học chính xác cao để tính toán độ mở mắt, độ ngáp miệng và góc xoay 3D (Head Pose 3DoF) | Có (được hỗ trợ bởi hệ thống chiếu sáng LED NIR 940 nm đồng đều trên mặt) |

## OMS (ít nhất 6 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (box, `seat`) | `seat`: driver, front_passenger, rear_left, rear_middle, rear_right | Nhận diện sự hiện diện của hành khách tại từng vị trí ghế; tự động tối ưu hóa điều hòa nhiệt độ cục bộ và kích hoạt hệ thống giải trí | Có (thân nhiệt và phản xạ bề mặt cơ thể phân biệt rõ với ghế ngồi) |
| 2 | `seatbelt` | `worn_correct`, `worn_incorrect`, `not_worn`, `unknown` | Cảnh báo thắt dây an toàn cho từng ghế; điều chỉnh lực bung của túi khí thông minh theo tư thế thắt dây an toàn | Có thể thấy dải chéo trên áo sáng màu; khó phân biệt trên áo tối màu (chuyển `unknown`) |
| 3 | `child_seat` (box, `occupied`) | `seat`: theo xe · `occupied`: `no`, `unknown` | Nhắc nhở kiểm tra trẻ em ở hàng ghế sau trước khi khóa cửa xe (Child Presence Detection - CPD), phòng chống sốc nhiệt nguy hiểm | Có (hình khối đệm dày và khung vỏ nhựa của ghế trẻ em nổi bật) |
| 4 | `infant_seat` (box, `facing`) | `seat`: theo xe · `facing`: `rear`, `front` | Tự động vô hiệu hóa (tắt) túi khí ghế phụ phía trước khi phát hiện nôi em bé lắp quay ngược hướng (`facing = rear`) để tránh chấn thương khi va chạm | Có (dựa trên cấu trúc hình học đặc thù của nôi xách và quai xách dạng vòm) |
| 5 | `object` (box, `type`) | `seat`: theo xe · `type`: `bag`, `box`, `cup`, `other` | Cảnh báo hành lý hoặc tài sản bỏ quên trong xe (Left Object Detection) sau chuyến đi; cảnh báo vật thể nặng không cố định có thể văng khi phanh gấp | Có (nhận diện theo đường nét biên dạng hình khối của đồ vật) |
| 6 | `frame_meta` (tag) | `modality`: rgb, ir · `light`: day, night, unknown · `camera_blocked`: yes, no | Cung cấp thông tin môi trường chụp để hệ thống tự động kích hoạt bộ lọc hoặc chuyển đổi mô hình thị giác phù hợp (ngày/đêm); cảnh báo camera bị che | Có (nhận biết cảm biến chuyển sang chế độ hồng ngoại đen trắng) |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. **Câu hỏi:** Dưới camera cận hồng ngoại (NIR 940 nm), nhiều loại kính râm có tròng kính trong suốt nhìn xuyên thấu thấy rõ mắt như kính cận (chỉ khác là gọng kính dày hoặc có lớp phản xạ nhẹ). Trong trường hợp này, thuộc tính `glasses` nên ưu tiên gán là `clear` (theo cảm nhận thực tế của cảm biến hình ảnh) hay `sun` (nếu biết đó là kính râm ngoài đời)?
   - **Khung ví dụ:** `D02.png`
   - **Bạn tạm gán thế nào và vì sao:** Tạm gán `glasses = clear` vì trên dữ liệu đào tạo cảm biến, model thị giác máy tính chỉ học các đặc trưng quang học hiển thị trên ảnh (tròng trong suốt xuyên thấu). Nếu đốm phản xạ NIR che khuất mắt thì chuyển trạng thái mắt thành `unknown`.

2. **Câu hỏi:** Khi ghế trẻ em (`child_seat`) hoặc nôi em bé (`infant_seat`) bị che phủ bởi một tấm chăn mỏng hoặc áo khoác trùm kín khiến camera hoàn toàn không thể quan sát được bên trong có vật thể hay em bé hay không, quy ước gán thuộc tính `occupied` và vẽ box `object` được ưu tiên như thế nào để không làm lệch tập dữ liệu huấn luyện?
   - **Khung ví dụ:** `S06_ir.png`
   - **Bạn tạm gán thế nào và vì sao:** Tạm gán `occupied = unknown` cho ghế và vẽ thêm một box `object` (`type = other`) bao quanh tấm vải phủ ngoài với cùng vị trí `seat`, tuân thủ nguyên tắc không được suy đoán khi vùng quan sát bị che lấp hoàn toàn.
