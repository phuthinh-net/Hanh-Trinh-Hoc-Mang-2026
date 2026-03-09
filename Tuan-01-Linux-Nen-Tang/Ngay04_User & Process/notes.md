# 🐧 Ngày 4: User & Process Management

> **Mục tiêu:** Quản lý không gian người dùng (User Home) và kiểm soát các chương trình đang chạy (Process) trên hệ thống.

## Ⅰ. Lý thuyết & Lệnh trọng tâm

### 1. Quản lý Người dùng (User)

* **`adduser`**: Khi chạy lệnh này, Linux thực hiện:
  
  * Tạo một User mới.
  * **Tạo thư mục Home**: Ví dụ tạo user `sinhvien`, hệ thống tạo `/home/sinhvien` (giống như `/home/dinh-thinh` của bạn).
  * Thiết lập mật khẩu và quyền sở hữu thư mục cho user đó.

* **`sudo`**: Quyền quản trị tối cao, bắt buộc phải có để thực hiện các thao tác quản lý hệ thống.

### 2. Tiến trình & PID (Process Control)

* **PID (Process ID)**: Mã số định danh duy nhất của mỗi ứng dụng đang chạy. Bạn cần PID để điều khiển hoặc tắt ứng dụng đó.

* **Theo dõi tài nguyên**:
  
  * `top`: Xem trực tiếp ứng dụng nào đang chiếm dụng CPU/RAM (Real-time). 
  * `ps aux`: Liệt kê tất cả ứng dụng đang chạy để lấy mã PID.

* Lệnh `kill`:
  
  * `kill <PID>`: Tắt ứng dụng an toàn.
  * `kill -9 <PID>`: **Cưỡng ép** tắt ngay lập tức (Dùng khi ứng dụng bị treo).

---

## 3. ⌨️ Các phím tắt trong giao diện `top`

| Phím    | Chức năng             | Ứng dụng thực tế                                                   |
|:------- |:--------------------- |:------------------------------------------------------------------ |
| **`q`** | **Thoát (Quit)**      | Quay lại màn hình Terminal.                                        |
| **`M`** | **Sắp xếp RAM**       | Đẩy các ứng dụng ngốn nhiều bộ nhớ nhất lên đầu bảng.              |
| **`P`** | **Sắp xếp CPU**       | Đẩy các ứng dụng đang làm máy lag/nóng lên đầu bảng.               |
| **`k`** | **Kill nhanh**        | Nhập trực tiếp số PID để tắt app ngay trong giao diện `top`.       |
| `c`     | **Hiện tên đầy đủ**   | Hiển thị đường dẫn chi tiết (giúp nhận diện `gnome-calculator`).   |
| `u`     | **Lọc theo User**     | Nhập tên user để chỉ xem tiến trình của người đó (vd: dinh-thinh). |
| `1`     | **Chi tiết CPU**      | Xem thông số hoạt động của từng nhân CPU riêng biệt.               |
| `V`     | **Dạng cây (Forest)** | Hiển thị quan hệ Cha-Con giữa các tiến trình.                      |
| `z`     | **Đổi màu**           | Bật/tắt màu sắc để giao diện dễ quan sát hơn.                      |
| `h`     | **Trợ giúp (Help)**   | Mở bảng hướng dẫn tất cả phím tắt có trong `top`.                  |

---

## 🔍 Tiêu điểm: Lệnh `grep` (Global Regular Expression Print)

**Lệnh `grep` dùng để làm gì?**

* **Định nghĩa**: Đây là công cụ **tìm kiếm và lọc văn bản**. Nó giống như tính năng **Ctrl + F** nhưng dành cho dòng lệnh.
* **Tại sao cần dùng với Process?**: Danh sách tiến trình (`ps aux`) thường rất dài. Dùng `grep` để lọc ra đúng ứng dụng bạn muốn xử lý.
* **Cú pháp phổ biến**:
  * `ps aux | grep <tên_app>`: Lọc danh sách tiến trình chỉ lấy những dòng chứa tên ứng dụng đó.
  * `grep "từ_khóa" tên_file`: Tìm từ khóa bên trong một file văn bản.

---

## Ⅱ. Các lệnh ứng dụng thực tế

| Lệnh                 | Ý nghĩa thực tế                                |
| -------------------- | ---------------------------------------------- |
| `sudo adduser <tên>` | Tạo user mới & thư mục `/home/<tên>` mới.      |
| `ps aux`             | grep <tên_app>`                                |
| `top`                | Kiểm tra xem app nào đang làm máy bị lag/nóng. |
| `kill -9 <PID>`      | "Khai tử" một app đang bị treo cứng.           |

---

## Ⅲ. Thực hành (Homework Lab)

### Bước 1: Tạo không gian mới (Giống `/home/dinhthinh`)

1. Tạo một user mới tên là `ubuntu_lab`:
   
   ```bash
   sudo adduser ubuntu_lab
   ```

```
2. Kiểm tra xem thư mục home mới đã được tạo chưa:
```bash
ls /home
```

*(Kết quả: Sẽ thấy thêm thư mục `/home/ubuntu_lab` bên cạnh `/home/dinhthinh`).*

### Bước 2: Truy tìm và Xử lý Process với `grep`

1. Mở một ứng dụng bất kỳ (ví dụ: Firefox hoặc một trình giả lập).

2. Tìm PID của tiến trình đó bằng cách phối hợp `ps` và `grep`:
   
   ```bash
   ps aux | grep firefox
   ```

```
3. Sử dụng mã PID tìm được ở cột thứ 2 để tắt ứng dụng:
```bash
kill -9 <số_PID_vừa_tìm>
```

---

**Ghi chú:** Việc sử dụng thành thạo `grep` kết hợp với các lệnh khác (dùng dấu gạch đứng `|`) là kỹ năng quan trọng nhất để làm chủ Terminal trên Ubuntu.
