# 🐧 Linux Ngày 5: Service & Log

> **Mục tiêu:** Kiểm soát trạng thái vận hành của hệ thống thông qua quản lý dịch vụ và phân tích lịch sử log.

---

## 1. Quản lý Service với `systemctl`

Lệnh `systemctl` là công cụ chính để điều khiển hệ thống `systemd`, dùng để quản lý các dịch vụ (services) chạy ngầm.

* **Kiểm tra trạng thái:** `systemctl status <tên_service>`
* **Khởi động dịch vụ:** `systemctl start <tên_service>`
* **Dừng dịch vụ:** `systemctl stop <tên_service>`
* **Khởi động lại:** `systemctl restart <tên_service>`
* **Tự động chạy khi boot:** `systemctl enable <tên_service>`
* **Tắt tự động chạy khi boot:** `systemctl disable <tên_service>`

---

## 2. Kiểm tra Log hệ thống

Các tệp tin log lưu trữ mọi hoạt động của hệ điều hành, giúp chẩn đoán và khắc phục lỗi.

* **Thư mục chứa log:** `/var/log`
* **Xem log hệ thống (Ubuntu):** `cat /var/log/syslog`
* **Xem log thời gian thực:** `tail -f /var/log/syslog` (Rất hữu ích để theo dõi lỗi ngay khi nó xảy ra).
* **Truy xuất log bằng journald:** `journalctl -u <tên_service>`

---

---

## ⚠️ Lưu ý quan trọng (Dùng nhiều sau này)

* **Restart vs Reload:** * `restart`: Dừng + Chạy lại (gây gián đoạn).
  * `reload`: Cập nhật cấu hình (không gây gián đoạn).
* **Xử lý sự cố (Troubleshooting):** * Sử dụng `journalctl -u <service> -n 50` để xem 50 dòng log gần nhất của một dịch vụ khi nó báo lỗi "Failed".
* **An ninh:** * Luôn kiểm tra `/var/log/auth.log` để theo dõi các nỗ lực đăng nhập trái phép vào hệ thống.

---

## 3. Bài tập thực hành

1. **Thao tác:** Thử cài đặt Apache (`sudo apt install apache2`), sau đó dùng `systemctl status` để xem nó có đang chạy không.
2. **Phân tích:** Mở một cửa sổ terminal mới, chạy `tail -f /var/log/auth.log` và thử thực hiện lệnh `sudo` để xem log ghi lại quá trình xác thực.
