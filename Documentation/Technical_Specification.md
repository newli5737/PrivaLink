# Đặc tả yêu cầu kỹ thuật (Technical Specification - SRS)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản tài liệu:** 1.0 (Bản hiện thực thực tế)  
**Năm:** 2026  
**Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống  
**Trạng thái:** Tài liệu đặc tả kỹ thuật chuẩn mực (Đã hoàn thiện & Sẵn sàng bàn giao)

---

## 1. Thông tin chung

### 1.1. Tên hệ thống
* **Tên đầy đủ:** Local Messenger - Hệ thống trao đổi thông tin và nhắn tin nội bộ bảo mật  
* **Tên viết tắt:** LMessenger  
* **Mã dự án:** SecureLAN-Messenger

### 1.2. Căn cứ phát triển
Dự án phát triển giải pháp phần mềm "Local Messenger" được xây dựng nhằm cung cấp hệ thống giao tiếp, trao đổi dữ liệu và chia sẻ tệp tin tức thời, an toàn tuyệt đối trong mạng cục bộ (LAN) của doanh nghiệp, cơ quan và tổ chức.

### 1.3. Mục tiêu kỹ thuật
Xây dựng giải pháp phần mềm hoàn chỉnh, hoạt động ổn định và tin cậy trong mạng nội bộ, đáp ứng các tiêu chuẩn kỹ thuật:
- Kiến trúc phần mềm Client - Server phân tầng rõ rệt, dễ bảo trì và mở rộng.
- Xây dựng RESTful API tốc độ cao với FastAPI (Python).
- Thiết kế giao diện máy trạm đồ họa đa nền tảng hiện đại với PyQt5.
- Kênh truyền thông hai chiều thời gian thực qua giao thức WebSocket với độ trễ dưới 100ms.
- Quản lý định danh và bảo mật bằng JSON Web Token (JWT) và thuật toán băm mật khẩu bcrypt.
- Tự động nhận diện máy chủ trong mạng LAN qua giao thức UDP Broadcast.

---

## 2. Kiến trúc giải pháp kỹ thuật

### 2.1. Sơ đồ kiến trúc tổng thể
```
┌─────────────────────────────────────────────────────────┐
│                    Mạng LAN trường học                  │
├─────────────────────────────────────────────────────────┤
│                                                         │
│  ┌──────────────┐                 ┌──────────────────┐ │
│  │   Client 1   │◄──HTTP/WS──────►│      Server      │ │
│  │  (PyQt5)     │                 │    (FastAPI)     │ │
│  └──────────────┘                 │  ┌────────────┐  │ │
│                                   │  │ SQLite CSDL│  │ │
│  ┌──────────────┐                 │  └────────────┘  │ │
│  │   Client 2   │◄──HTTP/WS──────►│  ┌────────────┐  │ │
│  │  (PyQt5)     │                 │  │ WebSocket  │  │ │
│  └──────────────┘                 │  │  Manager   │  │ │
│                                   │  └────────────┘  │ │
│                                   └──────────────────┘ │
└─────────────────────────────────────────────────────────┘
```

### 2.2. Kiến trúc thành phần chi tiết

#### Ứng dụng Client (PyQt5):
* **Tầng UI:**
  * `MainWindow`: Cửa sổ làm việc chính, thanh công cụ, danh sách liên hệ.
  * `ChatWidget`: Khung trò chuyện, dòng nhập văn bản, nút đính kèm ảnh [Đính kèm], nút gửi.
  * `LoginDialog`: Hộp thoại đăng nhập và đăng ký tài khoản.
* **Tầng Logic nghiệp vụ:**
  * `Message`: Mô hình đối tượng tin nhắn.
  * `User`: Mô hình người dùng.
* **Tầng Mạng & Kết nối:**
  * Client HTTP (`requests`): Giao tiếp API đồng bộ.
  * Client WebSocket (`websockets`): Kênh lắng nghe sự kiện đẩy thời gian thực.
  * Timer cập nhật (`QTimer`): Quét trạng thái người dùng định kỳ.

#### Ứng dụng Server (FastAPI):
* **Tầng định tuyến API (Routers):**
  * `/auth`: Xác thực, cấp phát token JWT.
  * `/messages`: Gửi, nhận, xóa tin nhắn.
  * `/users`: Danh sách người dùng, cập nhật trạng thái trực tuyến.
  * `/admin`: Quyền quản trị viên truy vấn toàn bộ dữ liệu.
  * `/ws`: Điểm kết nối socket hai chiều.
* **Tầng xử lý dữ liệu & ORM:**
  * `db.py`: Kết nối và tạo bảng CSDL.
  * `user_model.py`, `message_model.py`: Xử lý truy vấn cơ sở dữ liệu.
* **Tầng kiểm thực dữ liệu (Schemas):**
  * Pydantic schemas đảm bảo dữ liệu đầu vào luôn chuẩn xác.

---

## 3. Stack công nghệ thực tế và phiên bản

