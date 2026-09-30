# Kế hoạch Kiểm thử Chấp nhận & Nghiệm thu Dự án (Acceptance Plan / UAT)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản tài liệu:** 1.0.0 (Release)  
**Ngày phát hành:** 23.01.2026  
**Đơn vị phát triển:** Ban dự án phần mềm / Đội ngũ kỹ thuật (Engineering Team)  
**Đơn vị tiếp nhận:** Đại diện Khách hàng & Bộ phận CNTT đối tác  

---

## 1. Thông tin chung & Mục đích tài liệu

### 1.1. Mục đích
Tài liệu này xác định quy trình, kịch bản kiểm thử chấp nhận người dùng (**User Acceptance Testing - UAT**), các tiêu chuẩn đánh giá chất lượng kỹ thuật và biên bản bàn giao giải pháp phần mềm "Local Messenger" giữa Đơn vị phát triển và Khách hàng.

Mục tiêu chính là giúp Khách hàng hiểu rõ các tiêu chí kiểm thử thực tế, thẩm định tính chuẩn xác của các tài liệu thiết kế ban đầu và xác nhận hệ thống đã sẵn sàng đưa vào vận hành chính thức trong hạ tầng mạng nội bộ của đơn vị.

### 1.2. Môi trường và Hình thức kiểm thử nghiệm thu
* **Môi trường thử nghiệm:** Mạng nội bộ cục bộ (LAN) độc lập, kết nối tối thiểu 02 máy trạm Client và 01 máy chủ Server.
* **Thời lượng phiên UAT:** 45 - 60 phút.
* **Phương thức:** Đại diện Khách hàng trực tiếp đối soát tài liệu, thực thi kịch bản kiểm thử 16 bước trên giao diện thực tế, kiểm tra log hệ thống và đối chiếu với hồ sơ đặc tả yêu cầu ban đầu.

---

## 2. Đối tượng và Phạm vi nghiệm thu

1. **Sản phẩm phần mềm hoàn thiện:**
   * Dịch vụ máy chủ Backend (FastAPI, WebSocket Server, cơ sở dữ liệu SQLite).
   * Ứng dụng máy trạm Desktop Client (PyQt5 GUI, Network Manager).
2. **Bộ hồ sơ tài liệu thiết kế và kỹ thuật (15 tài liệu):**
   * Đầy đủ toàn bộ tài liệu kiến trúc, đặc tả kỹ thuật SRS, yêu cầu nghiệp vụ BRD, tài liệu API, hướng dẫn sử dụng, hướng dẫn cài đặt và bảo trì.
3. **Chất lượng mã nguồn:**
   * Cấu trúc phân tầng rõ ràng, tuân thủ chuẩn PEP 8, có chú thích mã nguồn và mã hóa an toàn dữ liệu mật khẩu/token.
4. **Năng lực chuyển giao và hỗ trợ vận hành:**
   * Hướng dẫn quản trị viên làm chủ quy trình sao lưu dữ liệu, cấu hình mạng và xử lý sự cố.

---

## 3. Quy trình nghiệm thu 5 bước chuẩn hóa

### Bước 1: Thẩm định hồ sơ thiết kế & Tài liệu kỹ thuật
- [ ] Bàn giao đủ 15 tài liệu kỹ thuật định dạng chuẩn Markdown (.md).
- [ ] Toàn bộ mã nguồn sản phẩm được đóng gói sạch sẽ, có file cấu hình môi trường rõ ràng.
- [ ] Môi trường máy chủ và máy trạm được thiết lập sẵn sàng theo tài liệu hướng dẫn triển khai.

### Bước 2: Kịch bản UAT kiểm thử chức năng thực tế (Checklist 16 bước)

Khách hàng thực hiện lần lượt các thao tác sau trên hệ thống thực tế để kiểm tra tính năng:

