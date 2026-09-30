# Kế hoạch kiểm thử ứng dụng Local Messenger (Test Plan)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật

**Phiên bản tài liệu:** 1.0 (Release)  
**Năm:** 2026  
**Đơn vị phát triển:** Bộ phận Đảm bảo Chất lượng Phần mềm (QA Team)

---

## 1. Tổng quan
* **Đối tượng:** Ứng dụng Desktop Client (PyQt5) và Server Backend (FastAPI).
* **Loại ứng dụng:** Desktop Client kết nối REST API và WebSocket.
* **Mục tiêu:** Đảm bảo tính ổn định, độ tin cậy và sự chính xác của giao diện người dùng khi gửi/nhận tin nhắn, quản lý danh bạ và nhận sự kiện thời gian thực.

---

## 2. Đối tượng kiểm thử (Test Objects)

* `main.py`: Khởi tạo và quản lý vòng đời ứng dụng.
* `login_dialog.py`: Hộp thoại đăng nhập và đăng ký tài khoản.
* `main_window.py`: Cửa sổ giao diện chính, danh bạ liên hệ, hệ thống các tab trò chuyện.
* `chat_widget.py`: Khung chat, nhập nội dung, nút gửi ảnh, menu xóa tin nhắn.
* `websocket_client.py`: Quản lý kết nối hai chiều WebSocket.
* `config.py`: File cấu hình địa chỉ IP máy chủ.
* `message.py`, `user.py`: Các mô hình dữ liệu xử lý phía Client.

---

## 3. Các phương pháp kiểm thử

1. **Kiểm thử chức năng giao diện (UI Functional Testing):** Kiểm tra hiển thị cửa sổ, nút bấm, trường nhập liệu, định dạng tin nhắn và phản hồi thao tác người dùng.
2. **Kiểm thử tích hợp (Integration Testing):** Kiểm tra tương tác giữa Client và REST API, kiểm tra nhận gói tin đẩy qua WebSocket.
3. **Kiểm thử khả năng chịu lỗi mạng (Network Resilience Testing):** Ngắt kết nối mạng đột ngột, khởi động lại server, kiểm tra cơ chế tự động kết nối lại (auto-reconnect).

---

## 4. Môi trường kiểm thử

* **Hệ điều hành:** Windows 10/11, Ubuntu Linux 20.04+, macOS.
* **Hạ tầng mạng:** Mạng LAN nội bộ (Ethernet hoặc Wi-Fi).
* **Phần mềm:** Python 3.8+, PyQt5, `requests`, `websockets`, máy chủ FastAPI đang chạy tại cổng `8000`.

---

## 5. Danh mục các kịch bản kiểm thử (Test Cases)

### 5.1. Xác thực tài khoản (`login_dialog.py`)

* **TC-AUTH-01: Đăng nhập thành công**
  * *Tiền điều kiện:* Tài khoản đã tồn tại trên hệ thống.
  * *Các bước:* Nhập đúng Username & Password $\rightarrow$ Nhấn "Login".
  * *Kết quả mong đợi:* Cửa sổ đăng nhập đóng lại, mở ra cửa sổ chính `MainWindow`.
* **TC-AUTH-02: Đăng nhập thất bại (Sai thông tin)**
  * *Các bước:* Nhập sai mật khẩu $\rightarrow$ Nhấn "Login".
  * *Kết quả mong đợi:* Hiển thị thông báo "Invalid credentials", không cho phép vào trong.
* **TC-AUTH-03: Đăng ký người dùng mới**
  * *Các bước:* Nhập Username mới và Password $\rightarrow$ Nhấn "Register".
  * *Kết quả mong đợi:* Thông báo "Registration successful".
* **TC-AUTH-04: Mất kết nối tới máy chủ**
  * *Tiền điều kiện:* Server chưa được bật.
  * *Kết quả mong đợi:* Báo lỗi "Cannot connect to server".

### 5.2. Cửa sổ làm việc chính (`main_window.py`)

