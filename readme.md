# WordPress Project with Git & Docker CI/CD Deployment

## 🧩 Mục Tiêu
Triển khai một website WordPress sử dụng Git để quản lý source code và Docker để thực hiện CI/CD tự động lên server thông qua môi trường DirectAdmin.

---

## 📁 Cấu Trúc Dự Án

├── docker-compose.yml
├── Dockerfile
├── .env
├── .gitignore
├── .github/
│ └── workflows/
│ └── deploy.yml
├── public_html/ (hoặc thư mục chứa source WP)
├── readme.md


---

## ⚙️ Công Cụ & Công Nghệ

- **Git**: quản lý source code
- **Docker**: môi trường chạy WordPress
- **GitHub Actions**: chạy CI/CD
- **DirectAdmin + FTP/SSH**: quản lý hosting/server

---

## 🚀 Quy Trình CI/CD

1. **Push Code lên GitHub**
   - Mỗi khi `push` hoặc `merge` vào branch `main`, GitHub Actions sẽ tự động chạy workflow.

2. **GitHub Actions Workflow**
   - Tự động build Docker image
   - Kết nối SSH tới server (hoặc upload qua FTP nếu không có SSH)
   - Dừng container cũ (nếu có)
   - Triển khai container mới
   - Đồng bộ code

3. **Kết quả**
   - Website được cập nhật tự động mà không cần thao tác tay trên server

---

## 📦 Docker Compose Ví Dụ

```yaml
version: '3.8'

services:
  wordpress:
    image: wordpress:latest
    ports:
      - "8080:80"
    volumes:
      - ./public_html:/var/www/html
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: wp_user
      WORDPRESS_DB_PASSWORD: wp_pass
      WORDPRESS_DB_NAME: wp_db
  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: wp_db
      MYSQL_USER: wp_user
      MYSQL_PASSWORD: wp_pass
      MYSQL_ROOT_PASSWORD: rootpass