| STT | Thao tác thực hiện | Kết quả kỳ vọng | Trạng thái đạt |
|:---:|---|---|:---:|
| 1 | Khởi chạy Server cổng 8000 | Server bật thành công, mở được trang Swagger UI tại `http://localhost:8000/docs` | [ ] |
| 2 | Khởi chạy Client 1 (Máy trạm A) | Cửa sổ đăng nhập hiển thị chính xác, giao diện hiện đại | [ ] |
| 3 | Đăng ký tài khoản quản trị `User1` | Hệ thống báo thành công, tài khoản khởi tạo đầu tiên nhận quyền Admin | [ ] |
| 4 | Đăng nhập tài khoản `User1` | Đăng nhập thành công vào giao diện chính, danh bạ sẵn sàng | [ ] |
| 5 | Khởi chạy Client 2 (Máy trạm B) | Cửa sổ ứng dụng hiển thị độc lập trên máy trạm thứ hai | [ ] |
| 6 | Đăng ký tài khoản thành viên `User2` | Đăng ký thành công tài khoản người dùng thông thường | [ ] |
| 7 | Đăng nhập tài khoản `User2` | Đăng nhập thành công, thấy tài khoản `User1` trong danh bạ | [ ] |
| 8 | Kiểm tra trạng thái trực tuyến | Khi cả hai cùng online, biểu tượng trạng thái chuyển sang màu xanh lá [Online] tức thời | [ ] |
| 9 | Mở phiên trò chuyện riêng | Người dùng nhấp vào tên đối tác trong danh bạ, tab trò chuyện mở ra ngay | [ ] |
| 10 | Gửi tin nhắn văn bản từ Client 1 | Tin nhắn hiển thị ngay bên phải (bong bóng xanh) kèm thời gian thực | [ ] |
| 11 | Nhận tin nhắn tức thời ở Client 2 | Tin nhắn xuất hiện bên trái (bong bóng xám) qua WebSocket dưới 100ms | [ ] |
| 12 | Phản hồi hai chiều Client 2 $\rightarrow$ Client 1 | Luồng trao đổi diễn ra liên tục, mượt mà và chính xác thứ tự | [ ] |
| 13 | Gửi tệp hình ảnh qua nút [Đính kèm] | Tải ảnh lên thành công, client tự động tạo ảnh thu nhỏ (thumbnail 200px) | [ ] |
| 14 | Xem trước và tải ảnh bên nhận | Bên nhận xem được ảnh thumbnail sắc nét và phóng to chi tiết | [ ] |
| 15 | Xóa tin nhắn đã gửi | Tin nhắn bị xóa đồng bộ tức thời trên cả hai màn hình | [ ] |
| 16 | Kiểm tra giao diện quản trị (Admin) | Tài khoản Admin truy xuất an toàn danh sách quản lý qua endpoint `/admin/all-messages` | [ ] |

### Bước 3: Kiểm tra chất lượng kỹ thuật & Bảo mật mã nguồn
- [ ] Phân tầng rõ rệt: Tầng giao diện (GUI PyQt5), tầng mạng (HTTP/WS), tầng dữ liệu (SQLite/ORM).
- [ ] Bảo mật thông tin: Mật khẩu người dùng được băm an toàn qua thuật toán bcrypt trước khi lưu DB.
- [ ] Cơ chế token: Xác thực phiên người dùng qua chuẩn công nghiệp JWT (JSON Web Token).
- [ ] Không có thông tin nhạy cảm (hardcoded secret keys) viết trực tiếp trong mã nguồn.

### Bước 4: Kiểm tra tính ổn định & Khả năng chịu tải mạng nội bộ
- [ ] Thử nghiệm ngắt kết nối mạng và kết nối lại: Client tự động nhận diện và khôi phục trạng thái.
- [ ] Dò tìm server tự động: Client tìm thấy máy chủ trong mạng LAN qua gói tin UDP Broadcast mà không cần nhập IP thủ công.
- [ ] Không rò rỉ bộ nhớ (memory leaks) khi gửi liên tục nhiều tin nhắn và hình ảnh.

### Bước 5: Hỏi đáp chuyển giao & Ký biên bản nghiệm thu
- Đại diện kỹ thuật giải đáp mọi câu hỏi của Khách hàng về kiến trúc, khả năng nâng cấp lên PostgreSQL và mở rộng hệ thống trong tương lai.
- Hai bên ký kết Biên bản bàn giao và nghiệm thu dự án chính thức.

---

## 4. Tiêu chí đánh giá chất lượng bàn giao (Thang điểm 100)