* **TC-MAIN-01: Tải danh bạ người dùng:** Đăng nhập thành công $\rightarrow$ Cột bên trái hiển thị danh sách tất cả người dùng trong hệ thống.
* **TC-MAIN-02: Cập nhật trạng thái trực tuyến:** Người dùng khác vừa đăng nhập/đăng xuất $\rightarrow$ Sau tối đa 10 giây biểu tượng chuyển đổi tương ứng ([Online]/[Offline]).
* **TC-MAIN-03: Mở tab trò chuyện:** Nhấp chuột vào tên liên hệ $\rightarrow$ Mở tab trò chuyện mới kèm lịch sử tin nhắn cũ.
* **TC-MAIN-04: Mở trùng lặp:** Nhấp vào liên hệ đã mở tab $\rightarrow$ Chuyển tab hiện có lên trước, không tạo thêm tab thừa.
* **TC-MAIN-05: Đóng tab:** Nhấn dấu 'X' trên tiêu đề tab $\rightarrow$ Tab đóng lại an toàn.

### 5.3. Khung trò chuyện (`chat_widget.py`)

* **TC-CHAT-01: Gửi tin nhắn chữ:** Nhập chữ $\rightarrow$ Nhấn "Send" $\rightarrow$ Tin nhắn hiển thị màu xanh ở bên phải và xuất hiện ngay lập tức trên máy người nhận.
* **TC-CHAT-02: Gửi file ảnh:** Bấm nút [Đính kèm] $\rightarrow$ Chọn file ảnh (.png/.jpg) $\rightarrow$ Ảnh hiển thị kích thước thu nhỏ (200px) ở cả 2 màn hình.
* **TC-CHAT-03: Nhận tin nhắn WebSocket:** Người đối diện gửi tin $\rightarrow$ Tin nhắn tự động hiển thị mà không cần tải lại trang.
* **TC-CHAT-04: Tải lịch sử tin nhắn:** Khi mở tab, 100 tin nhắn gần nhất được tải về và sắp xếp đúng thứ tự thời gian.
* **TC-CHAT-05: Xóa tin nhắn cá nhân:** Chuột phải vào tin nhắn $\rightarrow$ Chọn "Delete Message" $\rightarrow$ Nhập ID $\rightarrow$ Tin nhắn biến mất trên cả máy gửi và máy nhận.
* **TC-CHAT-06: Phân biệt trực quan:** Tin gửi đi căn lề phải (xanh dương), tin nhận về căn lề trái (xám).

### 5.4. Kết nối WebSocket (`websocket_client.py`)

* **TC-WS-01: Tự động kết nối:** Mở màn hình chính $\rightarrow$ WebSocket kết nối thành công.
* **TC-WS-02: Giữ kết nối Ping/Pong:** Ứng dụng duy trì kết nối ổn định sau nhiều phút không thao tác.
* **TC-WS-03: Khôi phục kết nối:** Rút dây mạng 5 giây rồi cắm lại $\rightarrow$ Kết nối WebSocket tự phục hồi.

---

## 6. Ma trận phân bổ độ ưu tiên

| Mức ưu tiên | Các kịch bản kiểm thử | Lý do |
|---|---|---|
| **Cao (Critical)** | TC-AUTH-01, TC-AUTH-02, TC-CHAT-01, TC-CHAT-03 | Tính năng cốt lõi bắt buộc phải chạy |
| **Trung bình (Major)**| TC-AUTH-03, TC-MAIN-01, TC-CHAT-02, TC-CHAT-05 | Chức năng nâng cao và tiện ích chính |
| **Thấp (Minor)** | TC-CHAT-06, TC-WS-02, TC-WS-03 | Tối ưu trải nghiệm và xử lý biên |

---

## 7. Lịch trình kiểm thử đề xuất (5 ngày)

* **Ngày 1:** Thiết lập môi trường, kiểm thử luồng đăng ký & đăng nhập (TC-AUTH).
* **Ngày 2:** Kiểm thử danh bạ và quản lý tab cửa sổ chính (TC-MAIN).
* **Ngày 3:** Kiểm thử toàn diện tính năng chat văn bản và gửi ảnh (TC-CHAT).
* **Ngày 4:** Kiểm thử đồng bộ WebSocket và kiểm thử tải nhẹ với nhiều client.
* **Ngày 5:** Kiểm thử xử lý lỗi ngoại lệ, kiểm thử hồi quy (Regression Testing) và lập báo cáo.

---

*Kế hoạch kiểm thử ứng dụng Local Messenger - Năm 2026*