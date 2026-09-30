# Câu chuyện người dùng (User Stories)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản:** 1.0 (Bản hiện thực thực tế)  
**Năm:** 2026  
**Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống  
**Trạng thái:** Đã đối soát 100% với mã nguồn dự án

---

## Hiện trạng tính năng thực tế trong mã nguồn:

### **Xác thực tài khoản (Authentication):**
- Đăng ký người dùng (`POST /auth/register`)
- Đăng nhập hệ thống (`POST /auth/login`)
- Cấp phát JWT token; người dùng đăng ký đầu tiên tự động nhận quyền Quản trị viên (Admin)

### **Danh bạ & Trạng thái người dùng:**
- Xem danh sách toàn bộ người dùng trong mạng (`GET /users`)
- Trạng thái trực tuyến trực quan (Online / Offline)
- Cơ chế quét cập nhật trạng thái tự động theo chu kỳ mỗi 10 giây

### **Tin nhắn & Đa phương tiện:**
- Gửi tin nhắn văn bản (`POST /messages`)
- Nhận tin nhắn tức thời qua kênh WebSocket thời gian thực
- Tải lịch sử trao đổi (`GET /messages?contact_id=`)
- Gửi hình ảnh dạng chuỗi Base64 (PNG, JPG, GIF, BMP)
- Hiển thị ảnh thu nhỏ xem trước trực tiếp trên khung chat

### **Quản lý tin nhắn:**
- Xóa tin nhắn do chính mình gửi theo ID (`DELETE /messages/{id}`)
- Phát thông báo sự kiện xóa qua WebSocket tới tất cả các client liên quan
- Menu chuột phải (Context menu) hỗ trợ thao tác xóa

### **Giao diện người dùng (UI):**
- Giao diện PyQt5 với thanh điều hướng dạng Tab (nhiều cuộc trò chuyện cùng lúc)
- Cột danh bạ bên trái, khung hội thoại hiển thị bên phải
- Phân biệt rõ ràng tin nhắn gửi đi (màu xanh, căn phải) và tin nhắn nhận về (màu xám, căn trái)

---

## 1. Đăng ký và Đăng nhập

### US-001: Đăng ký tài khoản mới
**Là một** người dùng mới  
**Tôi muốn** tạo tài khoản cá nhân trên hệ thống  
**Để** có thể truy cập và sử dụng ứng dụng nhắn tin

**Tiêu chí chấp nhận (Acceptance Criteria):**
- [x] Cho phép nhập Tên đăng nhập (Username) và Mật khẩu (Password).
- [x] Kiểm tra tính duy nhất của Username (báo lỗi nếu tên đã tồn tại).
- [x] Băm mật khẩu bằng thuật toán an toàn bcrypt trước khi lưu CSDL.
- [x] Người dùng tạo tài khoản đầu tiên tự động được gán quyền Admin.
- [x] Sau khi đăng ký thành công, thông báo hoàn tất và yêu cầu đăng nhập.

---

### US-002: Đăng nhập vào hệ thống
**Là một** người dùng đã có tài khoản  
**Tôi muốn** đăng nhập vào tài khoản của mình  
**Để** bắt đầu trò chuyện với bạn bè, đồng nghiệp

**Tiêu chí chấp nhận:**
- [x] Nhập Username và Password chính xác.
- [x] Xác thực thông tin qua API; trả về JWT token nếu hợp lệ.
- [x] Cập nhật trạng thái `is_online = True` trong CSDL.
- [x] Mở giao diện chính hiển thị danh bạ người dùng.
- [x] Báo lỗi rõ ràng nếu nhập sai thông tin xác thực.

---

## 2. Quản lý danh bạ & Cuộc trò chuyện

### US-003: Xem danh sách người dùng
**Là một** người dùng trong hệ thống  
**Tôi muốn** nhìn thấy danh sách mọi người  
**Để** biết ai đang trực tuyến và có thể trò chuyện

**Tiêu chí chấp nhận:**
- [x] Danh sách hiển thị tại cột bên trái của giao diện chính.
- [x] Hiển thị chấm trạng thái: [Online] (Trực tuyến) hoặc [Offline] (Ngoại tuyến).
- [x] Danh sách tự động làm mới trạng thái định kỳ mỗi 10 giây.

---

### US-004: Mở tab trò chuyện với một người
**Là một** người dùng  
**Tôi muốn** mở một cuộc hội thoại với một người bất kỳ  
**Để** bắt đầu trao đổi tin nhắn riêng

**Tiêu chí chấp nhận:**
- [x] Nhấp đúp hoặc bấm vào tên liên hệ trong danh bạ.
- [x] Tạo một tab mới mang tên người đó trên thanh tab chat.
- [x] Tự động tải lịch sử các tin nhắn đã trao đổi trước đây.
- [x] Hỗ trợ mở và chuyển đổi linh hoạt giữa nhiều tab trò chuyện cùng lúc.

---

## 3. Gửi và Nhận tin nhắn

### US-005: Gửi tin nhắn văn bản
**Là một** người đang trong phòng chat  
**Tôi muốn** soạn và gửi tin nhắn chữ  
**Để** trao đổi thông tin nhanh chóng

**Tiêu chí chấp nhận:**
- [x] Nhập nội dung vào thanh soạn thảo ở dưới cùng và nhấn nút "Gửi" hoặc phím Enter.
- [x] Tin nhắn lập tức được lưu vào CSDL máy chủ.
- [x] Hiển thị tin nhắn ngay trên khung chat người gửi (màu xanh, bên phải).
- [x] Bắn sự kiện đẩy tin nhắn qua WebSocket tới người nhận.

