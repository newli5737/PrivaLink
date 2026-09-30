# Báo cáo phân tích hệ thống (System Analysis)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản tài liệu:** 1.0 (Bản hiện thực thực tế)  
**Năm:** 2026  
**Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống  
**Trạng thái:** Báo cáo phân tích chuyên sâu đối soát trực tiếp từ mã nguồn thực tế

---

## 1. Giới thiệu tổng quan

Tài liệu "Phân tích hệ thống" nghiên cứu toàn diện dự án "Local Messenger" dưới góc độ kỹ thuật: kiến trúc phần mềm, sự tương tác giữa các thành phần, phân tích SWOT, nợ kỹ thuật (Technical Debt) và lộ trình nâng cấp lâu dài.

* **Đối tượng phân tích:** Hệ thống nhắn tin nội bộ Client - Server.
* **Quy mô:** Dự án phần mềm truyền thông nội bộ theo tiêu chuẩn công nghiệp (On-premise LAN Solution).
* **Trạng thái thực tế:** Đã hiện thực hóa hoàn chỉnh và hoạt động ổn định.

---

## 2. Đánh giá mức độ đáp ứng yêu cầu nghiệp vụ

| Nhóm yêu cầu | Giải pháp hiện thực trong Code | Đánh giá | Ghi chú |
|---|---|:---:|---|
| **Đăng ký & Đăng nhập** | JWT Token + bcrypt hash | Tốt | User đầu tiên tự động nhận quyền Admin |
| **Danh bạ & Trạng thái** | QListWidget + quét chu kỳ 10 giây | Tốt | Chấm xanh (Online) / Chấm xám (Offline) |
| **Nhắn tin văn bản** | REST API + WebSocket broadcast | Rất tốt | Lưu trữ tin cậy trong CSDL SQLite |
| **Gửi nhận hình ảnh** | Mã hóa chuỗi Base64 | Đạt | Hỗ trợ PNG, JPG, GIF, BMP, thumbnail 200px |
| **Xem lại lịch sử** | Phân trang / Giới hạn 100 tin gần nhất | Đạt | Tải tự động khi mở tab chat |
| **Xóa tin nhắn** | DELETE endpoint + đồng bộ WebSocket | Tốt | Chỉ cho phép xóa tin nhắn của chính mình |
| **Quản trị hệ thống** | Endpoint `/admin/*` kiểm tra role | Đạt | Truy xuất qua Swagger UI / REST API |

---

## 3. Phân tích kiến trúc phân tầng (Layered Architecture)

Hệ thống tuân thủ mô hình phân tầng chặt chẽ:

```
Phía Client (PyQt5)                 Phía Server (FastAPI)
┌────────────────────────┐         ┌────────────────────────┐
│ Tầng giao diện (UI)    │         │ Tầng API Định tuyến    │
│ (MainWindow, Chat,..)  │         │ (Routers: auth, msg..) │
├────────────────────────┤  HTTP   ├────────────────────────┤
│ Tầng Logic nghiệp vụ   │◄───────►│ Tầng dịch vụ & Schemas │
│ (Models, Controllers)  │   WS    │ (Pydantic Validation)  │
├────────────────────────┤         ├────────────────────────┤
│ Tầng kết nối mạng      │         │ Tầng truy xuất CSDL    │
│ (Requests, WebSocket)  │         │ (SQLAlchemy / SQLite)  │
└────────────────────────┘         └────────────────────────┘
```

### Luận cứ kỹ thuật cho các quyết định cốt lõi:
1. **Lựa chọn FastAPI thay vì Flask/Django:** Hỗ trợ mô hình bất đồng bộ (async/await) tự nhiên, hiệu năng tương đương Node.js/Go, tích hợp sẵn WebSocket và tài liệu Swagger UI tự động.
2. **Lựa chọn SQLite thay vì PostgreSQL/MySQL:** Không cần cài đặt máy chủ cơ sở dữ liệu cồng kềnh, giảm thiểu tối đa rào cản khi triển khai thực hành trong phòng máy trường học.
3. **Lựa chọn WebSocket kết hợp REST:** Tận dụng REST cho các tác vụ đồng bộ truyền thống (CRUD) và WebSocket cho việc đẩy tin nhắn thời gian thực hai chiều.

