# BTVN2_PhatTrienUngDungVoiMaNguonMo

## kết nối với ubuntu
<img width="1245" height="558" alt="image" src="https://github.com/user-attachments/assets/a1285977-2c0f-4230-821d-56e6d47af25a" />
ssh admin123@192.168.0.122. pass:11111111
ip -4 addr show ens33

## BƯỚC 2: TẠO CẤU TRÚC THƯ MỤC TRÊN UBUNTU
mkdir -p ~/quanlycamdo/django_app
cd ~/quanlycamdo

## BƯỚC 3: TẠO CÁC FILE CẤU HÌNH (DOCKER & DJANGO)
## dùng sudo nano để tạo các file sau:
### File requirements.txt

### File Dockerfile (Cho Django)
<img width="1145" height="725" alt="image" src="https://github.com/user-attachments/assets/658dabf6-2393-4395-94e4-2f68b0d13345" />
## File docker-compose.yml
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6555c624-985e-457b-9fed-3af1634fabd7" />
## File Setting
<img width="1240" height="771" alt="image" src="https://github.com/user-attachments/assets/e5e96e19-dc2e-4513-b2e5-225066c3a3da" />

## BƯỚC 4: KHỞI TẠO DỰ ÁN DJANGO
Chạy lệnh này để build các service:
docker compose up -d --build
<img width="1144" height="757" alt="image" src="https://github.com/user-attachments/assets/73debff1-df25-4030-8995-73f205571c41" />

Sau đó, khởi tạo code Django vào thư mục đã mount:
docker compose exec web django-admin startproject core .

Trang web: Mở trình duyệt Windows gõ http://192.168.179.128:8080 (Hiện tên lửa là thắng).

CSDL: Mở http://192.168.179.128:9631 (User: root, Pass: 123).

chạy lệnh này để Django nạp dữ liệu vào MariaDB::
docker compose exec web python manage.py migrate
<img width="838" height="661" alt="image" src="https://github.com/user-attachments/assets/4a0fbca6-a38d-415f-8038-5693a9c0c8b8" />


## BƯỚC 5: CẤU HÌNH DJANGO KẾT NỐI MARIADB
dùng sudo nano django_app/core/settings.py tìm phần DATABASES và sửa thành:

## BƯỚC 6: TẠO MODEL & MIGRATION
Định nghĩa bảng trong django_app/core/models.py
Chạy lệnh để tạo bảng thật trong MariaDB:
docker compose exec web python manage.py makemigrations
docker compose exec web python manage.py migrate

Tạo tài khoản Admin để đăng nhập:
docker compose exec web python manage.py createsuperuser

## BƯỚC 7: KIỂM TRA & PUBLIC (CLOUDFLARE)
<img width="651" height="151" alt="image" src="https://github.com/user-attachments/assets/cf4cd93b-b4eb-4e27-a22c-acef500adcac" />


Trang Admin: Truy cập http://<IP_Ubuntu>/admin. Đăng nhập và thêm bớt con nợ thoải mái.

PhpMyAdmin: Truy cập http://<IP_Ubuntu>:9630 để soi các bảng.

Cloudflare Tunnel:

Cài cloudflared trên Ubuntu.

Chạy lệnh: cloudflared tunnel --url http://localhost:80

Nó sẽ cho anh một cái link sub-domain dạng xxx.trycloudflare.com. Copy link đó chụp ảnh nộp bài là xong!
