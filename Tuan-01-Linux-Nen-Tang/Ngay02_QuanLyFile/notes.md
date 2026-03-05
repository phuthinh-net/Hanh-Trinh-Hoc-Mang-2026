# 🐧 Ngày 2: Quản lý File & Thư mục

> **Mục tiêu:** Nắm vững các lệnh điều hướng và thao tác với file cơ bản.

## 1. Bảng so sánh nhanh (Cheat Sheet)

| Lệnh    | Ý nghĩa           | Ví dụ                |
|:------- |:----------------- |:-------------------- |
| `touch` | Tạo file trống    | `touch note.txt`     |
| `mkdir` | Tạo thư mục       | `mkdir data`         |
| `cp`    | Sao chép          | `cp file1 file2`     |
| `mv`    | Di chuyển/Đổi tên | `mv old.txt new.txt` |
| `rm`    | Xóa (Cẩn thận!)   | `rm file.txt`        |

---

## 2. Ghi chú quan trọng (Key Points)

- **File vs Directory:** - Directory là "cái túi", File là "đồ vật".
  
  - Dùng `-r` (recursive) khi muốn áp dụng `cp` hoặc `rm` lên thư mục.

- **Mẹo đổi tên:** Linux không có lệnh `rename` riêng biệt phổ biến, ta dùng `mv` (move từ tên cũ sang tên mới).

- **Lưu ý về lệnh `mv`:** 
  
  1. `mv A B` (Nếu B chưa có) -> Đổi tên A thành B.
  2. `mv A B` (Nếu B có rồi) -> Di chuyển A vào trong B (Đường dẫn mới: `B/A`).

- **Tạo nhiều file và folder :**
  
  - Sử dụng dấu ngoặc nhọn `{}` giúp bạn viết lệnh ngắn gọn hơn, tránh lặp lại các tiền tố hoặc hậu tố giống nhau.
    
    | Mục tiêu               | Cách thủ công (Cơ bản)              | Cách dùng `{ }` (Pro)        |
    |:---------------------- |:----------------------------------- |:---------------------------- |
    | **Nhiều thư mục**      | `mkdir Folder1 Folder2 Folder3`     | `mkdir Folder{1,2,3}`        |
    | **Thư mục lồng nhau**  | `mkdir -p App/src App/css App/js`   | `mkdir -p App/{src,css,js}`  |
    | **Nhiều file theo số** | `touch f1.txt f2.txt f3.txt...`     | `touch file{1..10}.txt`      |
    | **File ở nhiều nơi**   | `touch dir1/note.txt dir2/note.txt` | `touch {dir1,dir2}/note.txt` |
    
    ---
    
    > [!NOTE]
    > **Lưu ý quan trọng:**
    > 
    > - **Không dùng khoảng trắng:** Bên trong `{ }`, bạn không được để khoảng trắng sau dấu phẩy (Ví dụ: `{src,css}` ✅, `{src, css}` ❌).
    > - **Dãy số `..`:** Sử dụng `{1..10}` để tạo số thứ tự liên tục một cách nhanh chóng.
    > - **Môi trường:** Hoạt động tốt nhất trên Terminal của **Linux** và **macOS** (Bash, Zsh).

---

## 3. Cây thư mục thực hành (Lab)

*Cấu trúc dự án nhỏ hôm nay:*

- `Project/`
  - `docs/` -> chứa `readme.md`
  - `src/`  -> chứa `main.sh`
  - `backup/`

### Lệnh đã thực hiện:

```bash
mkdir -p Project/docs Project/src Project/backup
touch Project/docs/readme.md Project/src/main.sh
```

### 📂 Khởi tạo cấu trúc đa dự án

Lệnh này tạo cùng lúc 2 project với các thư mục và file hoàn toàn khác nhau.

**Sơ đồ cấu trúc:**

* 📁 **Project_A**: `Source/app.js`, `Assets/logo.png`
* 📁 **Project_B**: `Data/users.csv`, `Backup/old.txt`

**Lệnh thực hiện:**

```bash
mkdir -p {Project_A/{Source,Assets},Project_B/{Data,Backup}} && touch {Project_A/Source/app.js,Project_A/Assets/logo.png,Project_B/Data/users.csv,Project_B/Backup/old.txt}
```
