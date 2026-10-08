# Bài 3: Viết Dockerfile đóng gói trang Web HTML tĩnh

## 1. Mục tiêu
Tự đóng gói một trang HTML tĩnh thành Docker Image siêu ngắn gọn bằng Dockerfile dựa trên image Nginx Alpine.

---

## 2. Cấu trúc thư mục
```text
homework/session_09/ex3/
├── Dockerfile
├── index.html
└── README.md
```

---

## 3. Nội dung các tệp tin

### 3.1. `index.html`
```html
<h1>Hello Docker Session 09!</h1>
```

### 3.2. `Dockerfile`
```dockerfile
FROM nginx:alpine
COPY index.html /usr/share/nginx/html/index.html
```

- `FROM nginx:alpine`: Sử dụng base image Nginx chạy trên nền Alpine Linux siêu nhẹ.
- `COPY index.html /usr/share/nginx/html/index.html`: Sao chép file `index.html` từ máy host vào thư mục phục vụ web tĩnh mặc định của Nginx.

---

## 4. Hướng dẫn thực hiện và kiểm tra

### Bước 1: Build Docker Image
Chạy lệnh sau tại thư mục chứa Dockerfile (`homework/session_09/ex3`):
```bash
docker build -t my-html-app:v1 .
```

### Bước 2: Khởi chạy container
Chạy container ở chế độ nền (detached), map cổng 8081 của host tới cổng 80 của container:
```bash
docker run -d -p 8081:80 --name html-app my-html-app:v1
```

### Bước 3: Kiểm tra kết quả
Sử dụng lệnh `curl`:
```bash
curl http://localhost:8081
```

Hoặc truy cập trình duyệt tại địa chỉ: `http://localhost:8081`

**Kết quả mong đợi:**
```text
<h1>Hello Docker Session 09!</h1>
```

---

## 5. Dọn dẹp tài nguyên (khi hoàn thành)
```bash
docker stop html-app
docker rm html-app
```
