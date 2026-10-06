# Bài 1: Khảo sát FHS và Phân quyền File/Folder nâng cao

## 1. Mục tiêu

* Khảo sát cấu trúc thư mục FHS trên Linux.
* Tạo cấu trúc thư mục cho ứng dụng web.
* Thực hành phân quyền bằng octal.
* Thực hành thay đổi Owner và Group bằng `chown`.

## 2. Cấu trúc thư mục

Đã tạo cấu trúc:

```text
/var/www/my-app/
├── public/
└── logs/
```

## 3. Các lệnh đã thực hiện

### Bước 1: Tạo thư mục

```bash
sudo mkdir -p /var/www/my-app/public
sudo mkdir -p /var/www/my-app/logs
```

### Bước 2: Đổi Owner và Group

Sử dụng tài khoản hiện tại làm Owner và nhóm `www-data` làm Group:

```bash
sudo chown -R $USER:www-data /var/www/my-app
```

### Bước 3: Phân quyền thư mục public

Thư mục `public` yêu cầu:

* Owner: đọc, ghi, thực thi
* Group: đọc, thực thi
* Others: không có quyền

Sử dụng quyền `750`:

```bash
sudo chmod 750 /var/www/my-app/public
```

### Bước 4: Phân quyền thư mục logs

Thư mục `logs` yêu cầu:

* Owner: đọc, ghi, thực thi
* Group: đọc, ghi, thực thi
* Others: không có quyền

Sử dụng quyền `770`:

```bash
sudo chmod 770 /var/www/my-app/logs
```

## 4. Kiểm tra

Lệnh kiểm tra:

```bash
ls -la /var/www/my-app
```

Kết quả:

```text
drwxrwx--- 2 student www-data 4096 Oct  6 21:50 logs
drwxr-x--- 2 student www-data 4096 Oct  6 21:50 public
```

> `student` là tài khoản non-root được sử dụng trong bài thực hành. Nếu tài khoản thực tế có tên khác thì thay `student` bằng tên tài khoản tương ứng.

## 5. Giải thích quyền

### public - 750

```text
rwx r-x ---
```

* Owner: `rwx` → đọc, ghi, truy cập.
* Group: `r-x` → đọc và truy cập.
* Others: `---` → không có quyền.

### logs - 770

```text
rwx rwx ---
```

* Owner: `rwx` → đọc, ghi, truy cập.
* Group: `rwx` → đọc, ghi, truy cập.
* Others: `---` → không có quyền.

## 6. Kết luận

Đã hoàn thành việc tạo cấu trúc thư mục `/var/www/my-app`, thiết lập Owner là tài khoản non-root hiện tại, Group là `www-data`, đồng thời phân quyền `750` cho `public` và `770` cho `logs`.