| Thành phần | Công nghệ | Phiên bản | Mục đích sử dụng |
|---|---|---|---|
| **Ngôn ngữ chính** | Python | 3.8+ | Toàn bộ Server và Client |
| **Backend Framework** | FastAPI | $\ge 0.104.0$ | Xây dựng REST API và WebSocket Endpoint |
| **ASGI Server** | Uvicorn | $\ge 0.24.0$ | Chạy dịch vụ ứng dụng web bất đồng bộ |
| **Cơ sở dữ liệu** | SQLite | $\ge 3.35$ | Lưu trữ dữ liệu file cục bộ, không cần cấu hình phức tạp |
| **Mã hóa Token** | PyJWT / python-jose | $\ge 3.3.0$ | Cấp phát chữ ký JWT an toàn |
| **Băm mật khẩu** | passlib (bcrypt) | $\ge 1.7.4$ | Băm mật khẩu người dùng trước khi lưu DB |
| **Giao diện Client** | PyQt5 | $\ge 5.15.0$ | Bộ công cụ dựng giao diện desktop native |
| **HTTP Client** | Requests | $\ge 2.31.0$ | Gửi REST request |
| **Truyền thông Real-time**| WebSockets | $\ge 12.0$ | Giao thức socket truyền tải tin nhắn tức thời |

---

## 4. Yêu cầu phần cứng và hạ tầng mạng

### 4.1. Cấu hình máy chủ (Server)
* **CPU:** 1 nhân, xung nhịp từ 1.0 GHz trở lên.
* **RAM:** Tối thiểu 512 MB.
* **Dung lượng ổ cứng trống:** Tối thiểu 100 MB.
* **Hệ điều hành:** Windows 10/11 hoặc Linux (Ubuntu 20.04+).
* **Mạng:** Kết nối mạng LAN, cấu hình địa chỉ IP tĩnh.

### 4.2. Cấu hình máy trạm người dùng (Client)
* **CPU:** 1 nhân, 1.0 GHz.
* **RAM:** Tối thiểu 256 MB.
* **Dung lượng ổ cứng trống:** Tối thiểu 50 MB.
* **Độ phân giải màn hình:** Tối thiểu 1024x768.
* **Mạng:** Kết nối cùng dải mạng LAN với Server.

---

## 5. Đặc tả giao tiếp API và WebSocket

### 5.1. Định dạng REST API chính
* Địa chỉ gốc: `http://{server_ip}:8000`

#### Endpoint xác thực tài khoản:
```http
POST /auth/register
Content-Type: application/json

{
  "username": "sinhvienA",
  "password": "mat_khau_an_toan"
}
```

```http
POST /auth/login
Content-Type: application/json

{
  "username": "sinhvienA",
  "password": "mat_khau_an_toan"
}
--> Phản hồi: {"access_token": "eyJhbGciOi...", "token_type": "bearer"}
```

#### Endpoint tin nhắn:
* `GET /messages?contact_id={id}`: Tải lịch sử trao đổi với người dùng có ID tương ứng.
* `POST /messages`: Gửi tin nhắn mới:
```json
{
  "content": "Chào bạn, gửi tài liệu giúp mình nhé!",
  "receiver_id": 2,
  "message_type": "text",
  "file_data": null
}
```
* `DELETE /messages/{message_id}`: Xóa tin nhắn cá nhân do chính mình gửi.

### 5.2. Giao thức WebSocket
* Điểm kết nối: `ws://{server_ip}:8000/ws/{user_id}`
* Gói tin nhận tin nhắn mới:
```json
{
  "type": "new_message",
  "message": {
    "id": 105,
    "sender_id": 1,
    "receiver_id": 2,
    "content": "Xin chào!",
    "timestamp": "2026-01-19T10:30:00",
    "message_type": "text"
  }
}
```
* Gói tin đồng bộ xóa tin nhắn:
```json
{
  "type": "message_deleted",
  "message_id": 105,
  "deleted_by": 1
}
```

---

## 6. Yêu cầu về an toàn và bảo mật

1. **Kiểm soát truy cập:** Mọi API thao tác dữ liệu đều yêu cầu Bearer JWT Token hợp lệ trong HTTP Header.
2. **Mật khẩu người dùng:** Tuyệt đối không lưu dạng văn bản thô (plain-text); sử dụng giải thuật bcrypt kèm chuỗi salt ngẫu nhiên.
3. **Phòng chống tấn công:**
   * SQL Injection: Sử dụng triệt để ORM và truy vấn tham số hóa (Parameterized queries).
   * XSS: Tầng giao diện PyQt5 hiển thị nội dung dạng text an toàn, không thực thi mã script.
   * Cách ly mạng: Hệ thống chạy hoàn toàn trong phạm vi mạng LAN nội bộ.

---

## 7. Chỉ số hiệu năng và tải trọng

* Thời gian phản hồi gửi/nhận tin nhắn qua mạng LAN: $\le 100$ ms.
* Thời gian tải lịch sử 100 tin nhắn gần nhất: $\le 300$ ms.
* Dung lượng ảnh tối đa cho phép gửi đính kèm: 5 - 10 MB (chuyển đổi base64).
* Số lượng kết nối đồng thời thiết kế trong mạng LAN: 10 - 50 máy trạm hoạt động ổn định.

---

## 8. Tiêu chuẩn nghiệm thu dự án

- [x] Đầy đủ tài liệu đặc tả, kiến trúc, hướng dẫn triển khai.
- [x] Khởi chạy máy chủ Server và kết nối thành công từ 2 Client độc lập.
- [x] Thực hiện đầy đủ quy trình: Đăng ký $\rightarrow$ Đăng nhập $\rightarrow$ Gửi/nhận tin nhắn tức thời $\rightarrow$ Gửi ảnh $\rightarrow$ Xóa tin nhắn.
- [x] Mã nguồn tổ chức khoa học, phân lớp rõ ràng, tuân thủ tiêu chuẩn PEP8.

---

*Ban Dự án & Kỹ sư Thiết kế Hệ thống - Local Messenger (19/01/2026)*