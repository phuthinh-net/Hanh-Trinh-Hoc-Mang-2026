# 🐧 Linux Ngày 3: Phân quyền (Permissions)

> **Mục tiêu:** Hiểu linh hồn của bảo mật Linux thông qua hệ thống phân quyền file và thư mục.

---

## 1. Công thức Vàng (rwx)

Mỗi file/thư mục có 3 loại quyền, tương ứng với các giá trị số cố định:

| Quyền       | Ký hiệu | Giá trị | Ý nghĩa                                        |
|:----------- |:-------:|:-------:|:---------------------------------------------- |
| **Read**    | `r`     | **4**   | Đọc nội dung file / Liệt kê file trong thư mục |
| **Write**   | `w`     | **2**   | Sửa file / Thêm, xóa file trong thư mục        |
| **Execute** | `x`     | **1**   | Chạy file script / Truy cập (`cd`) vào thư mục |

### 💡 Cách tính quyền nhanh:

Cộng các giá trị lại cho từng nhóm đối tượng:

* **7** (4+2+1): Toàn quyền (`rwx`)
* **6** (4+2+0): Đọc & Ghi (`rw-`)
* **5** (4+0+1): Đọc & Chạy (`r-x`)
* **3** (0+2+1): Ghi & Chạy (`-wx`) -> *Hiếm dùng*
* **0** (0+0+0): Không có quyền (`---`) -> *Dùng để khóa sạch*

---

## 2. Đối tượng sở hữu (Ownership)

Thứ tự phân quyền luôn xuất hiện theo bộ ba: **User - Group - Others**

*Ví dụ:* `chmod 755 file.sh`

1. **User (7):** Chủ sở hữu có toàn quyền.
2. **Group (5):** Nhóm người dùng chỉ được đọc và chạy.
3. **Others (5):** Những người khác chỉ được đọc và chạy.

---

## 3. Lệnh quan trọng (Key Commands)

### 🔹 chmod (Change Mode) - Đổi quyền

* **Dùng số:** `chmod 644 document.txt` (Quyền phổ biến cho file văn bản).
* **Dùng chữ:** `chmod +x script.sh` (Thêm quyền thực thi cho tất cả).

### 🔹 chown (Change Owner) - Đổi chủ

* **Đổi user:** `sudo chown nickname file.txt`
* **Đổi cả user & group:** `sudo chown user:group file.txt`
* **Đổi toàn bộ thư mục con:** `sudo chown -R user:group folder/`

---

## 4. ⚠️ LƯU Ý QUAN TRỌNG (Áp dụng nhiều nhất)

* **Quyền `x` với Thư mục:** Đây là chìa khóa để vào cửa. Bạn phải có quyền `x` thì mới có thể `cd` vào bên trong thư mục đó.
* **Quyền `x` file:** Cần để thực thi các file script hoặc phần mềm và để chạy file bắt buộc có `./` phía trước (Vd: `./script.sh`). 
* **Bộ số "kinh điển":** 
  * `644`: Dùng cho mọi file văn bản, ảnh, code (Bạn sửa được, người khác xem được).
  
  * `755`: Dùng cho thư mục hoặc các file muốn chạy (script).
* **Tuyệt đối tránh `777`:** Không bao giờ dùng `777` cho các file quan trọng vì nó mở toang cửa cho virus hoặc các tiến trình lạ phá hoại.
* **Mẹo thực hành:** Khi bị báo "Permission denied", hãy bình tĩnh gõ `ls -l` để xem file đó có đúng là của mình không trước khi dùng đến `sudo`.

--- 

## 5. Thực hành nhanh (Quick Lab)

1. **Kiểm tra quyền:** `ls -l`
2. **Thử thách "Tự khóa":**
   * Tạo file: `touch test.txt`
   * Khóa sạch quyền: `chmod 000 test.txt`
   * Thử đọc: `cat test.txt` -> *(Bị từ chối!)*
3. **Mở khóa lại:** `chmod 644 test.txt`

---

*Ghi chú: Luôn dùng `sudo` khi thao tác với các file hệ thống ngoài thư mục Home.*
