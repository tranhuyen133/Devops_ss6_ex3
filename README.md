# Báo cáo Bài 3: Cấu hình tường lửa UFW và chẩn đoán cổng mạng

## 1. Mục tiêu
Dùng UFW bảo vệ máy chủ: chặn mọi kết nối vào theo mặc định, chỉ mở cổng SSH (22) và cổng ứng dụng web (8080).

## 2. Các lệnh đã thực hiện
# Chính sách mặc định
ufw default deny incoming
ufw default allow outgoing

# Mở cổng SSH trước (tránh mất kết nối quản trị)
ufw allow 22/tcp

# Mở cổng ứng dụng web
ufw allow 8080/tcp

# Bật tường lửa
ufw enable

## 3. Giải thích
- deny incoming: chặn toàn bộ kết nối đi vào theo mặc định (an toàn).
- allow outgoing: máy chủ vẫn kết nối ra ngoài được (update, API...).
- Mở 22/tcp TRƯỚC khi enable để không bị ngắt phiên SSH đang quản trị.
- Mở 8080/tcp cho ứng dụng web lắng nghe.

## 4. Kết quả kiểm tra (ufw status verbose)
Status: active
Default: deny (incoming), allow (outgoing)

To            Action      From
--            ------      ----
22/tcp        ALLOW IN    Anywhere
8080/tcp      ALLOW IN    Anywhere

## 5. Kết luận
Tường lửa đã active, chặn mặc định đầu vào và chỉ mở đúng cổng cần thiết (22 cho SSH, 8080 cho web), đảm bảo máy chủ an toàn mà vẫn giữ được kết nối quản trị.
