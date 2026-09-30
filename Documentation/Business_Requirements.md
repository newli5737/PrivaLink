# Yêu cầu nghiệp vụ (Business Requirements Document - BRD)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản tài liệu:** 1.1 (Bản cập nhật mới nhất)  
**Năm:** 2026  
**Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống  
**Trạng thái:** Hoàn thiện và sẵn sàng triển khai thực tế

---

## 1. Tổng quan dự án

* **Tên dự án:** Local Messenger (Ứng dụng nhắn tin nội bộ)
* **Loại hình dự án:** Giải pháp phần mềm truyền thông nội bộ theo mô hình Client - Server
* **Phiên bản hiện tại:** 1.1

### Mô tả tóm tắt
Local Messenger là giải pháp phần mềm được thiết kế và xây dựng nhằm phục vụ nhu cầu trao đổi thông tin, gửi tin nhắn, chia sẻ hình ảnh và dữ liệu an toàn trong phạm vi mạng cục bộ (LAN) của doanh nghiệp, cơ quan và các đơn vị tổ chức, không phụ thuộc vào kết nối Internet bên ngoài.

**Các tính năng nổi bật trong phiên bản 1.1:**
- **Tự động dò tìm máy chủ (Dynamic Server Discovery)** qua giao thức UDP Broadcast.
- **Khởi tạo và quản lý máy chủ** trực tiếp từ giao diện Client.
- **Bảo vệ máy chủ bằng mật khẩu** (chỉ người có mật khẩu mới có quyền kích hoạt server).
- **Hỗ trợ giao diện Dark Mode** và khả năng tùy biến màu sắc giao diện theo theme JSON.
- **Hệ thống thông báo đẩy (Desktop Notifications)** kèm âm thanh đa dạng.
- **Quản lý danh sách nhiều máy chủ** linh hoạt.

---

## 2. Mục tiêu và nhiệm vụ của dự án

### 2.1. Mục tiêu chiến lược của giải pháp
1. **Làm chủ toàn bộ stack công nghệ:** FastAPI + PyQt5 + SQLite + WebSocket + UDP Networking.
2. **Hiện thực hóa kiến trúc Client - Server chuẩn mực.**
3. **Triển khai giao thức tự dò tìm dịch vụ mạng** (UDP broadcast discovery).
4. **Xây dựng hệ thống thông báo đa nền tảng** và cá nhân hóa trải nghiệm người dùng.
5. **Thiết kế hệ thống đa người dùng** có phân quyền và bảo mật mật khẩu.

### 2.2. Nhiệm vụ cụ thể đã hoàn thành (Phiên bản 1.1)

#### Hệ thống dò tìm máy chủ (Tính năng mới):
- Sử dụng **UDP Broadcast** để tự động quét tìm các server đang chạy trong cùng mạng LAN.
- Hiển thị trạng thái máy chủ (Online / Offline).
- Cung cấp thông tin chi tiết của server: tên, mô tả, số lượng người dùng đang kết nối, cổng dịch vụ.
- Biểu tượng cảnh báo trực quan máy chủ có mật khẩu ([Bảo mật]).
- Hai chế độ quét mạng: Quét nhanh (Quick scan - 1.5s) và Quét toàn diện (Full scan - 3s).

#### Quản lý máy chủ từ phía Client:
- Tạo mới cấu hình máy chủ ngay trên hộp thoại giao diện người dùng.
- Bật / tắt tiến trình server trực tiếp từ Client.
- Tùy chọn tự động khởi chạy server (Auto-start) khi mở Client.
- Lưu trữ cấu hình danh sách server dưới dạng file JSON.

#### Bảo mật máy chủ bằng mật khẩu:
- Thiết lập mật khẩu quản trị khi tạo server.
- Băm mật khẩu an toàn bằng giải thuật SHA-256 kết hợp chuỗi ngẫu nhiên (Salt).
- Yêu cầu nhập mật khẩu xác thực khi ra lệnh khởi chạy server.

