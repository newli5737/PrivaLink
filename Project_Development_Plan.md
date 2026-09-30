# **KẾ HOẠCH PHÁT TRIỂN VÀ TRIỂN KHAI DỰ ÁN (PROJECT DEVELOPMENT PLAN)**
## **Dự án:** Hệ thống trao đổi thông tin & nhắn tin nội bộ bảo mật (PrivaLink)

---

### 1. Thông tin tổng quan dự án
* **Tên giải pháp:** PrivaLink (Hệ thống nhắn tin và truyền thông mạng LAN nội bộ bảo mật)
* **Khách hàng mục tiêu / Đơn vị thụ hưởng:** Các doanh nghiệp, tổ chức, cơ quan và đơn vị đào tạo có nhu cầu trao đổi dữ liệu nội bộ bảo mật, hoạt động độc lập không phụ thuộc kết nối Internet công cộng.
* **Mô hình kiến trúc:** Client - Server thời gian thực (FastAPI Backend + PyQt5 Desktop Client + WebSocket & SQLite/PostgreSQL).
* **Mục tiêu tài liệu:** Cung cấp lộ trình triển khai chi tiết, các mốc tiến độ chính (milestones), phân bổ nguồn lực và tiêu chuẩn bàn giao để khách hàng và các bên liên quan theo dõi, giám sát toàn diện quá trình hiện thực hóa giải pháp.

---

### 2. Mục tiêu chiến lược của dự án
1. **Bảo mật & Tự chủ dữ liệu:** Triển khai on-premise 100% trong hạ tầng mạng cục bộ, ngăn chặn hoàn toàn nguy cơ rò rỉ dữ liệu ra ngoài Internet.
2. **Hiệu năng & Tức thời:** Đảm bảo thời gian chuyển phát tin nhắn dưới **100ms** qua giao thức WebSocket hai chiều; hỗ trợ đa người dùng kết nối đồng thời ổn định.
3. **Trải nghiệm người dùng mượt mà:** Giao diện Desktop hiện đại viết bằng PyQt5, hỗ trợ chat 1-1, chat nhóm, chia sẻ hình ảnh, xem trước thumbnail và thông báo âm thanh.
4. **Triển khai đơn giản:** Tính năng tự động dò tìm máy chủ (UDP Broadcast Auto-discovery) giúp người dùng kết nối ngay mà không cần cấu hình IP thủ công phức tạp.
5. **Bộ hồ sơ thiết kế chuẩn mực:** Bàn giao bộ tài liệu kỹ thuật hoàn chỉnh gồm 15 văn bản đạt chuẩn công nghiệp, phục vụ công tác nghiệm thu, đào tạo và bảo trì lâu dài.

---

### 3. Phạm vi công việc (Scope of Work)
* **Phân tích nghiệp vụ & Thiết kế:** Xác định bài toán, khảo sát thực tế, xây dựng tài liệu yêu cầu (BRD), đặc tả kỹ thuật (SRS), thiết kế kiến trúc phân tầng (SAD), mô hình thực thể dữ liệu (ERD) và các ca sử dụng (Use Cases).
* **Phát triển Backend Service:** Xây dựng hệ thống máy chủ bằng Python (FastAPI), xác thực JWT, mã hóa mật khẩu bcrypt, quản lý kết nối WebSocket và cơ sở dữ liệu.
* **Phát triển Desktop Client:** Thiết kế giao diện đồ họa PyQt5, module kết nối mạng bất đồng bộ, luồng xử lý nhận diện tin nhắn và hiển thị trạng thái online/offline.
* **Đảm bảo chất lượng (QA & Testing):** Lập kế hoạch kiểm thử, thực thi 23 test case kiểm tra chức năng, kiểm thử tích hợp, kiểm thử chịu tải và lập báo cáo chất lượng.
* **Bàn giao và Nghiệm thu:** Chuyển giao mã nguồn, hướng dẫn cài đặt, quy trình vận hành và ký kết biên bản nghiệm thu (UAT) với khách hàng.

---

### 4. Lộ trình thực hiện chi tiết (4 Giai đoạn / Sprints)

#### Giai đoạn 1: Khảo sát, Thiết kế kiến trúc & Chuẩn bị môi trường
* **Mục tiêu:** Thống nhất yêu cầu nghiệp vụ với khách hàng và hoàn thiện thiết kế kiến trúc nền tảng.
* **Nội dung công việc:**
  1. Phỏng vấn khách hàng, làm rõ các quy định bảo mật và luồng truyền thông nội bộ.
  2. Xây dựng tài liệu Yêu cầu nghiệp vụ (BRD) và Đặc tả kỹ thuật phần mềm (SRS).
  3. Thiết kế kiến trúc tổng thể Client-Server, định nghĩa các luồng dữ liệu REST API và WebSocket.
  4. Thiết kế mô hình cơ sở dữ liệu quan hệ (ERD) gồm các bảng Users, Messages, Attachments.
  5. Thiết lập môi trường phát triển chuẩn hóa, kho mã nguồn và quy chuẩn viết mã (PEP 8).
* **Kết quả bàn giao Giai đoạn 1:**
  * Bộ hồ sơ phân tích thiết kế ban đầu (BRD, SRS, SAD, ERD).
  * Lược đồ CSDL và mã nguồn khởi tạo bảng dữ liệu ban đầu.

---

