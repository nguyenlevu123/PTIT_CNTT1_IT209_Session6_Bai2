Bài 2: Quản trị Tường lửa UFW cho Cụm Dịch vụ Multi-port
Mục tiêu
Thiết lập tường lửa UFW bảo vệ cụm dịch vụ chạy multi-port: SSH (22), Nginx HTTP (80), Spring Boot (8082).
Cô lập cổng hệ quản trị cơ sở dữ liệu MySQL (3306) khỏi truy cập từ bên ngoài Internet.
1. Các bước Cấu hình Tường lửa UFW
Bước 1: Khai báo chính sách mặc định
sudo ufw default deny incoming
sudo ufw default allow outgoing
Bước 2: Cho phép các cổng dịch vụ công khai
# Cho phép SSH quản trị
sudo ufw allow 22/tcp

# Cho phép Nginx Web Server
sudo ufw allow 80/tcp

# Cho phép Spring Boot Application
sudo ufw allow 8082/tcp
Bước 3: Kích hoạt tường lửa
sudo ufw enable
2. Kiểm tra Trạng thái UFW (sudo ufw status verbose)
$ sudo ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere                  
80/tcp                     ALLOW IN    Anywhere                  
8082/tcp                   ALLOW IN    Anywhere                  
22/tcp (v6)                ALLOW IN    Anywhere (v6)             
80/tcp (v6)                ALLOW IN    Anywhere (v6)             
8082/tcp (v6)              ALLOW IN    Anywhere (v6)             
3. Đánh giá Bảo mật
Cổng 3306/tcp (MySQL) hoàn toàn không có trong quy tắc ALLOW IN, đảm bảo dữ liệu chỉ có thể kết nối nội bộ từ 127.0.0.1.
Tất cả cổng đi vào khác mặc định bị từ chối (Default: deny incoming).
