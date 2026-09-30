# Sổ tay hướng dẫn sử dụng (User Manual)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản:** 1.0  
**Năm:** 2026  
**Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống

---

## Mục lục
1. [Khởi động nhanh](#khoi-dong-nhanh)
2. [Cài đặt ứng dụng Client](#cai-dat-ung-dung-client)
3. [Lần đầu sử dụng](#lan-dau-su-dung)
4. [Giao diện làm việc chính](#giao-dien-lam-viec-chinh)
5. [Thao tác với các phòng chat](#thao-tac-voi-phong-chat)
6. [Gửi và nhận tin nhắn](#gui-va-nhan-tin-nhan)
7. [Gửi và xem hình ảnh](#gui-va-xem-hinh-anh)
8. [Quản lý và xóa tin nhắn](#quan-ly-va-xoa-tin-nhan)
9. [Các câu hỏi thường gặp (FAQ)](#cau-hoi-thuong-gap)
10. [Giới hạn của hệ thống](#gioi-han-he-thong)

---

<a name="khoi-dong-nhanh"></a>
## 1. Khởi động nhanh (Quickstart)

### Điều kiện cần chuẩn bị:
1. **Địa chỉ IP của máy Server:** Hỏi người quản trị mạng nội bộ (IT Admin) hoặc để ứng dụng tự động dò tìm qua mạng LAN (Ví dụ: `192.168.1.100`).
2. Máy tính của bạn kết nối vào cùng mạng Wi-Fi hoặc dây LAN với máy chủ.
3. Máy tính đã cài đặt Python 3.8 trở lên.

### Các bước thực hiện nhanh:
1. Cấu hình IP server trong file `config.py`.
2. Cài đặt thư viện: `pip install pyqt5 requests websockets`.
3. Chạy Client: `python3 main.py`.
4. Đăng ký tài khoản và bắt đầu trò chuyện.

---

<a name="cai-dat-ung-dung-client"></a>
## 2. Cài đặt ứng dụng Client

### Cấu hình file `config.py`
Mở file `client/config.py` bằng trình soạn thảo và điền IP của máy Server:
```python
# client/config.py
SERVER_HOST = "192.168.1.100"  # ← Thay đổi thành địa chỉ IP thực tế của máy chủ
SERVER_PORT = 8000
SERVER_URL = f"http://{SERVER_HOST}:{SERVER_PORT}"
```

### Khởi chạy:
```bash
cd client
python3 main.py
```

---

<a name="lan-dau-su-dung"></a>
## 3. Lần đầu sử dụng

### 3.1. Hộp thoại Đăng nhập / Đăng ký
Khi khởi chạy, cửa sổ xác thực sẽ xuất hiện:
* **Đăng ký (Register):** Nếu chưa có tài khoản, nhấn nút "Đăng ký", nhập Tên đăng nhập và Mật khẩu.  
  *(Lưu ý: Tài khoản đăng ký đầu tiên trên hệ thống sẽ tự động trở thành Quản trị viên - Admin).*
* **Đăng nhập (Login):** Nhập tài khoản vừa tạo và nhấn "Đăng nhập". Khi đăng nhập thành công, cửa sổ ứng dụng chính sẽ mở ra.

---

<a name="giao-dien-lam-viec-chinh"></a>
## 4. Giao diện làm việc chính

```
┌─────────────────────────────────────────┐
│ Local Messenger                         │
├─────────────────┬───────────────────────┤
│   DANH BẠ       │      KHUNG CHAT       │
│   ┌──────────┐  │                       │
│   │ [Online] Nam    │ │  Trò chuyện với: Nam  │
│   │ [Offline] Hùng   │ │ ┌──────────────────┐  │
│   │ [Online] Mai    │ │ │ 14:30 Nam:       │  │
│   │ [Offline] Lan    │ │ │ Xin chào!        │  │
│   │          │ │ │                  │  │
│   │          │ │ │ 14:31 Bạn:       │  │
│   │          │ │ │ Bài tập xong chưa?│ │
│   └──────────┘ │ └──────────────────┘  │
│                 │ ┌──────────────────┐  │
│                 │ │ [Nhập nội dung...]│  │
│                 │ └──────────────────┘  │
│                 │   [[Đính kèm]] [  Gửi  ]     │
└─────────────────┴───────────────────────┘
```

* **Cột Danh bạ (Bên trái):** Hiển thị danh sách tất cả các bạn học trong lớp.
  * [Online] Chấm xanh: Đang trực tuyến (Online).
  * [Offline] Chấm xám: Đang ngoại tuyến (Offline).
  * Danh sách tự động làm mới trạng thái mỗi 10 giây.
* **Khung Chat (Bên phải):** Hiển thị lịch sử hội thoại và thanh công cụ soạn thảo tin nhắn.

---

<a name="thao-tac-voi-phong-chat"></a>
## 5. Thao tác với các phòng chat

1. **Bắt đầu trò chuyện:** Nhấp chuột vào tên người bạn muốn chat ở cột bên trái $\rightarrow$ Hệ thống sẽ mở một Tab trò chuyện mới mang tên người đó.
2. **Chat nhiều người:** Bạn có thể mở nhiều tab trò chuyện cùng lúc và nhấp qua lại giữa các tab ở thanh tiêu đề trên cùng.
3. **Đóng tab:** Nhấn vào dấu `x` ở góc tab để đóng khung chat (Lịch sử trò chuyện vẫn được lưu trên máy chủ an toàn).

---

<a name="gui-va-nhan-tin-nhan"></a>
## 6. Gửi và nhận tin nhắn

* Nhập nội dung vào thanh văn bản dưới cùng.
* Nhấn phím **Enter** hoặc nhấp chuột vào nút **"Gửi"**.
* **Quy ước màu sắc:**
  * Tin nhắn của bạn: Căn lề bên phải, nền màu xanh dương.
  * Tin nhắn của đối phương: Căn lề bên trái, nền màu xám.
  * Dưới mỗi tin nhắn có hiển thị mốc thời gian (Giờ:Phút) và mã số tin nhắn (`ID: xxx`).

---

<a name="gui-va-xem-hinh-anh"></a>
## 7. Gửi và xem hình ảnh

1. Trong tab chat đang mở, nhấp vào biểu tượng chiếc kẹp ghim **[Đính kèm]**.
2. Chọn file hình ảnh từ máy tính (Hỗ trợ định dạng `.png`, `.jpg`, `.jpeg`, `.gif`, `.bmp`).
3. Nhấn **"Open"** $\rightarrow$ Ảnh sẽ tự động được gửi và xuất hiện ngay trong khung chat của cả hai bạn.

---

<a name="quan-ly-va-xoa-tin-nhan"></a>
## 8. Quản lý và xóa tin nhắn

Bạn có thể xóa tin nhắn do chính bạn gửi đi để sửa nhầm lẫn:
1. Nhìn vào mã số **ID** hiển thị ngay dưới tin nhắn muốn xóa.
2. Nhấp chuột phải vào tin nhắn $\rightarrow$ Chọn **"Delete Message"**.
3. Nhập mã ID của tin nhắn vào hộp thoại xác nhận $\rightarrow$ Nhấn **OK**.
4. Tin nhắn sẽ lập tức biến mất ở cả màn hình của bạn và màn hình người nhận.

---

<a name="cau-hoi-thuong-gap"></a>
## 9. Các câu hỏi thường gặp (FAQ)

### Q1: Bị báo lỗi "Cannot connect to server"?
* **Giải pháp:** Kiểm tra lại địa chỉ IP trong file `client/config.py`. Hỏi người phụ trách xem máy Server đã khởi chạy chưa.

### Q2: Tại sao trong danh bạ chỉ có một mình tôi?
* **Giải pháp:** Đợi 10 - 20 giây để hệ thống quét cập nhật, hoặc bảo bạn cùng phòng máy đăng nhập vào hệ thống.

### Q3: Tôi quên mật khẩu thì lấy lại thế nào?
* **Giải pháp:** Vì là hệ thống mạng nội bộ học tập, tính năng tự lấy lại mật khẩu qua email chưa hỗ trợ. Bạn hãy liên hệ Quản trị viên (người tạo tài khoản đầu tiên) để được cấp lại tài khoản mới.

---

<a name="gioi-han-he-thong"></a>
## 10. Giới hạn của hệ thống (Những điều phần mềm CHƯA hỗ trợ)

* Chưa hỗ trợ tạo nhóm chat nhiều người (hiện tại hỗ trợ chat riêng 1-1).
* Chưa hỗ trợ gọi thoại (Audio) hay gọi video (Video call).
* Không đồng bộ qua Internet ra ngoài khuôn viên trường học (chỉ chạy trong mạng LAN).
* Không hỗ trợ ứng dụng trên điện thoại di động (Android / iOS).

---

*Tài liệu hướng dẫn người dùng - Dự án Local Messenger 2026*