#### Hệ thống thông báo và giao diện:
- Thông báo góc màn hình (Desktop Notification) khi có tin nhắn mới.
- Âm thanh thông báo sự kiện (tin nhắn đến, kết nối, ngắt kết nối).
- Thu nhỏ ứng dụng xuống khay hệ thống (System Tray) với menu tiện ích.
- Bộ 4 chủ đề giao diện có sẵn: Sáng (Light), Tối (Dark), Xanh dương (Blue), Đêm khuya (Midnight), cùng khả năng nạp thêm theme tùy biến qua JSON.

---

## 3. Kiến trúc và tương tác giữa các thành phần

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT (PyQt5)                          │
├─────────────────────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │
│  │   UI Layer   │  │   Managers   │  │ Network Layer│           │
│  │• MainWindow  │  │• AuthManager │  │• WebSocket   │           │
│  │• LoginDialog │  │• ServerMgr   │  │• Broadcast   │           │
│  │• ChatWidget  │  │• ThemeMgr    │  │  Client      │           │
│  │• SettingsDlg │  │• Notification│  │              │           │
│  └──────────────┘  └──────────────┘  └──────────────┘           │
└─────────────────────────────────────────────────────────────────┘
                               │
                    ┌──────────┴──────────┐
                    │                     │
               HTTP / WS             UDP Broadcast
                    │                     │
                    ▼                     ▼