---

### US-006: Nhận tin nhắn thời gian thực
**Là một** người dùng đang mở ứng dụng  
**Tôi muốn** nhận tin nhắn ngay khi người khác vừa gửi  
**Để** nắm bắt thông tin kịp thời mà không cần bấm tải lại

**Tiêu chí chấp nhận:**
- [x] Tự động đón nhận tin nhắn qua WebSocket socket event.
- [x] Hiển thị tức thời vào đúng tab trò chuyện tương ứng.
- [x] Hiển thị rõ tên người gửi, thời gian gửi (Giờ:Phút).
- [x] Định dạng màu xám, căn về phía bên trái.

---

### US-007: Xem lịch sử trò chuyện
**Là một** người dùng  
**Tôi muốn** xem lại các tin nhắn cũ  
**Để** nắm lại nội dung cuộc thảo luận trước đó

**Tiêu chí chấp nhận:**
- [x] Tải 100 tin nhắn gần nhất khi mở khung chat.
- [x] Sắp xếp theo trình tự thời gian (cũ ở trên, mới ở dưới).
- [x] Hiển thị mã định danh tin nhắn (Message ID) để phục vụ quản trị hoặc xóa.

---

## 4. Gửi nhận hình ảnh

### US-008: Gửi hình ảnh đính kèm
**Là một** người dùng  
**Tôi muốn** gửi ảnh qua tin nhắn  
**Để** chia sẻ tài liệu trực quan, ảnh chụp màn hình

**Tiêu chí chấp nhận:**
- [x] Bấm nút [Đính kèm] cạnh ô nhập tin nhắn để mở hộp thoại chọn file.
- [x] Hỗ trợ các định dạng ảnh phổ biến: PNG, JPG, JPEG, GIF, BMP.
- [x] Mã hóa file ảnh sang dạng Base64 và truyền tải qua API.
- [x] Hiển thị ảnh thu nhỏ với chiều rộng 200px trong khung chat.

---

### US-009: Xem hình ảnh nhận được
**Là một** người nhận  
**Tôi muốn** nhìn thấy ảnh trực tiếp trong cuộc hội thoại  
**Để** xem nội dung mà không cần phải tải về mở bằng phần mềm khác

**Tiêu chí chấp nhận:**
- [x] Ảnh hiển thị trực tiếp trong bong bóng tin nhắn.
- [x] Tự động giải mã chuỗi Base64 và kết xuất giao diện.

---

## 5. Xóa tin nhắn

### US-010: Xóa tin nhắn cá nhân
**Là một** người đã gửi tin nhắn  
**Tôi muốn** xóa tin nhắn mình đã gửi  
**Để** thu hồi thông tin nhầm lẫn

**Tiêu chí chấp nhận:**
- [x] Nhấp chuột phải vào tin nhắn $\rightarrow$ Chọn "Delete Message".
- [x] Nhập xác nhận ID tin nhắn cần xóa.
- [x] Hệ thống kiểm tra quyền sở hữu (chỉ cho phép xóa tin của chính mình).
- [x] Xóa bản ghi trong CSDL và gửi lệnh xóa qua WebSocket tới máy người nhận.

---

## 6. Chức năng Quản trị (Admin)

### ADM-001: Xem toàn bộ tin nhắn hệ thống (Admin)
**Là một** quản trị viên hệ thống  
**Tôi muốn** truy xuất toàn bộ dữ liệu tin nhắn qua API  
**Để** giám sát và kiểm duyệt an toàn mạng nội bộ

**Tiêu chí chấp nhận:**
- [x] Endpoint `GET /admin/all-messages` chỉ cho phép token của tài khoản có quyền `is_admin = True`.
- [x] Trả về toàn bộ lịch sử tin nhắn cùng định danh người gửi / người nhận.

---

## 7. Ma trận hiện thực yêu cầu (Traceability Matrix)

| Mã Story | Tên chức năng | Trạng thái mã nguồn | Kết quả |
|---|---|---|:---:|
| **US-001** | Đăng ký tài khoản | `auth.py`, `login_dialog.py` | Hoàn thành |
| **US-002** | Đăng nhập hệ thống | `auth.py`, `login_dialog.py`, JWT | Hoàn thành |
| **US-003** | Danh sách danh bạ | `users.py`, `main_window.py` | Hoàn thành |
| **US-004** | Mở tab chat riêng | `main_window.py`, `chat_widget.py` | Hoàn thành |
| **US-005** | Gửi tin nhắn text | `messages.py`, `chat_widget.py` | Hoàn thành |
| **US-006** | Nhận tin nhắn WebSocket | `websocket_manager.py`, `websocket_client.py` | Hoàn thành |
| **US-007** | Xem lịch sử chat | `messages.py`, `chat_widget.py` | Hoàn thành |
| **US-008** | Gửi hình ảnh Base64 | `chat_widget.py`, Pillow, Base64 | Hoàn thành |
| **US-009** | Hiển thị hình ảnh | `chat_widget.py`, QPixmap | Hoàn thành |
| **US-010** | Xóa tin nhắn cá nhân | `messages.py`, WebSocket broadcast | Hoàn thành |
| **ADM-001** | API Quản trị tin nhắn | `admin.py`, xác thực Admin | Hoàn thành |

---

*Tài liệu phản ánh chính xác các tính năng có trong mã nguồn thực tế - Dự án Local Messenger 2026*