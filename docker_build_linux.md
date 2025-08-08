
# Hướng dẫn Sử dụng Docker trên Arch Linux

## 1. Kiểm tra trạng thái Docker

### Kiểm tra các Docker image hiện có
- **Cú pháp**:  
  ```bash
  sudo docker images
  ```
- **Giải thích**: Liệt kê tất cả các Docker image trên máy. Hiển thị: `Repository`, `Tag`, `Image ID`, `Created`, `Size`.
- **Ví dụ**:
  - Khi chưa có image nào: Kết quả trống.
  - Sau khi build image: Sẽ hiển thị danh sách image đã tạo.

### Kiểm tra các Docker container đang chạy
- **Cú pháp**:  
  ```bash
  sudo docker ps
  ```
- **Giải thích**: Chỉ hiển thị các container đang chạy.

### Kiểm tra tất cả container (đang chạy và đã dừng)
- **Cú pháp**:  
  ```bash
  sudo docker ps -a
  ```
- **Giải thích**: Thêm tùy chọn `-a` để hiển thị tất cả container (bao gồm cả đã dừng).

---

## 2. Xây dựng Docker Image

### Build image từ Dockerfile
- **Cú pháp**:  
  ```bash
  sudo docker build -t <ten_image> .
  ```
- **Ví dụ**:  
  ```bash
  sudo docker build -t machine_learning .
  ```
- **Giải thích**:
  - `build`: Lệnh xây dựng image.
  - `-t`: Gán tên cho image.
  - `.`: Chỉ định Dockerfile ở thư mục hiện tại.

- **Lưu ý**: Lần đầu build sẽ chậm nếu phải tải base image từ Docker Hub.

---

## 3. Chạy Docker Container

### Chạy container và mở shell tương tác
- **Cú pháp**:  
  ```bash
  sudo docker run -it <ten_image> bash
  ```
- **Ví dụ**:  
  ```bash
  sudo docker run -it machine_learning bash
  ```
- **Giải thích**:
  - `-it`: Cho phép tương tác qua terminal.
  - `bash`: Mở Bash shell bên trong container.

### Chạy container không tương tác
- **Cú pháp**:  
  ```bash
  sudo docker run <ten_image>
  ```

### Chạy container và tự xóa sau khi hoàn tất
- **Cú pháp**:  
  ```bash
  sudo docker run --rm <ten_image>
  ```
- **Giải thích**: Container sẽ bị xóa sau khi kết thúc.

---

## 4. Xóa Docker Container và Image

### Xóa container
- **Cú pháp**:  
  ```bash
  sudo docker rm <ID_container_1> [<ID_container_2> ...]
  ```
- **Ví dụ**:  
  ```bash
  sudo docker rm d85e1234abc
  ```

### Xóa image
- **Cú pháp**:  
  ```bash
  sudo docker rmi <ID_image>
  ```
- **Ví dụ**:  
  ```bash
  sudo docker rmi ee9e5678def
  ```

---

## 5. Các lệnh tiện ích trong Terminal

### Xóa sạch Terminal
- **Cú pháp**:  
  ```bash
  clear
  ```

### Xem lịch sử lệnh
- **Cú pháp**:  
  ```bash
  history
  ```

### Chạy lại một lệnh từ lịch sử
- **Cú pháp**:  
  ```bash
  !<số_thứ_tự_lệnh>
  ```
- **Ví dụ**:  
  ```bash
  !2005
  ```

---

## Ghi chú dành cho Arch Linux

- Đảm bảo Docker đã được cài đặt bằng cách chạy:
  ```bash
  sudo pacman -S docker
  ```

- Kích hoạt và khởi động dịch vụ Docker:
  ```bash
  sudo systemctl enable docker
  sudo systemctl start docker
  ```

- Để chạy Docker mà không cần `sudo`, thêm user vào nhóm `docker`:
  ```bash
  sudo usermod -aG docker $USER
  # Sau đó đăng xuất và đăng nhập lại
  ```

---
