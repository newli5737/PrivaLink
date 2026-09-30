# Cài đặt và Triển khai
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản tài liệu:** 1.0  
**Năm:** 2026  
**Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống

---

## Mục lục

1. [Tổng quan hệ thống](#tong-quan-he-thong)
2. [Yêu cầu môi trường](#yeu-cau-moi-truong)
3. [Lấy mã nguồn](#lay-ma-nguon)
4. [Cấu hình dự án](#cau-hinh-du-an)
5. [Cài đặt các gói phụ thuộc](#cai-dat-cac-goi-phu-thuoc)
6. [Cấu hình Server](#cau-hinh-server)
7. [Cấu hình Client](#cau-hinh-client)
8. [Khởi chạy hệ thống](#khoi-chay-he-thong)
9. [Kiểm tra hoạt động](#kiem-tra-hoat-dong)
10. [Khắc phục sự cố](#khac-phuc-su-co)
11. [Các lệnh hữu ích](#cac-lenh-huu-ich)
12. [Phụ lục](#phu-luc)

---

<a name="tong-quan-he-thong"></a>
## 1. Tổng quan hệ thống

**Local Messenger** là giải pháp phần mềm theo mô hình Client - Server chuyên dụng để trao đổi tin nhắn, gửi hình ảnh và dữ liệu an toàn trong phạm vi mạng cục bộ (LAN) của doanh nghiệp, cơ quan và các đơn vị tổ chức. Hệ thống hoạt động độc lập, tự chủ dữ liệu và không cần kết nối Internet công cộng.

### Kiến trúc:
```
┌─────────────────┐        ┌─────────────────┐
│   Ứng dụng      │        │   Ứng dụng      │
│   Client        │◄──────►│   Server        │
│   (PyQt5)       │ HTTP   │   (FastAPI)     │
│                 │WebSocket│                │
└─────────────────┘        └─────────────────┘
                                    │
                                    ▼
                            ┌─────────────────┐
                            │  Cơ sở dữ liệu  │
                            │   (SQLite)      │
                            └─────────────────┘
```

### Các tính năng cốt lõi:
- **Giao tiếp Real-time** qua WebSocket
- **Xác thực bảo mật** sử dụng JWT Token
- **Gửi hình ảnh** kèm xem trước trực quan
- **Lưu trữ dữ liệu cục bộ**, hoàn toàn không cần kết nối Internet bên ngoài
- **Đa nền tảng** (Windows, Linux, macOS)

---

<a name="yeu-cau-moi-truong"></a>
## 2. Yêu cầu môi trường

### 2.1. Yêu cầu tối thiểu

| Thành phần | Phía Client | Phía Server |
|---|---|---|
| **Hệ điều hành** | Windows 10/11, Linux Ubuntu 20.04+, macOS | Windows 10/11, Linux Ubuntu 20.04+, macOS |
| **CPU** | 1 nhân, 1 GHz | 1 nhân, 1 GHz |
| **RAM** | 256 MB | 512 MB |
| **Dung lượng đĩa trống** | 50 MB | 100 MB |
| **Phiên bản Python** | 3.8 trở lên | 3.8 trở lên |
| **Kết nối mạng** | Mạng LAN (Ethernet/Wi-Fi) | IP tĩnh trong mạng LAN |

### 2.2. Kiểm tra hệ thống hiện tại

**Kiểm tra Python:**
```bash
python --version
# Kết quả mong đợi: Python 3.8.x hoặc cao hơn
# Nếu chưa nhận lệnh python, thử:
python3 --version
```

**Kiểm tra dung lượng đĩa:**
```bash
# Windows:
dir

# Linux/Mac:
df -h .
```

### 2.3. Cài đặt phần mềm bổ sung

**Nếu máy tính chưa có Python:**

**Windows:**
1. Tải bản cài đặt Python từ [python.org](https://www.python.org/downloads/)
2. Khi cài đặt, **bắt buộc tích chọn "Add Python to PATH"**
3. Khởi động lại máy tính

**Linux (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv
```

**macOS:**
```bash
brew install python
```

---

<a name="lay-ma-nguon"></a>
## 3. Lấy mã nguồn

### 3.1. Cách 1: Clone từ kho Git (Khuyến nghị)

#### Cài đặt Git:
* **Windows:** Tải từ [git-scm.com](https://git-scm.com/download/win)  
* **Linux:** `sudo apt install git`  
* **macOS:** `brew install git`

#### Clone dự án:
```bash
# Mở terminal hoặc command prompt
# Chuyển vào thư mục lưu trữ dự án
cd ~/projects   # Trên Linux/Mac
# hoặc trên Windows: cd C:\Users\YourName\Projects

# Clone repository
git clone https://github.com/Leendeseqy/PKOvchinnikova_21IS_4semestr_Malinevskiy.git
cd PKOvchinnikova_21IS_4semestr_Malinevskiy

# Chuyển vào thư mục mã nguồn messenger
cd messenger
```

### 3.2. Cách 2: Tải file nén ZIP

1. Truy cập trang dự án trên GitHub
2. Nhấn vào nút **"Code"** $\rightarrow$ **"Download ZIP"**
3. Giải nén vào thư mục mong muốn
4. Mở terminal và chuyển vào thư mục dự án:
```bash
cd PKOvchinnikova_21IS_4semestr_Malinevskiy
cd messenger
```

### 3.3. Cấu trúc thư mục mã nguồn

Sau khi vào thư mục `messenger/`, bạn sẽ thấy cấu trúc như sau:

```
messenger/ 
├── requirements.txt              # Danh sách thư viện phụ thuộc
├── client/                       # Mã nguồn ứng dụng Client
│   ├── main.py                   # Điểm khởi chạy Client
│   ├── config.py                 # Cấu hình kết nối Server
│   ├── websocket_client.py       # Client kết nối WebSocket
│   ├── models/                   # Định nghĩa đối tượng Client
│   │   ├── message.py
│   │   └── user.py
│   └── ui/                       # Giao diện đồ họa (PyQt5)
│       ├── login_dialog.py       # Cửa sổ đăng nhập / đăng ký
│       ├── main_window.py        # Cửa sổ ứng dụng chính
│       └── chat_widget.py        # Widget khung chat
│   
├── server/                       # Mã nguồn ứng dụng Server
│   ├── main.py                   # Điểm khởi chạy Server (FastAPI)
│   ├── websocket_manager.py      # Quản lý các kết nối WebSocket
│   ├── dependencies.py           # Dependency injection & JWT auth
│   ├── database/                 # Tương tác cơ sở dữ liệu
│   │   ├── db.py                 # Khởi tạo kết nối DB
│   │   ├── user_model.py         # Model người dùng
│   │   ├── message_model.py      # Model tin nhắn
│   │   └── models.py
│   ├── routers/                  # Các router điều hướng API
│   │   ├── auth.py               # Xác thực tài khoản
│   │   ├── messages.py           # Xử lý tin nhắn
│   │   ├── users.py              # Quản lý người dùng
│   │   └── admin.py              # Chức năng quản trị
│   └── schemas/                  # Pydantic schemas xác thực dữ liệu
│       ├── user.py
│       └── message.py
```

> **Lưu ý:** Tất cả các lệnh thao tác tiếp theo đều được chạy từ thư mục `messenger/`.

---

<a name="cau-hinh-du-an"></a>
## 4. Cấu hình dự án

### 4.1. Tạo môi trường ảo (Khuyến nghị)

Môi trường ảo giúp cô lập các gói thư viện của dự án, tránh xung đột với hệ thống.

```bash
# Tại thư mục messenger/
python3 -m venv venv
```

**Kích hoạt môi trường ảo:**

* **Trên Windows (Command Prompt):**
```cmd
venv\Scripts\activate
```

* **Trên Windows (PowerShell):**
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
.\venv\Scripts\Activate.ps1
```

* **Trên Linux / macOS:**
```bash
source venv/bin/activate
```

**Kiểm tra kích hoạt:**  
Dòng lệnh sẽ xuất hiện tiền tố `(venv)`, ví dụ:
```
(venv) user@machine:~/messenger$
```

### 4.2. Thoát khỏi môi trường ảo

Khi hoàn thành công việc:
```bash
deactivate
```

---

<a name="cai-dat-cac-goi-phu-thuoc"></a>
## 5. Cài đặt các gói phụ thuộc

### 5.1. Cài đặt toàn bộ dependencies

Đảm bảo môi trường ảo đang được kích hoạt:

```bash
pip install -r requirements.txt
```

### 5.2. Kiểm tra cài đặt thành công

```bash
pip list
```

Các thư viện chính bao gồm:
* `fastapi` ($\ge 0.104.1$)
* `uvicorn` ($\ge 0.24.0$)
* `PyQt5` ($\ge 5.15.9$)
* `websockets` ($\ge 12.0$)
* `requests` ($\ge 2.31.0$)
* `sqlalchemy`, `pydantic`, `python-jose`, `passlib`, `bcrypt`

### 5.3. Xử lý lỗi cài đặt thường gặp

**Lỗi: `pip is not recognized`**
```bash
python -m pip install -r requirements.txt
```

**Lỗi khi cài PyQt5 trên Linux (Ubuntu/Debian):**
```bash
sudo apt-get update
sudo apt-get install python3-pyqt5
```

---

<a name="cau-hinh-server"></a>
## 6. Cấu hình Server

### 6.1. Xác định địa chỉ IP của máy chủ

Máy chủ nên có một địa chỉ IP cố định (Static IP) trong mạng nội bộ.

* **Trên Windows:**
```cmd
ipconfig
# Tìm dòng IPv4 Address (ví dụ: 192.168.1.100)
```

* **Trên Linux / macOS:**
```bash
ip addr show
# hoặc
ifconfig
```

### 6.2. Cấu hình mặc định của Server

Server được cấu hình mặc định:
- **Host:** `0.0.0.0` (Lắng nghe kết nối trên tất cả các card mạng)
- **Port:** `8000`
- **Cơ sở dữ liệu:** `messenger.db` (Tự động khởi tạo trong thư mục `server/`)

### 6.3. Khởi tạo thủ công cơ sở dữ liệu (tùy chọn)

Cơ sở dữ liệu sẽ tự động tạo ở lần chạy đầu tiên. Bạn cũng có thể khởi tạo trước bằng lệnh:
```bash
cd server
python3 -c "from database.db import init_db; init_db()"
cd ..
```

---

<a name="cau-hinh-client"></a>
## 7. Cấu hình Client

### 7.1. Cấu hình kết nối tới Server

**Bước quan trọng:** Trước khi chạy Client, bạn cần trỏ địa chỉ kết nối về IP của máy chủ.

Mở file `client/config.py` và chỉnh sửa:
```python
# client/config.py

# Thay đổi IP này thành địa chỉ IP thực tế của máy Server trong mạng LAN
SERVER_HOST = "192.168.1.100"  # ← Điền IP của Server tại đây
SERVER_PORT = 8000
SERVER_URL = f"http://{SERVER_HOST}:{SERVER_PORT}"
```

*(Lưu ý: Nếu phiên bản có tính năng UDP Broadcast Discovery, Client có thể tự động dò quét server trong cùng dải mạng LAN).*

### 7.2. Kiểm tra kết nối mạng từ Client đến Server

Trước khi khởi chạy Client:
```bash
# Kiểm tra ping đến server
ping 192.168.1.100

# Kiểm tra cổng 8000 có thông hay không
# Trên Linux/Mac:
nc -zv 192.168.1.100 8000

# Trên Windows PowerShell:
Test-NetConnection 192.168.1.100 -Port 8000
```

---

<a name="khoi-chay-he-thong"></a>
## 8. Khởi chạy hệ thống

### 8.1. Thứ tự khởi chạy bắt buộc

1. **Khởi chạy Server trước** (Server cần duy trì hoạt động liên tục).
2. **Khởi chạy các Client sau** (Các máy người dùng bật/tắt tự do).

### 8.2. Khởi chạy Server

**Cách 1: Khởi chạy trực tiếp bằng Python:**
```bash
cd server
python3 main.py
```

**Cách 2: Khởi chạy bằng Uvicorn (Khuyến nghị khi phát triển):**
```bash
cd server
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```

**Thông báo khi Server sẵn sàng:**
```
INFO:     Started server process [1234]
INFO:     Waiting for application startup.
INFO:     Application startup complete.
INFO:     Uvicorn running on http://0.0.0.0:8000 (Press CTRL+C to quit)
```

### 8.3. Khởi chạy Client

Mở một cửa sổ terminal mới:
```bash
cd client
python3 main.py
```

* Cửa sổ đăng nhập/đăng ký sẽ xuất hiện.
* Tiến hành đăng ký tài khoản mới hoặc đăng nhập tài khoản có sẵn.
* Sau khi đăng nhập thành công, giao diện chính của Local Messenger sẽ hiển thị.

---

<a name="kiem-tra-hoat-dong"></a>
## 9. Kiểm tra hoạt động

### 9.1. Kiểm tra Server qua trình duyệt
Mở trình duyệt trên bất kỳ máy nào trong mạng LAN và truy cập:
`http://<IP_SERVER>:8000/docs`

Giao diện **FastAPI Swagger UI** tự động sẽ hiển thị đầy đủ danh sách các API endpoints.

### 9.2. Kịch bản kiểm thử quy trình thực tế

| Bước | Hành động | Kết quả mong đợi |
|---|---|---|
| 1 | Bật Server | Hiển thị log `Uvicorn running on http://0.0.0.0:8000` |
| 2 | Mở Client 1 | Cửa sổ đăng nhập hiển thị |
| 3 | Đăng ký tài khoản `User1` | Báo "Registration successful" |
| 4 | Đăng nhập với `User1` | Vào màn hình chat chính |
| 5 | Mở Client 2 (máy khác hoặc cửa sổ mới) | Cửa sổ đăng nhập hiển thị |
| 6 | Đăng ký và đăng nhập `User2` | Vào màn hình chat chính |
| 7 | `User1` chọn `User2` trong danh bạ | Mở khung trò chuyện riêng |
| 8 | `User1` gửi tin nhắn "Xin chào!" | Tin nhắn lập tức xuất hiện ở màn hình của cả 2 phía qua WebSocket |
| 9 | `User2` phản hồi lại | Tin nhắn hiển thị tức thời cho cả 2 người dùng |
| 10 | Gửi file ảnh (nút [Đính kèm]) | Ảnh hiển thị kèm thumbnail xem trước |

---

<a name="khac-phuc-su-co"></a>
## 10. Khắc phục sự cố

#### Sự cố 1: Lỗi cổng bị chiếm dụng (`Address already in use`)
* **Nguyên nhân:** Cổng 8000 đang được tiến trình khác sử dụng.
* **Xử lý:**
  * Windows: `netstat -ano | findstr :8000` sau đó tắt PID tương ứng: `taskkill /PID <PID> /F`
  * Linux/Mac: `lsof -i :8000` sau đó tắt: `kill -9 <PID>`

#### Sự cố 2: Client báo lỗi `Cannot connect to server`
* **Xử lý:**
  1. Kiểm tra lại địa chỉ IP trong `client/config.py`.
  2. Đảm bảo Server đang bật.
  3. Kiểm tra tường lửa (Firewall): Cần mở cổng 8000 (TCP) trên máy chủ Server.

#### Sự cố 3: Không thấy danh sách người dùng khác
* **Xử lý:** Đợi 5-10 giây để cơ chế polling/WebSocket cập nhật trạng thái người dùng online, hoặc kiểm tra xem tài khoản khác đã đăng nhập chưa.

---

<a name="cac-lenh-huu-ich"></a>
## 11. Các lệnh hữu ích

```bash
# Kiểm tra log server chạy ngầm trên Linux
tail -f server.log

# Kiểm tra cơ sở dữ liệu SQLite
sqlite3 messenger.db ".tables"
sqlite3 messenger.db "SELECT id, username FROM users;"
```

---

<a name="phu-luc"></a>
## 12. Phụ lục

### Mở cổng tường lửa trên máy chủ Server:
* **Trên Windows:** Mở *Windows Defender Firewall* $\rightarrow$ *Inbound Rules* $\rightarrow$ Thêm Rule mới cho cổng TCP 8000 $\rightarrow$ Allow Connection.
* **Trên Linux (Ubuntu ufw):**
```bash
sudo ufw allow 8000/tcp
sudo ufw reload
```

---

*Tài liệu hướng dẫn triển khai ứng dụng Local Messenger phiên bản 1.0 - Năm 2026*
