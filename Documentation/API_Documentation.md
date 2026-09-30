# Tài liệu đặc tả API (API Documentation)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản tài liệu:** 1.0  
**Năm:** 2026  
**Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống  
**Địa chỉ Base URL:** `http://localhost:8000` hoặc `http://<server_ip>:8000`

---

## Mục lục

1. [Giới thiệu tổng quan](#gioi-thieu)
2. [Các quy ước cơ bản](#quy-uoc-co-ban)
3. [Cơ chế xác thực (Authentication)](#co-che-xac-thuc)
4. [Nhóm Endpoints: Xác thực & Tài khoản](#endpoints-auth)
5. [Nhóm Endpoints: Quản lý Người dùng](#endpoints-users)
6. [Nhóm Endpoints: Tin nhắn & Hội thoại](#endpoints-messages)
7. [Nhóm Endpoints: Quản trị hệ thống (Admin)](#endpoints-admin)
8. [Giao thức WebSocket thời gian thực](#websocket)
9. [Cấu trúc mô hình dữ liệu (Data Schemas)](#mo-hinh-du-lieu)
10. [Bảng mã lỗi chuẩn HTTP](#ma-loi)
11. [Code mẫu gọi API (Python, cURL, JavaScript)](#code-mau)

---

<a name="gioi-thieu"></a>
## 1. Giới thiệu tổng quan

Tài liệu này đặc tả chi tiết toàn bộ hệ thống REST API và kênh WebSocket hai chiều của ứng dụng "Local Messenger". Hệ sinh thái API hỗ trợ:
- Đăng ký, đăng nhập và cấp phát phiên làm việc qua JWT.
- Trao đổi tin nhắn văn bản và hình ảnh đa phương tiện.
- Cập nhật danh bạ và trạng thái trực tuyến của người dùng.
- Quản trị và giám sát hệ thống mạng cục bộ.

### Stack công nghệ API:
- **Framework:** FastAPI 0.104+
- **Định dạng dữ liệu:** JSON (UTF-8, `Content-Type: application/json`)
- **Tài liệu tự động hóa:** Swagger UI tại `/docs` và ReDoc tại `/redoc`.
- **WebSocket:** RFC 6455 hỗ trợ kết nối hai chiều với cơ chế Ping/Pong.

---

<a name="quy-uoc-co-ban"></a>
## 2. Các quy ước cơ bản

### Header bắt buộc cho các API bảo mật:
```http
Authorization: Bearer <access_token>
Content-Type: application/json
```

### Định dạng phản hồi chuẩn:
```json
{
  "success": true,
  "data": { ... },
  "message": "Thao tác thực hiện thành công"
}
```

---

<a name="co-che-xac-thuc"></a>
## 3. Cơ chế xác thực (Authentication)

Hệ thống sử dụng cơ chế xác thực **JSON Web Token (JWT)** không lưu trạng thái (Stateless):
1. Client gửi Username và Password tới `/auth/login`.
2. Server kiểm tra tính hợp lệ và trả về Access Token.
3. Client đính kèm chuỗi Bearer Token này vào Header của mọi request tiếp theo.
4. Thời hạn hiệu lực của token: **24 giờ**.

---

<a name="endpoints-auth"></a>
## 4. Nhóm Endpoints: Xác thực & Tài khoản

### 4.1. Đăng ký tài khoản
* **Endpoint:** `POST /auth/register`
* **Mô tả:** Tạo tài khoản mới trong hệ thống. Tài khoản đăng ký đầu tiên sẽ tự động có cờ `is_admin = True`.
* **Request Body:**
```json
{
  "username": "sinhvien_a",
  "password": "mat_khau_bao_mat"
}
```
* **Response (200 OK):**
```json
{
  "id": 1,
  "username": "sinhvien_a",
  "is_admin": true,
  "message": "Registration successful"
}
```
* **Mã lỗi thường gặp:**
  * `400 Bad Request`: Username đã tồn tại.

---

### 4.2. Đăng nhập
* **Endpoint:** `POST /auth/login`
* **Mô tả:** Xác thực người dùng và nhận JWT Token.
* **Request Body:**
```json
{
  "username": "sinhvien_a",
  "password": "mat_khau_bao_mat"
}
```
* **Response (200 OK):**
```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "token_type": "bearer",
  "user_id": 1,
  "username": "sinhvien_a",
  "is_admin": true
}
```
* **Mã lỗi:**
  * `401 Unauthorized`: Sai tên đăng nhập hoặc mật khẩu.

---

<a name="endpoints-users"></a>
## 5. Nhóm Endpoints: Quản lý Người dùng

### 5.1. Lấy danh sách toàn bộ người dùng
* **Endpoint:** `GET /users`
* **Yêu cầu:** Token xác thực Bearer.
* **Response (200 OK):**
```json
[
  {
    "id": 1,
    "username": "sinhvien_a",
    "is_online": true,
    "status": "online",
    "is_admin": true
  },
  {
    "id": 2,
    "username": "sinhvien_b",
    "is_online": false,
    "status": "offline",
    "is_admin": false
  }
]
```

### 5.2. Lấy thông tin tài khoản hiện tại
* **Endpoint:** `GET /users/me`
* **Response (200 OK):** Thông tin chi tiết của người dùng gắn với token.

---

<a name="endpoints-messages"></a>
## 6. Nhóm Endpoints: Tin nhắn & Hội thoại

### 6.1. Gửi tin nhắn mới
* **Endpoint:** `POST /messages`
* **Request Body (Tin nhắn văn bản):**
```json
{
  "receiver_id": 2,
  "content": "Chào bạn, hôm nay có học thực hành không?",
  "message_type": "text",
  "file_data": null
}
```
* **Request Body (Tin nhắn gửi hình ảnh Base64):**
```json
{
  "receiver_id": 2,
  "content": "anh_chup_man_hinh.png",
  "message_type": "image",
  "file_data": "iVBORw0KGgoAAAANSUhEUgAA..."
}
```
* **Response (200 OK):**
```json
{
  "id": 101,
  "sender_id": 1,
  "receiver_id": 2,
  "content": "Chào bạn, hôm nay có học thực hành không?",
  "message_type": "text",
  "timestamp": "2026-01-19T10:30:00",
  "is_read": false
}
```

### 6.2. Lấy lịch sử tin nhắn
* **Endpoint:** `GET /messages?contact_id=2&limit=100`
* **Mô tả:** Lấy danh sách tối đa 100 tin nhắn qua lại giữa tài khoản hiện tại và người dùng có `contact_id`.
* **Response (200 OK):** Mảng các đối tượng tin nhắn sắp xếp theo thứ tự thời gian.

### 6.3. Xóa tin nhắn cá nhân
* **Endpoint:** `DELETE /messages/{message_id}`
* **Mô tả:** Xóa một tin nhắn. Người dùng chỉ có quyền xóa tin nhắn do chính mình gửi (`sender_id == current_user.id`).
* **Response (200 OK):**
```json
{
  "status": "success",
  "message": "Message deleted successfully"
}
```
* **Mã lỗi:**
  * `403 Forbidden`: Cố gắng xóa tin nhắn của người khác.
  * `404 Not Found`: Không tìm thấy mã tin nhắn.

---

<a name="endpoints-admin"></a>
## 7. Nhóm Endpoints: Quản trị hệ thống (Admin)

Chỉ có hiệu lực khi tài khoản mang cờ `is_admin = True`.

* `GET /admin/all-messages`: Trả về toàn bộ dữ liệu tin nhắn trong CSDL.
* `GET /admin/all-users`: Trả về danh sách chi tiết toàn bộ người dùng và thời gian hoạt động.

---

<a name="websocket"></a>
## 8. Giao thức WebSocket thời gian thực

* **URL kết nối:** `ws://<server_ip>:8000/ws/{user_id}`
* **Cơ chế hoạt động:** Sau khi đăng nhập, Client mở luồng kết nối WebSocket bền vững tới server. Server duy trì danh bạ kết nối `ActiveConnections`.

### Các sự kiện truyền phát:
1. **Sự kiện có tin nhắn mới (`new_message`):**
```json
{
  "type": "new_message",
  "message": {
    "id": 102,
    "sender_id": 2,
    "receiver_id": 1,
    "content": "Mình có đi học nhé!",
    "timestamp": "2026-01-19T10:31:00",
    "message_type": "text"
  }
}
```
2. **Sự kiện xóa tin nhắn (`message_deleted`):**
```json
{
  "type": "message_deleted",
  "message_id": 102,
  "deleted_by": 2
}
```
3. **Cơ chế giữ nhịp (Ping/Pong):**
   * Client gửi: `"ping"`
   * Server đáp: `"pong"`

---

<a name="mo-hinh-du-lieu"></a>
## 9. Cấu trúc mô hình dữ liệu (Pydantic Schemas)

```python
# User Schemas
class UserCreate(BaseModel):
    username: str
    password: str

class UserResponse(BaseModel):
    id: int
    username: str
    is_online: bool
    status: str
    is_admin: bool

# Message Schemas
class MessageCreate(BaseModel):
    receiver_id: int
    content: str
    message_type: Optional[str] = "text"
    file_data: Optional[str] = None

class MessageResponse(BaseModel):
    id: int
    sender_id: int
    receiver_id: int
    content: str
    message_type: str
    file_data: Optional[str] = None
    timestamp: datetime
    is_read: bool
```

---

<a name="ma-loi"></a>
## 10. Bảng mã lỗi chuẩn HTTP

| Mã HTTP | Tên mã | Trường hợp xảy ra |
|:---:|---|---|
| **200** | OK | Thao tác thành công |
| **400** | Bad Request | Dữ liệu đầu vào không hợp lệ hoặc username bị trùng |
| **401** | Unauthorized | Thiếu token, token sai hoặc đã hết hạn |
| **403** | Forbidden | Không có quyền thao tác (xóa tin người khác, gọi API Admin) |
| **404** | Not Found | Người dùng hoặc tin nhắn không tồn tại |
| **500** | Internal Server Error | Lỗi cơ sở dữ liệu hoặc ngoại lệ máy chủ chưa bắt được |

---

<a name="code-mau"></a>
## 11. Code mẫu gọi API

### Gửi tin nhắn bằng Python (`requests`):
```python
import requests

SERVER_URL = "http://192.168.1.100:8000"
headers = {"Authorization": f"Bearer {auth_token}"}

payload = {
    "receiver_id": 2,
    "content": "Xin chào từ Python script!",
    "message_type": "text"
}

response = requests.post(f"{SERVER_URL}/messages", json=payload, headers=headers)
print(response.json())
```

### Gọi bằng cURL:
```bash
curl -X POST "http://192.168.1.100:8000/messages" \
     -H "Authorization: Bearer <TOKEN>" \
     -H "Content-Type: application/json" \
     -d '{"receiver_id": 2, "content": "Hello World", "message_type": "text"}'
```

---

*Tài liệu đặc tả API chuẩn OpenAPI 3.0 - Local Messenger 2026*