┌─────────────────────────────────────────────────────────────────┐
│                         SERVER (FastAPI)                        │
├─────────────────────────────────────────────────────────────────┤
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │
│  │  API Routers │  │  WebSocket   │  │  Broadcast   │           │
│  │ (Auth/Msg/..)│  │   Manager    │  │    Server    │           │
│  └──────────────┘  └──────────────┘  └──────────────┘           │
│         │                                                       │
│         ▼                                                       │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │
│  │   Database   │  │ Server Auth  │  │ Server Config│           │
│  │ (SQLAlchemy) │  │  (Security)  │  │  (JSON cfg)  │           │
│  └──────────────┘  └──────────────┘  └──────────────┘           │
└─────────────────────────────────────────────────────────────────┘
```

---

## 4. Bảng tính năng và phạm vi hệ thống

### 4.1. Bảng tính năng đã hoàn thiện trong phiên bản 1.1

| Nhóm tính năng | Chi tiết tính năng | Trạng thái |
|---|---|:---:|
| **Dò tìm Server** | Quét UDP broadcast trong mạng LAN | Hoàn thành |
| | Hiển thị trạng thái Online/Offline, số người kết nối | Hoàn thành |
| | Nhận diện biểu tượng máy chủ bảo vệ mật khẩu ([Bảo mật]) | Hoàn thành |
| **Quản lý Server** | Tạo, cấu hình, lưu trữ cấu hình Server | Hoàn thành |
| | Khởi chạy và dừng tiến trình server từ Client | Hoàn thành |
| | Tự động khởi chạy server (Auto-start) | Hoàn thành |
| **Bảo mật Server** | Đặt mật khẩu kích hoạt, băm SHA-256 + Salt | Hoàn thành |
| **Xác thực User** | Đăng ký, đăng nhập tài khoản người dùng, JWT Token | Hoàn thành |
| | Tài khoản tạo đầu tiên tự động nhận quyền Admin | Hoàn thành |
| **Nhắn tin** | Chat trực tiếp 1-1 theo thời gian thực (WebSocket) | Hoàn thành |
| | Gửi và hiển thị hình ảnh (JPG, PNG, GIF, BMP) qua Base64 | Hoàn thành |
| | Lưu trữ và tải lại toàn bộ lịch sử tin nhắn | Hoàn thành |
| | Xóa tin nhắn cá nhân (đồng bộ xóa tức thời qua WebSocket) | Hoàn thành |
| **Giao diện & Tiện ích** | Đổi chủ đề sáng / tối, lưu cấu hình người dùng | Hoàn thành |
| | Thông báo Desktop Notification và âm thanh | Hoàn thành |
| | Thu nhỏ xuống System Tray | Hoàn thành |

### 4.2. Các giới hạn thực tế của phiên bản hiện tại (Hệ thống CHƯA làm):
1. **Chưa hỗ trợ chat nhóm:** Phiên bản 1.1 tập trung chat cá nhân 1-1.
2. **Chưa mã hóa đầu cuối tin nhắn (End-to-End Encryption):** Mới áp dụng mã hóa bảo mật tầng vận chuyển và mã hóa mật khẩu JWT/bcrypt.
3. **Không đồng bộ đám mây:** Toàn bộ dữ liệu nằm cục bộ tại máy chủ LAN.
4. **Chưa có client di động:** Ứng dụng hiện phát triển cho desktop (Windows, Linux, macOS).
5. **Chưa có cuộc gọi thoại / video call.**

---

## 5. Đặc tính kỹ thuật & Stack công nghệ

| Thành phần | Công nghệ | Phiên bản | Mục đích |
|---|---|---|---|
| **Backend API** | FastAPI | 0.104.1 | Xây dựng REST API tốc độ cao, hỗ trợ bất đồng bộ |
| **ASGI Server** | Uvicorn | 0.24.0 | Máy chủ web chạy FastAPI |
| **Real-time** | WebSockets | 12.0 | Kênh truyền thông 2 chiều độ trễ thấp |
| **Xác thực** | Python-JOSE / Passlib | 3.3.0 / 1.7.4 | Sinh và xác thực JWT token, băm mật khẩu bcrypt |
| **Cơ sở dữ liệu** | SQLite / SQLAlchemy | 3.x / 2.0.23 | Lưu trữ dữ liệu người dùng, tin nhắn |
| **Frontend GUI** | PyQt5 | 5.15.10 | Xây dựng giao diện Desktop trực quan |
| **HTTP Client** | Requests | 2.31.0 | Gửi request REST API từ Client lên Server |
| **Thông báo & Âm thanh** | Plyer / Pygame | 2.1.0 / 2.5.2 | Đẩy notification ra màn hình máy tính và phát âm thanh |
| **Xử lý đồ họa** | Pillow | 10.1.0 | Xử lý nén và định dạng hình ảnh đính kèm |

---

## 6. Phân tích rủi ro và phương án ứng phó

| Rủi ro | Mức độ | Khả năng xảy ra | Biện pháp ứng phó |
|---|:---:|:---:|---|
| **Mất mát cơ sở dữ liệu** | Cao | Trung bình | Cơ chế sao lưu thủ công/tự động file `messenger.db` định kỳ |
| **Nghẽn mạng LAN / Mất gói tin** | Trung bình | Trung bình | Cơ chế Ping/Pong kiểm tra kết nối WebSocket, tự động kết nối lại |
| **Xung đột cổng mạng (Port Conflict)** | Trung bình | Thấp | Kiểm tra trạng thái cổng trước khi bind, cho phép đổi port linh hoạt |
| **Lộ mật khẩu người dùng** | Cao | Thấp | Sử dụng thuật toán băm bcrypt an toàn kèm Salt, tuyệt đối không lưu plain-text |
| **Khó khăn khi cài đặt môi trường** | Trung bình | Cao | Viết tài liệu hướng dẫn từng bước chi tiết, cung cấp file script chạy tự động |

---

## 7. Kết luận

Tài liệu yêu cầu nghiệp vụ phiên bản 1.1 phản ánh chính xác 100% các tính năng và năng lực của giải pháp Local Messenger đã được phát triển và kiểm thử thực tế. Hệ thống đáp ứng toàn diện các tiêu chí về an toàn thông tin, bảo mật mạng nội bộ và tính năng truyền thông thời gian thực, sẵn sàng bàn giao và đưa vào triển khai chính thức cho khách hàng.

*Bộ phận chịu trách nhiệm: Ban Dự án & Kỹ sư Thiết kế Hệ thống - Ngày phát hành: 19/01/2026*