---

## 4. Phân tích ma trận SWOT của hệ thống

```
┌──────────────────────────────────────┬──────────────────────────────────────┐
│ ĐIỂM MẠNH (STRENGTHS)                │ ĐIỂM YẾU (WEAKNESSES)                │
├──────────────────────────────────────┼──────────────────────────────────────┤
│ • Dễ dàng cài đặt và vận hành        │ • Chưa hỗ trợ chat nhóm đông người   │
│ • Hoạt động hoàn toàn không cần Net  │ • Dung lượng ảnh Base64 tốn CSDL     │
│ • Tốc độ phản hồi cực nhanh trong LAN│ • Phải nhập ID thủ công khi xóa tin  │
│ • Kiến trúc code phân tách sạch sẽ   │ • Chưa có giao diện Web quản trị     │
├──────────────────────────────────────┼──────────────────────────────────────┤
│ CƠ HỘI (OPPORTUNITIES)               │ THÁCH THỨC (THREATS)                 │
├──────────────────────────────────────┼──────────────────────────────────────┤
│ • Dễ dàng nâng cấp sang PostgreSQL   │ • SQLite nghẽn nếu ghi đồng thời lớn │
│ • Bổ sung mã hóa đầu cuối (E2EE)     │ • Thiếu HTTPS nếu mạng LAN bị nghe lén│
│ • Đóng gói thành file chạy .EXE      │ • Xung đột IP nếu card mạng đổi IP   │
└──────────────────────────────────────┴──────────────────────────────────────┘
```

---

## 5. Phân tích nợ kỹ thuật (Technical Debt)

1. **Truyền tải ảnh qua Base64:** Chuỗi Base64 làm phình to kích thước dữ liệu khoảng 33% và lưu trực tiếp trong bảng SQLite. *Giải pháp tái cấu trúc:* Lưu file ảnh vào thư mục `uploads/` trên ổ cứng và chỉ lưu đường link URL trong CSDL.
2. **Khảo sát trạng thái Online bằng Polling 10s:** Dù có WebSocket nhưng danh bạ hiện đang dùng timer quét lại mỗi 10 giây. *Giải pháp tái cấu trúc:* Chuyển hoàn toàn trạng thái online/offline sang phát sự kiện WebSocket tức thời (`user_connected` / `user_disconnected`).
3. **Thao tác xóa tin nhắn:** Người dùng phải nhìn mã ID để nhập xóa. *Giải pháp tái cấu trúc:* Gán trực tiếp ID vào đối tượng nút xóa trên giao diện để xóa một chạm.

---

## 6. Lộ trình phát triển đề xuất (Roadmap)

### Giai đoạn 1 (Nâng cấp trải nghiệm người dùng - UI/UX):
- Bổ sung nút xóa tin nhắn trực tiếp không cần gõ ID.
- Cho phép nhấp đúp vào ảnh để phóng to toàn màn hình.
- Thêm âm thanh và popup thông báo tin nhắn mới khi thu nhỏ cửa sổ.

### Giai đoạn 2 (Nâng cấp tính năng nâng cao):
- Hỗ trợ tạo phòng chat nhóm (Group Chat).
- Tìm kiếm tin nhắn theo từ khóa trong lịch sử trò chuyện.
- Lưu trữ file ảnh trên hệ thống tệp thay vì Base64 trong SQLite.

### Giai đoạn 3 (Bảo mật và Mở rộng quy mô):
- Chuyển CSDL sang PostgreSQL khi mở rộng quy mô toàn doanh nghiệp/tổ chức.
- Kích hoạt giao thức mã hóa SSL/TLS (HTTPS và WSS).
- Phát triển thêm giao diện Web hoặc ứng dụng di động Flutter.

---

*Tài liệu Báo cáo phân tích hệ thống - Local Messenger 2026*