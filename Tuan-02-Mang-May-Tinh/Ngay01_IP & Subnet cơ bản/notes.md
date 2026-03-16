# 🌐 Ngày 1: IP & Subnet cơ bản

> **Mục tiêu:** Hiểu rõ sự khác biệt giữa các loại địa chỉ IP, cách kiểm tra IP trên Linux và nắm vững khái niệm cơ bản về Subnet Mask.

### 1. Phân biệt IP Public và IP Private

* **IP Public (Địa chỉ công cộng):**
* Là địa chỉ duy nhất trên toàn thế giới do nhà mạng (ISP) cung cấp.
* Dùng để định danh thiết bị khi đi ra ngoài Internet.
* **Cách kiểm tra nhanh từ Terminal:** `curl ifconfig.me`

* **IP Private (Địa chỉ nội bộ):**
* Sử dụng trong mạng nội bộ (mạng LAN gia đình, công ty).
* Các dải phổ biến: `192.168.x.x`, `10.x.x.x`, `172.16.x.x`.
* Giúp tiết kiệm địa chỉ IP và bảo mật thiết bị bên trong mạng.

### 2. Kiểm tra IP trên Linux

* **Lệnh thực hiện:** `ip a` (viết tắt của `ip address`).
* **Thông tin quan trọng cần chú ý:**
* **lo (loopback):** Địa chỉ `127.0.0.1`, dùng để thiết bị tự kết nối với chính nó.
* **ens33/ens32/eth0:** Tên card mạng phổ biến trên Ubuntu/VMware.
* **inet:** Dòng hiển thị địa chỉ IP hiện tại của máy (ví dụ: `192.168.1.10/24`).

### 3. Khái niệm bổ trợ quan trọng (Phải biết)

* **Subnet Mask:** Giúp hệ thống xác định phần nào là địa chỉ mạng (Network) và phần nào là thiết bị (Host). Cách viết thông dụng: `255.255.255.0` (tương ứng `/24`).
* **Default Gateway:** Là "cánh cửa" để máy tính đi ra ngoài mạng khác. Xem bằng lệnh: `ip route` (Tìm dòng `default via...`).
* **DNS (Domain Name System):** Chuyển đổi tên miền (https://www.google.com/url?sa=E&source=gmail&q=google.com) thành IP. Nếu không có DNS, bạn sẽ không lướt web bằng tên miền được.
* **Công cụ `curl` (Client URL):** - **Tác dụng:** Là "trình duyệt web dạng dòng lệnh". Dùng để **truyền tải dữ liệu, kiểm tra kết nối Internet, tải file hoặc gọi API.**
* **Tại sao cần dùng:** Cực kỳ nhanh để kiểm tra xem một trang web có "sống" hay không hoặc lấy IP Public mà không cần mở trình duyệt.

### 4. Bài tập thực hành (Lab)

#### **📂 Khởi tạo cấu trúc bài tập thực hành**

```bash
mkdir -p Network_Lab/Branch_A Network_Lab/Branch_B
touch Network_Lab/Branch_A/ip_config.txt Network_Lab/Branch_B/ip_config.txt
```

#### **🛠 Thực hành trên Terminal**

1. **Kiểm tra IP nội bộ:** Chạy lệnh `ip a` và xác định dòng `inet`.
2. **Kiểm tra IP công cộng:** Chạy lệnh `curl ifconfig.me`.
3. **Kiểm tra kết nối web:** Chạy `curl -I google.com` (Nếu trả về `HTTP/1.1 200 OK` là mạng ngon).
4. **Lưu thông tin vào file:**
   
   ```bash
   # Ghi thông tin IP nội bộ, Gateway và IP Public vào file report
   ip a > Network_Lab/Branch_A/my_network_info.txt
   ip route >> Network_Lab/Branch_A/my_network_info.txt
   curl ifconfig.me >> Network_Lab/Branch_A/my_network_info.txt
   ```

```

### 5. Trạng thái tiến độ

* [x] Hiểu sự khác biệt giữa IP Public và Private.
* [x] Biết cách dùng `ip a`, `ip route` và `curl`.
* [x] Tạo thành công cấu trúc thư mục thực hành Lab và lưu thông tin.

---

**Mẹo nhỏ cho bạn:** Khi làm việc trên VMware, nếu bạn thấy IP có dạng `192.168.x.x` thì thường là do card mạng đang để chế độ **Bridged**, còn nếu thấy `172.x.x.x` hoặc dải lạ thì thường là **NAT**.