| Nhóm tiêu chí đánh giá | Trọng số | Điểm đạt được | Đánh giá của Đại diện Khách hàng |
|---|:---:|:---:|---|
| **Chức năng thực tế (UAT Checklist)** | **40%** | | Hoàn thành đầy đủ 16/16 bước kiểm thử thực tế |
| **Kiến trúc hệ thống & Độ bảo mật** | **25%** | | Mô hình phân tầng sạch, mã hóa mật khẩu bcrypt, JWT |
| **Tính đầy đủ của bộ hồ sơ thiết kế** | **20%** | | Trọn bộ 15 tài liệu kỹ thuật chuẩn mực, đồng bộ |
| **Độ ổn định, hiệu năng & Tự động dò tìm** | **15%** | | Tự phát hiện IP trong mạng LAN, phản hồi nhanh dưới 100ms |
| **TỔNG KẾT CHẤT LƯỢNG** | **100%** | | |

### Điều kiện chấp thuận nghiệm thu:
* **Từ 85% trở lên:** **Nghiệm thu toàn diện (Approved)** - Hệ thống đáp ứng xuất sắc mọi yêu cầu kỹ thuật và nghiệp vụ, sẵn sàng đưa vào vận hành thực tế ngay.
* **Từ 70% đến 84%:** **Nghiệm thu có điều kiện (Conditional Acceptance)** - Hệ thống vận hành tốt, đội ngũ kỹ thuật hoàn thiện một số ghi chú nhỏ trong vòng 03 ngày làm việc.
* **Dưới 70%:** **Chưa nghiệm thu (Pending Corrections)** - Cần khắc phục các lỗi phát sinh trước khi tổ chức phiên UAT tiếp theo.

---

## 5. Mẫu Biên bản bàn giao và nghiệm thu dự án (Sign-off)

### **CỘNG HÒA XÃ HỘI CHỦ NGHĨA VIỆT NAM**
**Độc lập – Tự do – Hạnh phúc**

---

### **BIÊN BẢN BÀN GIAO VÀ NGHIỆM THU DỰ ÁN PHẦN MỀM**

* **Tên dự án:** Hệ thống trao đổi thông tin và nhắn tin nội bộ bảo mật (Local Messenger)
* **Thời gian nghiệm thu:** Ngày 23 tháng 01 năm 2026
* **Địa điểm:** Trụ sở / Phòng kỹ thuật của Khách hàng

**ĐẠI DIỆN CÁC BÊN THAM GIA:**

**BÊN A (ĐẠI DIỆN KHÁCH HÀNG / BÊN TIẾP NHẬN):**
* Đơn vị: ____________________________________________________
* Đại diện: __________________________________________________
* Chức vụ: ___________________________________________________

**BÊN B (ĐƠN VỊ PHÁT TRIỂN / BÊN BÀN GIAO):**
* Nhóm phát triển: Đội ngũ Kỹ thuật Dự án Local Messenger
* Đại diện kỹ thuật: Malinevsky Egor Sergeevich
* Chức vụ: Kỹ sư trưởng / Trưởng dự án phát triển

---

**NỘI DUNG NGHIỆM THU VÀ BÀN GIAO:**

1. **Về sản phẩm phần mềm:**
   * Đã bàn giao đầy đủ mã nguồn chương trình máy chủ (Server Backend) và máy khách (Desktop Client).
   * Ứng dụng đã hoàn thành 16/16 bước kiểm thử UAT, hoạt động ổn định trên hạ tầng mạng LAN.
2. **Về hồ sơ tài liệu:**
   * Bàn giao trọn bộ 15 tài liệu kỹ thuật, đặc tả kiến trúc, API và tài liệu hướng dẫn vận hành.
3. **Về công tác đào tạo chuyển giao:**
   * Đã hướng dẫn chi tiết quy trình cài đặt, cấu hình mạng và sao lưu định kỳ cơ sở dữ liệu.

**KẾT LUẬN CHUNG:**
Bên A thống nhất nghiệm thu và tiếp nhận bàn giao toàn bộ sản phẩm cùng hồ sơ kỹ thuật của dự án "Local Messenger" do Bên B bàn giao.

| ĐẠI DIỆN BÊN A (KHÁCH HÀNG) | ĐẠI DIỆN BÊN B (ĐƠN VỊ PHÁT TRIỂN) |
|:---:|:---:|
| *(Ký, ghi rõ họ tên và đóng dấu)* | *(Ký và ghi rõ họ tên)* |
| <br><br><br>________________________________________ | <br><br><br>________________________________________ |