#### Giai đoạn 2: Xây dựng Máy chủ Dịch vụ (Backend & API Engine)
* **Mục tiêu:** Hoàn thiện toàn bộ các dịch vụ lõi phía Server đảm bảo tốc độ và độ tin cậy cao.
* **Nội dung công việc:**
  1. Khởi tạo dịch vụ FastAPI với cấu trúc module hóa phân tầng (Routers, Services, Repositories).
  2. Hiện thực cơ chế xác thực an toàn: Đăng ký, đăng nhập, cấp phát và xác thực JWT token, mã hóa bcrypt.
  3. Xây dựng các endpoint REST API phục vụ quản lý người dùng, lịch sử tin nhắn, và quyền quản trị.
  4. Xây dựng WebSocket Server trung tâm quản lý kết nối đồng thời và broadcast sự kiện thời gian thực.
  5. Tích hợp cơ chế tự động broadcast địa chỉ IP qua cổng mạng UDP phục vụ tính năng tự dò tìm.
* **Kết quả bàn giao Giai đoạn 2:**
  * Dịch vụ Backend hoàn chỉnh, sẵn sàng chạy nền (Daemon / Background service).
  * Bộ sưu tập API Request và tài liệu tương tác trực tiếp qua Swagger UI (`/docs`).

---

#### Giai đoạn 3: Phát triển Ứng dụng Phía Khách (Desktop Client GUI)
* **Mục tiêu:** Xây dựng ứng dụng người dùng trực quan, thân thiện và phản hồi nhanh.
* **Nội dung công việc:**
  1. Thiết kế hệ thống màn hình: Đăng nhập/Đăng ký, Danh bạ người dùng, Cửa sổ chat riêng, Chat nhóm.
  2. Xây dựng Network Manager quản lý các yêu cầu HTTP và duy trì kết nối WebSocket liên tục.
  3. Hiện thực cơ chế tự động dò tìm IP máy chủ trong mạng LAN qua cổng UDP.
  4. Tích hợp tính năng gửi ảnh: Mã hóa Base64, nén dữ liệu, tạo ảnh thu nhỏ (thumbnail preview).
  5. Xử lý logic trạng thái người dùng (Online/Offline) hiển thị tức thời qua đèn báo hiệu.
* **Kết quả bàn giao Giai đoạn 3:**
  * Bộ cài đặt / Gói thực thi Desktop Client chạy trên Windows và Linux.
  * Hoàn thành kịch bản kết nối liên thông Client - Server thành công.

---

#### Giai đoạn 4: Kiểm thử, Nghiệm thu & Chuyển giao Khách hàng
* **Mục tiêu:** Kiểm chứng chất lượng toàn diện và chính thức bàn giao đưa hệ thống vào vận hành.
* **Nội dung công việc:**
  1. Thực thi toàn bộ 23 ca kiểm thử chức năng, tích hợp và kiểm thử giao diện người dùng.
  2. Thực hiện kiểm thử chịu tải với kịch bản đa kết nối đồng thời trên mạng LAN.
  3. Biên soạn bộ tài liệu vận hành: Hướng dẫn người dùng cuối, Hướng dẫn cài đặt & bảo trì máy chủ.
  4. Thực hiện quy trình kiểm thử chấp nhận người dùng (UAT) với khách hàng theo checklist 16 bước.
  5. Ký kết biên bản nghiệm thu bàn giao chính thức.
* **Kết quả bàn giao Giai đoạn 4:**
  * Báo cáo kết quả kiểm thử (Test Report) đạt tỷ lệ thành công trên 88%.
  * Ma trận truy vết yêu cầu (RTM) đạt độ phủ chức năng 92%.
  * Biên bản nghiệm thu và bàn giao dự án hoàn tất.

---

### 5. Danh mục hồ sơ bàn giao cho Khách hàng
1. **Bộ mã nguồn dự án (Source Code):**
   * Mã nguồn Backend Server (Python / FastAPI).
   * Mã nguồn Desktop Client (Python / PyQt5).
   * File phụ thuộc thư viện (`requirements.txt`) và script khởi động nhanh (`start.sh` / `start.bat`).
2. **Bộ hồ sơ tài liệu thiết kế & kỹ thuật (15 tài liệu):**
   * Yêu cầu nghiệp vụ, Tài liệu kiến trúc, Đặc tả kỹ thuật SRS.
   * Câu chuyện người dùng, Kịch bản Use Cases, Ma trận truy vết RTM.
   * Kế hoạch kiểm thử, Báo cáo kiểm thử, Báo cáo phân tích hệ thống.
   * Sách hướng dẫn sử dụng, Hướng dẫn cài đặt & triển khai, Hướng dẫn bảo trì hệ thống.
   * Đặc tả API chi tiết, Từ điển thuật ngữ kỹ thuật, Kế hoạch nghiệm thu UAT.
3. **Kịch bản UAT & Biên bản nghiệm thu dự án:** Bản cam kết chất lượng và biên bản ký nhận bàn giao.

---

### 6. Đại diện phê duyệt và bàn giao

| Đại diện Khách hàng / Đơn vị tiếp nhận | Đại diện Ban Quản trị Dự án / Kỹ thuật |
|:---:|:---:|
| *(Ký và ghi rõ họ tên)* | *(Ký và ghi rõ họ tên)* |
| <br><br>____________________________________ | <br><br>____________________________________ |
| **Ngày xác nhận:** ____ / ____ / 2026 | **Ngày hoàn tất:** 19 / 01 / 2026 |
