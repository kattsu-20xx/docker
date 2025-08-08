
# Hướng Dẫn Sử Dụng Docker Trên PowerShell (Windows)

## I. Chuẩn Bị Ban Đầu

### 1. Cài đặt Docker Desktop

- Truy cập: [https://www.docker.com/get-started](https://www.docker.com/get-started)
- Tải file cài đặt cho Windows và cài đặt như sau:
  - Nhấn **"Download for Windows"**
  - Chạy file cài đặt → **OK** → đợi hoàn tất → **Close**
- Mở Docker Desktop:
  - Nhấn nút Windows → tìm "docker" → chọn **Docker Desktop**
  - Nhấp **Accept** điều khoản (có thể bỏ qua đăng nhập)

### 2. Mở PowerShell

- Nhấn nút Windows → tìm "PowerShell" → chọn **Windows PowerShell**
- Gợi ý: đặt PowerShell bên phải, Docker Desktop bên trái để dễ quan sát

---

## II. Các Khái Niệm Chính (Tóm Tắt)

| Thành phần         | Mô tả                                                                 |
|--------------------|------------------------------------------------------------------------|
| **Docker Desktop** | Giao diện quản lý Docker Image, Container                              |
| **Dockerfile**     | File hướng dẫn cách tạo Docker Image (giống như công thức nấu ăn)     |
| **Docker Image**   | Khuôn mẫu để tạo Container (giống class trong OOP)                    |
| **Docker Container**| Thực thể chạy thực tế từ Image (giống object trong OOP)              |

**Mối quan hệ:** `Dockerfile → Docker Image → Docker Container`

---

## III. Các Bước Làm Việc Với Docker Trên Terminal

### 1. Clone Repository chứa Dockerfile mẫu

- Trong Docker Desktop → "How do I run a container" → **Next**
- Sao chép câu lệnh:

```bash
git clone https://github.com/docker/welcome-to-docker
```

- Trong PowerShell, dán và chạy lệnh trên

### 2. Di chuyển vào thư mục dự án

```bash
cd welcome-to-docker
```

### 3. Kiểm tra nội dung và xem Dockerfile

```bash
ls
cat dockerfile
```

Hoặc mở Dockerfile bằng Notepad nếu muốn.

---

### 4. Tìm Hiểu Các Lệnh Dockerfile

| Lệnh                    | Mô tả                                                                 |
|-------------------------|----------------------------------------------------------------------|
| `FROM <image>`          | Image cơ sở (giống kế thừa)                                          |
| `WORKDIR <dir>`         | Thư mục làm việc bên trong Container                                 |
| `COPY <src> <dest>`     | Sao chép file từ máy host vào Container                             |
| `RUN <command>`         | Chạy lệnh khi build image                                            |
| `EXPOSE <port>`         | Mở cổng trong container (cho web app, API,...)                       |
| `CMD ["cmd", "arg1"]`   | Lệnh mặc định khi container khởi động                                |

> Ví dụ:  
> `FROM ubuntu`  
> `RUN apt-get update -y && apt-get install python3 -y`  
> `CMD ["python3", "script.py"]`

---

### 5. Build Docker Image

```bash
docker build -t <image_name> .
```

Ví dụ:

```bash
docker build -t welcome-to-docker .
```

- `-t`: đặt tên cho image  
- `.`: build từ thư mục hiện tại

---

### 6. Run Docker Container

#### a. Chạy ở chế độ tương tác (bash)

```bash
docker run -it <image_name> bash
```

- Dùng `ls`, `cd` để khám phá bên trong
- Thoát bằng:
  - `Ctrl+P`, `Ctrl+Q` → **thoát mà không dừng**
  - `exit` hoặc `Ctrl+D` → **thoát và dừng**

#### b. Chạy để thực thi lệnh trong `CMD`

```bash
docker run <image_name>
```

- Chạy lệnh đã khai báo trong `CMD` của Dockerfile

---

## IV. Ví Dụ Thực Hành: Build Image Chạy Script Machine Learning

### 1. Tạo Dockerfile

Tên file: `dockerfile` (không phần mở rộng)

### 2. Nội dung Dockerfile

```dockerfile
FROM ubuntu
RUN apt-get update -y
RUN apt-get install python3 -y
RUN apt-get install python3-scikit-learn -y
WORKDIR /source
COPY Iris_classification.py .
CMD ["python3", "Iris_classification.py"]
```

> - File `Iris_classification.py` phải nằm cùng thư mục với Dockerfile.

### 3. Build Image

```bash
docker build -t iris-ml .
```

### 4. Run Container

```bash
docker run iris-ml
```

- Container sẽ chạy script và hiển thị output nếu có.

---

## Ghi Chú

- Mỗi khi sửa Dockerfile hoặc file Python, bạn **phải build lại image**
- Có thể kiểm tra các image đã build bằng:

```bash
docker images
```

- Xem container đang chạy hoặc đã chạy:

```bash
docker ps -a
```

- Xóa container hoặc image nếu cần:

```bash
docker rm <container_id>
docker rmi <image_name>
```

---

## Tài Nguyên Tham Khảo

- [Docker chính thức](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
