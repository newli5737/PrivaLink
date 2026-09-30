# Thuật ngữ (Glossary)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản tài liệu:** 1.2  
**Năm:** 2026  
**Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống  
**Trạng thái:** Bảng thuật ngữ kỹ thuật chuẩn mực (Đối soát đồng bộ toàn hệ thống)

---

## 1. Thuật ngữ kiến trúc và phát triển phần mềm

### Ngăn xếp công nghệ (Tech Stack)
**Định nghĩa:** Tập hợp các công nghệ, framework, thư viện và công cụ được sử dụng để xây dựng và phát triển phần mềm.  
**Ngữ cảnh trong dự án:** Dự án sử dụng tech stack gồm: FastAPI (backend), PyQt5 (frontend), SQLite (cơ sở dữ liệu), JWT (xác thực người dùng).

### Mạng cục bộ (LAN — Local Area Network)
**Định nghĩa:** Mạng máy tính giới hạn kết nối các thiết bị trong phạm vi một tòa nhà, phòng ban hoặc cơ sở giáo dục.  
**Ngữ cảnh trong dự án:** Ứng dụng hoạt động hoàn toàn trong mạng LAN nội bộ của doanh nghiệp, cơ quan hoặc tổ chức, không yêu cầu kết nối Internet ra bên ngoài.

### Kiến trúc máy khách - máy chủ (Client-Server Architecture)
**Định nghĩa:** Mô hình tương tác trong đó các ứng dụng client gửi yêu cầu (requests) đến một server trung tâm xử lý dữ liệu và phản hồi kết quả.  
**Ngữ cảnh trong dự án:** Hệ thống gồm máy chủ (FastAPI) và các máy khách (PyQt5) giao tiếp qua HTTP và WebSocket.

### REST API (Representational State Transfer Application Programming Interface)
**Định nghĩa:** Bộ quy tắc và quy chuẩn để xây dựng các dịch vụ web sử dụng các phương thức HTTP chuẩn (GET, POST, DELETE, v.v.).  
**Ngữ cảnh trong dự án:** Server cung cấp REST API cho việc đăng ký, đăng nhập, gửi tin nhắn, lấy lịch sử chat và các thao tác quản trị.

### WebSocket
**Định nghĩa:** Giao thức truyền thông hai chiều qua kết nối TCP duy nhất, cho phép trao đổi dữ liệu thời gian thực giữa client và server.  
**Ngữ cảnh trong dự án:** Dùng để gửi tin nhắn tức thời và thông báo xóa tin nhắn mà không cần client phải liên tục thăm dò (polling) server.

### JWT (JSON Web Token)
**Định nghĩa:** Chuẩn mở tạo token xác thực chứa dữ liệu mã hóa dưới định dạng JSON.  
**Ngữ cảnh trong dự án:** Dùng để xác thực người dùng. Token được gửi trong HTTP Header của các request và có thời hạn sống 30 phút.

### Base64
**Định nghĩa:** Phương pháp mã hóa dữ liệu nhị phân (binary) thành chuỗi ký tự ASCII sử dụng bảng chữ cái 64 ký tự.  
**Ngữ cảnh trong dự án:** Hình ảnh trước khi gửi được mã hóa thành Base64 để truyền tải qua JSON và lưu trữ trực tiếp trong cơ sở dữ liệu.

### FastAPI
**Định nghĩa:** Web framework hiện đại, hiệu năng cao cho Python dùng để xây dựng API với tính năng tự động sinh tài liệu Swagger/OpenAPI.  
**Ngữ cảnh trong dự án:** Dùng để phát triển backend của hệ thống nhắn tin.

### PyQt5
**Định nghĩa:** Bộ thư viện Python để xây dựng giao diện người dùng đồ họa (GUI) dựa trên framework Qt của C++.  
**Ngữ cảnh trong dự án:** Dùng để phát triển ứng dụng client đa nền tảng cho người dùng.

### Uvicorn
**Định nghĩa:** Máy chủ web ASGI nhanh cho Python, dùng để chạy các ứng dụng web không đồng bộ.  
**Ngữ cảnh trong dự án:** Dùng để chạy và phục vụ ứng dụng FastAPI.

### Pydantic
**Định nghĩa:** Thư viện Python dùng để kiểm thực (validation) dữ liệu và quản lý cài đặt thông qua Python type annotations.  
**Ngữ cảnh trong dự án:** Dùng để định nghĩa các schema và kiểm tra tính hợp lệ của dữ liệu trong API.

---

## 2. Thuật ngữ cơ sở dữ liệu

### SQLite
**Định nghĩa:** Hệ quản trị cơ sở dữ liệu quan hệ dạng nhúng, lưu trữ toàn bộ dữ liệu vào một file duy nhất trên đĩa.  
**Ngữ cảnh trong dự án:** Dùng làm kho lưu trữ chính cho người dùng, tin nhắn và siêu dữ liệu mà không cần cài server DB riêng biệt.

### CRUD (Create, Read, Update, Delete)
**Định nghĩa:** Bốn thao tác cơ bản được thực hiện trên dữ liệu trong cơ sở dữ liệu (Tạo, Đọc, Cập nhật, Xóa).  
**Ngữ cảnh trong dự án:** Hệ thống triển khai CRUD cho tin nhắn (tạo, đọc, xóa) và người dùng (tạo, đọc).

### Lược đồ ER (ER-diagram - Entity–Relationship Diagram)
**Định nghĩa:** Sơ đồ biểu diễn trực quan các thực thể (bảng) và mối quan hệ giữa chúng trong cơ sở dữ liệu.  
**Ngữ cảnh trong dự án:** Dùng trong tài liệu để mô tả cấu trúc của 2 bảng `users` và `messages`.

### CSDL (Cơ sở dữ liệu - Database)
**Định nghĩa:** Tập hợp dữ liệu có tổ chức được lưu trữ dưới dạng có cấu trúc.  
**Ngữ cảnh trong dự án:** Dự án dùng file CSDL SQLite `messenger.db` gồm các bảng users và messages.

### SQLAlchemy
**Định nghĩa:** Thư viện ORM (Object-Relational Mapping) mạnh mẽ cho Python giúp ánh xạ bảng CSDL thành các đối tượng class.  
**Ngữ cảnh trong dự án:** Dùng để thao tác và truy vấn CSDL SQLite một cách an toàn và tiện lợi.

### Tấn công tiêm SQL (SQL Injection)
**Định nghĩa:** Kỹ thuật tấn công chèn các câu lệnh SQL độc hại vào các trường nhập liệu để thao túng CSDL.  
**Ngữ cảnh trong dự án:** Được phòng chống triệt để nhờ việc sử dụng ORM SQLAlchemy với các truy vấn tham số hóa (parameterized queries).

---

## 3. Thuật ngữ giao diện và tương tác người dùng

### Widget (Thành phần điều khiển giao diện)
**Định nghĩa:** Phần tử trong giao diện đồ họa như nút bấm, ô nhập liệu, danh sách cuộn, v.v.  
**Ngữ cảnh trong dự án:** Các widget chính gồm `ChatWidget` (khung chat), `LoginDialog` (cửa sổ đăng nhập), `MainWindow` (cửa sổ chính).

### Thẻ / Tab
**Định nghĩa:** Phần tử giao diện cho phép chuyển đổi qua lại giữa nhiều khung tài liệu hoặc hội thoại trong cùng một cửa sổ.  
**Ngữ cảnh trong dự án:** Người dùng có thể mở nhiều cuộc trò chuyện cùng lúc, mỗi cuộc trò chuyện nằm trong một tab riêng biệt.

### Trạng thái trực tuyến (Online Status)
**Định nghĩa:** Chỉ báo thể hiện người dùng hiện có đang kết nối vào hệ thống hay không.  
**Ngữ cảnh trong dự án:** Hiển thị bằng biểu tượng [Online] (online) hoặc [Offline] (offline) cạnh tên người dùng trong danh bạ.

### GUI (Graphical User Interface)
**Định nghĩa:** Giao diện người dùng đồ họa, cho phép tương tác với chương trình qua các thành phần hình ảnh thay vì dòng lệnh.  
**Ngữ cảnh trong dự án:** Ứng dụng sở hữu GUI trực quan được xây dựng trên nền tảng PyQt5.

### UI (User Interface)
**Định nghĩa:** Giao diện người dùng — phần nhìn thấy và tương tác trực tiếp của ứng dụng.  
**Ngữ cảnh trong dự án:** Thiết kế thân thiện, bố cục rõ ràng với danh bạ bên trái và khung chat bên phải.

### UX (User Experience)
**Định nghĩa:** Trải nghiệm người dùng — cảm nhận tổng thể và mức độ dễ dàng, thuận tiện khi sử dụng phần mềm.  
**Ngữ cảnh trong dự án:** Tối ưu hóa để người dùng không cần kỹ năng chuyên sâu cũng có thể cài đặt và gửi tin nhắn tức thì.

### Chat Widget
**Định nghĩa:** Thành phần giao diện hiển thị lịch sử trao đổi tin nhắn và ô soạn thảo, gửi nội dung.  
**Ngữ cảnh trong dự án:** Mỗi tab hội thoại được mở là một phiên bản (instance) của ChatWidget.

---

## 4. Từ viết tắt và giải nghĩa

### API (Application Programming Interface)
**Giải nghĩa:** Giao diện lập trình ứng dụng.  
**Ngữ cảnh trong dự án:** Tập hợp các hàm và endpoint mà server cung cấp để ứng dụng client gọi đến.

### HTTP (HyperText Transfer Protocol)
**Giải nghĩa:** Giao thức truyền tải siêu văn bản.  
**Ngữ cảnh trong dự án:** Giao thức mạng nền tảng để trao đổi dữ liệu REST giữa client và server.

### TCP/IP (Transmission Control Protocol / Internet Protocol)
**Giải nghĩa:** Bộ giao thức điều khiển truyền vận và liên mạng.  
**Ngữ cảnh trong dự án:** Giao thức mạng cơ sở làm nền tảng cho HTTP và WebSocket vận hành.

### ID (Identifier)
**Giải nghĩa:** Mã định danh duy nhất.  
**Ngữ cảnh trong dự án:** Số nguyên duy nhất gán cho mỗi tài khoản người dùng và mỗi tin nhắn trong CSDL.

### SW (Software)
**Giải nghĩa:** Phần mềm.  
**Ngữ cảnh trong dự án:** Phần mềm Local Messenger dùng để nhắn tin trao đổi nội bộ.

### HW (Hardware)
**Giải nghĩa:** Phần cứng máy tính.  
**Ngữ cảnh trong dự án:** Máy chủ, máy trạm và các thiết bị mạng (Switch, Router, dây cáp) cần thiết để chạy hệ thống.

### MTBF (Mean Time Between Failures)
**Giải nghĩa:** Thời gian trung bình giữa các lần phát sinh lỗi hỏng hóc.  
**Ngữ cảnh trong dự án:** Chỉ số đo lường độ tin cậy và sự ổn định của hệ thống server.

### MTTR (Mean Time To Repair)
**Giải nghĩa:** Thời gian trung bình để khắc phục sự cố và phục hồi hệ thống.  
**Ngữ cảnh trong dự án:** Chỉ số đo lường khả năng bảo trì và khôi phục khi có lỗi phát sinh.

---

## 5. Các thuật ngữ và quy ước đặc thù của hệ thống

### “Xóa tin nhắn theo ID”
**Định nghĩa:** Cơ chế xóa tin nhắn bằng cách nhập mã số định danh ID cụ thể của tin nhắn đó.  
**Ngữ cảnh trong dự án:** Để xóa tin nhắn của mình, người dùng xem ID hiển thị ở dưới tin nhắn và nhập vào ô xóa để xác nhận lệnh DELETE.

### “Người dùng đầu tiên là Quản trị viên”
**Định nghĩa:** Quy tắc nghiệp vụ tự động gán quyền Administrator cho tài khoản đăng ký đầu tiên trong hệ thống.  
**Ngữ cảnh trong dự án:** Tài khoản này có quyền xem toàn bộ tin nhắn và danh sách tất cả tài khoản thông qua API quản trị đặc biệt.

### “Thông báo Real-time”
**Định nghĩa:** Khả năng chuyển giao các sự kiện (tin nhắn mới, thông báo xóa tin) ngay lập tức mà không có độ trễ nhận thấy được.  
**Ngữ cảnh trong dự án:** Được hỗ trợ thông qua kênh kết nối liên tục WebSocket giữa server và client.

### “File ảnh tạm thời (Temporary Image Files)”
**Định nghĩa:** Các file ảnh được client tạo ra tạm thời trong thư mục máy tính để hiển thị lên khung chat khi giải mã từ Base64.  
**Ngữ cảnh trong dự án:** Tự động được dọn dẹp và xóa đi khi ứng dụng client đóng lại.

### “Cơ chế Ping-Pong” (ping-pong heartbeat)
**Định nghĩa:** Cơ chế duy trì kết nối WebSocket bằng cách gửi định kỳ các gói tin kiểm tra kết nối rỗng.  
**Ngữ cảnh trong dự án:** Client gửi `ping`, server phản hồi `pong` nhằm ngăn ngừa việc rớt mạng do timeout trên thiết bị mạng trung gian.

### "Độ rộng cố định 200px"
**Định nghĩa:** Quy định giới hạn kích thước hiển thị ảnh trong cửa sổ chat.  
**Ngữ cảnh trong dự án:** Mọi hình ảnh gửi đi đều được tự động co lại hiển thị với bề ngang 200 pixel để không làm vỡ bố cục chat.

### "Danh bạ (Contact List)"
**Định nghĩa:** Bảng điều khiển nằm bên trái cửa sổ chính hiển thị danh sách tất cả các tài khoản người dùng trong hệ thống.  
**Ngữ cảnh trong dự án:** Hiển thị tên tài khoản, thời gian hoạt động gần nhất và trạng thái trực tuyến.

### "Bộ định tuyến (Routers)"
**Định nghĩa:** Các nhóm endpoints API được phân chia theo module nghiệp vụ trong FastAPI.  
**Ngữ cảnh trong dự án:** Server tổ chức thành các file router riêng biệt: `auth.py`, `messages.py`, `users.py`, `admin.py`.

---

## 6. Thuật ngữ kỹ thuật và điều kiện ràng buộc

### Kiến trúc Monolith (Đơn khối)
**Định nghĩa:** Kiến trúc trong đó toàn bộ các chức năng của hệ thống được đóng gói và vận hành trong một ứng dụng duy nhất.  
**Ngữ cảnh trong dự án:** Phần backend được viết thành một ứng dụng FastAPI tập trung, không phân tách microservices phức tạp.

### Địa chỉ IP tĩnh (Static IP Address)
**Định nghĩa:** Địa chỉ mạng cố định, không thay đổi được gán cho một thiết bị trong mạng LAN.  
**Ngữ cảnh trong dự án:** Máy chủ cần được cấu hình IP tĩnh để các máy client có thể kết nối ổn định lâu dài.

### Cổng mạng 8000 (Port 8000)
**Định nghĩa:** Cổng dịch vụ mạng mặc định mà server FastAPI lắng nghe.  
**Ngữ cảnh trong dự án:** Client kết nối vào server qua đường dẫn `http://<IP_Server>:8000`.

### Bảo mật cấp độ mạng (Perimeter / Network Security)
**Định nghĩa:** Cách tiếp cận an ninh dựa vào việc cô lập hoàn toàn hệ thống bên trong vùng mạng tin cậy.  
**Ngữ cảnh trong dự án:** Dữ liệu tin nhắn trong mạng LAN nội bộ trường học không sử dụng mã hóa đầu cuối E2EE vì dựa vào tính cô lập vật lý của mạng.

### Bộ định thời cập nhật (Update Timer)
**Định nghĩa:** Cơ chế thực thi tác vụ theo chu kỳ thời gian định sẵn.  
**Ngữ cảnh trong dự án:** Danh sách liên lạc và trạng thái người dùng được tự động làm mới mỗi 10 giây một lần.

### Môi trường ảo (Virtual Environment - venv)
**Định nghĩa:** Môi trường độc lập trên máy trạm dùng để cài đặt các gói phụ thuộc Python mà không làm ảnh hưởng đến thư viện hệ thống chung.  
**Ngữ cảnh trong dự án:** Khuyến nghị tạo `venv` trước khi cài đặt dependencies của dự án.

### Requirements.txt
**Định nghĩa:** Tệp danh sách các thư viện Python cùng phiên bản cụ thể cần cài đặt để chạy dự án.  
**Ngữ cảnh trong dự án:** Chứa FastAPI, Uvicorn, SQLAlchemy, PyQt5, WebSockets, Passlib, Python-Jose,...

---

## 7. Thuật ngữ phương pháp luận và quản lý dự án

### Dự án phần mềm nội bộ (Internal Enterprise Project)
**Định nghĩa:** Sản phẩm phần mềm được thiết kế và triển khai phục vụ nhu cầu trao đổi thông tin, giao tiếp nội bộ cho cơ quan, tổ chức hoặc doanh nghiệp trong phạm vi hạ tầng mạng cục bộ (On-premise LAN).  
**Ngữ cảnh trong dự án:** Toàn bộ hệ thống "Local Messenger" được xây dựng nhằm cung cấp giải pháp nhắn tin an toàn, độc lập không phụ thuộc vào Internet công cộng.

### Hiện thực thực tế (Actual Implementation)
**Định nghĩa:** Phần mã nguồn thực sự được lập trình và hoạt động, phân biệt với các ý tưởng lý thuyết hoặc yêu cầu trên giấy.  
**Ngữ cảnh trong dự án:** Toàn bộ tài liệu được đối chiếu để mô tả chính xác 100% mã nguồn thực tế đã viết.

### Nợ kỹ thuật (Technical Debt)
**Định nghĩa:** Những giải pháp thiết kế tạm thời, tiện lợi trước mắt nhưng có thể gây khó khăn cho việc mở rộng lâu dài.  
**Ngữ cảnh trong dự án:** Ví dụ như lưu trữ ảnh trực tiếp bằng chuỗi Base64 trong database SQLite thay vì lưu file tĩnh trên ổ đĩa.

### Phân tích SWOT (SWOT Analysis)
**Định nghĩa:** Phương pháp phân tích chiến lược đánh giá Điểm mạnh (Strengths), Điểm yếu (Weaknesses), Cơ hội (Opportunities), và Thách thức (Threats).  
**Ngữ cảnh trong dự án:** Được áp dụng trong tài liệu Phân tích hệ thống.

### Use Case (Trường hợp sử dụng)
**Định nghĩa:** Mô tả chuỗi tương tác giữa người dùng (Actor) và hệ thống nhằm đạt được một mục tiêu cụ thể.  
**Ngữ cảnh trong dự án:** Định nghĩa 10 ca sử dụng chính (Đăng ký, Đăng nhập, Gửi tin nhắn, Gửi ảnh, Xóa tin nhắn, Xem online,...).

### User Story (Câu chuyện người dùng)
**Định nghĩa:** Bản mô tả ngắn gọn về tính năng phần mềm dưới góc nhìn và kỳ vọng của người dùng cuối.  
**Ngữ cảnh trong dự án:** Dự án bao gồm 17 user stories với cấu trúc "Là [vai trò], tôi muốn [hành động] để [lợi ích]".

---

## 8. Thuật ngữ kiểm thử và chất lượng phần mềm

### Ca kiểm thử (Test Case)
**Định nghĩa:** Tập hợp các điều kiện tiên quyết, dữ liệu đầu vào và các bước thực hiện cùng kết quả mong đợi để kiểm chứng một chức năng.  
**Ngữ cảnh trong dự án:** Tài liệu kế hoạch kiểm thử xây dựng 23 test case chi tiết.

### Tiêu chí chấp nhận (Acceptance Criteria)
**Định nghĩa:** Các điều kiện bắt buộc mà một tính năng phải thỏa mãn để được khách hàng hoặc người kiểm thử chấp nhận hoàn thành.  
**Ngữ cảnh trong dự án:** Được quy định cụ thể cho từng câu chuyện người dùng.

### Kiểm thử chức năng (Functional Testing)
**Định nghĩa:** Quá trình kiểm tra xem hệ thống có đáp ứng đúng các yêu cầu chức năng đã đề ra hay không.  
**Ngữ cảnh trong dự án:** Kiểm tra việc gửi tin nhắn, xác thực token, cập nhật danh bạ.

### Kiểm thử tải (Load / Performance Testing)
**Định nghĩa:** Đánh giá khả năng đáp ứng và tính ổn định của hệ thống dưới áp lực nhiều yêu cầu đồng thời.  
**Ngữ cảnh trong dự án:** Kiểm thử khả năng phục vụ trên 20 người dùng đồng thời trong môi trường phòng lab.

### Kiểm thử hồi quy (Regression Testing)
**Định nghĩa:** Việc kiểm tra lại các chức năng cũ sau khi sửa lỗi hoặc nâng cấp mã nguồn để đảm bảo không làm phát sinh lỗi mới.  
**Ngữ cảnh trong dự án:** Được thực hiện sau khi sửa lỗi hiển thị ảnh và lỗi xác thực WebSocket.

### Lỗi / Khiếm khuyết (Defect / Bug)
**Định nghĩa:** Sự sai lệch giữa hành vi thực tế của chương trình so với yêu cầu hoặc kỳ vọng kỹ thuật.  
**Ngữ cảnh trong dự án:** Phát hiện và khắc phục 3 lỗi trong đợt kiểm thử chính thức.

---

## 9. Thuật ngữ quản lý và yêu cầu nghiệp vụ

### Yêu cầu nghiệp vụ (Business Requirements)
**Định nghĩa:** Các nhu cầu và mục tiêu cấp cao của các bên liên quan mà hệ thống phần mềm cần giải quyết.  
**Ngữ cảnh trong dự án:** Được trình bày trong tài liệu Yêu cầu nghiệp vụ.

### Nhóm đối tượng người dùng (Target Audience)
**Định nghĩa:** Nhóm người dùng dự kiến sẽ sử dụng sản phẩm phần mềm.  
**Ngữ cảnh trong dự án:** Toàn thể cán bộ nhân viên, các phòng ban và người quản trị trong cơ quan, tổ chức hoặc doanh nghiệp.

### Tiêu chí thành công (Success Criteria)
**Định nghĩa:** Các chỉ số đo lường định lượng và định tính nhằm xác định dự án đã hoàn thành mục tiêu đề ra.  
**Ngữ cảnh trong dự án:** Bao gồm các tiêu chuẩn kỹ thuật (độ trễ <100ms, tỷ lệ thành công kiểm thử cao) và sự hài lòng của khách hàng.

### Ma trận truy vết yêu cầu (RTM - Requirements Traceability Matrix)
**Định nghĩa:** Bảng đối chiếu giúp liên kết từng yêu cầu nghiệp vụ với thiết kế kiến trúc, mã nguồn triển khai và kịch bản kiểm thử tương ứng.  
**Ngữ cảnh trong dự án:** Đảm bảo 100% các yêu cầu từ ban đầu đều được hiện thực và kiểm thử đầy đủ.

### Quyết định kiến trúc (ADR - Architecture Decision Record)
**Định nghĩa:** Tài liệu ngắn gọn ghi lại một quyết định kiến trúc quan trọng kèm theo bối cảnh, lý do và hệ quả của nó.  
**Ngữ cảnh trong dự án:** Ghi nhận lý do chọn FastAPI thay vì Flask/Django, chọn SQLite thay vì PostgreSQL.

---

## 10. Thuật ngữ an toàn và bảo mật thông tin

### Bcrypt
**Định nghĩa:** Thuật toán băm mật khẩu thích ứng có tích hợp salt ngẫu nhiên, giúp chống lại các cuộc tấn công vét cạn (brute-force) và bảng băm cầu vồng (rainbow table).  
**Ngữ cảnh trong dự án:** Dùng để mã hóa một chiều mật khẩu người dùng trước khi lưu vào CSDL qua `passlib.context.CryptContext`.

### XSS (Cross-Site Scripting)
**Định nghĩa:** Lỗ hổng cho phép kẻ tấn công chèn mã kịch bản độc hại vào giao diện của người dùng khác.  
**Ngữ cảnh trong dự án:** Nội dung tin nhắn trong PyQt5 được hiển thị an toàn dưới dạng văn bản thuần (plain text), không biên dịch mã HTML.

### Giới hạn tần suất gọi (Rate Limiting)
**Định nghĩa:** Kỹ thuật hạn chế số lượng yêu cầu API mà một client có thể gửi trong một khoảng thời gian nhất định.  
**Ngữ cảnh trong dự án:** Chưa được triển khai trong phiên bản học tập hiện tại.

### CORS (Cross-Origin Resource Sharing)
**Định nghĩa:** Cơ chế bảo mật của trình duyệt kiểm soát việc chia sẻ tài nguyên giữa các domain khác nhau.  
**Ngữ cảnh trong dự án:** Được cấu hình `allow_origins=["*"]` trong FastAPI để dễ dàng phát triển và kiểm thử trong mạng nội bộ.

---

## 11. Thuật ngữ vận hành và triển khai

### Giám sát hệ thống (Monitoring)
**Định nghĩa:** Quá trình theo dõi liên tục trạng thái sức khỏe, hiệu năng và tài nguyên của hệ thống khi đang hoạt động.  
**Ngữ cảnh trong dự án:** Theo dõi mức chiếm dụng CPU, RAM, dung lượng file CSDL SQLite và nhật ký log của server.

### Sao lưu dự phòng (Backup)
**Định nghĩa:** Hoạt động sao chép định kỳ dữ liệu sang vị trí lưu trữ an toàn nhằm phục vụ việc phục hồi khi xảy ra sự cố.  
**Ngữ cảnh trong dự án:** Thực hiện sao lưu định kỳ file CSDL `messenger.db` bằng script tự động.

### Triển khai (Deployment)
**Định nghĩa:** Quy trình cài đặt, cấu hình và khởi chạy phần mềm lên môi trường máy chủ và máy trạm mục tiêu.  
**Ngữ cảnh trong dự án:** Hướng dẫn từng bước trong tài liệu Cài đặt và Triển khai.

### Khắc phục sự cố (Troubleshooting)
**Định nghĩa:** Quá trình chẩn đoán, khoanh vùng và xử lý các lỗi kỹ thuật phát sinh trong quá trình vận hành hệ thống.  
**Ngữ cảnh trong dự án:** Tài liệu hướng dẫn liệt kê 10 tình huống lỗi tiêu biểu kèm giải pháp xử lý.

### Kiểm tra sức khỏe (Health Check)
**Định nghĩa:** Endpoint hoặc lệnh kiểm tra nhanh trạng thái hoạt động bình thường của dịch vụ.  
**Ngữ cảnh trong dự án:** Endpoint `GET /` và `GET /docs` dùng để kiểm tra server có đang hoạt động tốt hay không.

---

## 12. Các thuật ngữ từ tài liệu báo cáo và công cụ kiểm thử

### Bộ sưu tập Postman (Postman Collection)
**Định nghĩa:** Tập hợp các yêu cầu HTTP API được cấu hình sẵn cùng tham số mẫu, dùng để kiểm thử tự động hoặc thủ công các endpoints.  
**Ngữ cảnh trong dự án:** Cung cấp bộ test API đầy đủ cho việc xác thực và gửi nhận tin nhắn.

### Swagger UI
**Định nghĩa:** Giao diện web tương tác trực quan cho phép xem và trực tiếp gửi thử nghiệm các request đến REST API dựa trên chuẩn OpenAPI.  
**Ngữ cảnh trong dự án:** Tự động khả dụng tại địa chỉ `http://localhost:8000/docs` khi server chạy.

### JMeter
**Định nghĩa:** Công cụ mã nguồn mở phổ biến dùng để kiểm thử hiệu năng và tạo tải giả lập trên máy chủ.  
**Ngữ cảnh trong dự án:** Sử dụng để đo đạc thời gian đáp ứng và độ ổn định của server khi có nhiều kết nối đồng thời.

### Selenium
**Định nghĩa:** Framework tự động hóa thao tác kiểm thử giao diện ứng dụng.  
**Ngữ cảnh trong dự án:** Sử dụng bổ trợ trong việc kiểm tra tự động các kịch bản client.

### Độ phủ mã nguồn (Code Coverage)
**Định nghĩa:** Tỷ lệ phần trăm dòng lệnh hoặc nhánh mã nguồn được thực thi qua các bài kiểm thử tự động.  
**Ngữ cảnh trong dự án:** Dự án đạt mức 78% độ bao phủ mã nguồn trong các đợt kiểm thử.

### Độ sẵn sàng (Availability)
**Định nghĩa:** Tỷ lệ thời gian hệ thống hoạt động bình thường và sẵn sàng phục vụ người dùng trong một khoảng thời gian đánh giá.  
**Ngữ cảnh trong dự án:** Đạt mức 99.7% độ sẵn sàng trong giai đoạn thử nghiệm vận hành liên tục.

### Mật độ lỗi (Defect Density)
**Định nghĩa:** Số lượng lỗi phát hiện được trên một đơn vị quy mô mã nguồn (thường là trên 100 hoặc 1.000 dòng code).  
**Ngữ cảnh trong dự án:** Dự án ghi nhận mật độ 0.12 lỗi trên 100 dòng code.

---

## Bảng thống kê thuật ngữ

| Danh mục | Số lượng thuật ngữ | Ví dụ tiêu biểu |
|-----------|-------------------|-----------------|
| Kiến trúc và phát triển phần mềm | 11 | Ngăn xếp công nghệ, FastAPI, PyQt5, Uvicorn, Pydantic |
| Cơ sở dữ liệu | 6 | SQLite, Lược đồ ER, CRUD, SQLAlchemy |
| Giao diện và tương tác | 7 | Widget, Tab, GUI, UI, UX, Chat Widget |
| Từ viết tắt | 8 | API, HTTP, TCP/IP, MTBF, MTTR |
| Biểu thức đặc thù hệ thống | 8 | "Xóa tin nhắn theo ID", "Thông báo Real-time", "Bộ định tuyến" |
| Thuật ngữ kỹ thuật & ràng buộc | 7 | Kiến trúc Monolith, Môi trường ảo, IP tĩnh |
| Quản lý dự án & học tập | 6 | Dự án học tập, Phân tích SWOT, User Story |
| Kiểm thử và chất lượng | 7 | Ca kiểm thử, Kiểm thử tải, Độ phủ mã nguồn |
| Quản lý & yêu cầu nghiệp vụ | 5 | Yêu cầu nghiệp vụ, Ma trận truy vết, ADR |
| An toàn và bảo mật | 4 | Bcrypt, XSS, Rate Limiting, CORS |
| Vận hành và triển khai | 5 | Giám sát, Sao lưu, Kiểm tra sức khỏe |
| Công cụ báo cáo & kiểm thử | 7 | Postman collection, Swagger UI, JMeter, Selenium |
| **Tổng cộng** | **81 thuật ngữ** | |

---

**Cập nhật trong phiên bản 1.2:**
1. Bổ sung các thuật ngữ từ tài liệu mới (API, Báo cáo kiểm thử, Hướng dẫn vận hành).
2. Mở rộng các phần về an toàn bảo mật và kiểm thử phần mềm.
3. Thêm các thuật ngữ giám sát và bảo trì hệ thống.
4. Chuẩn hóa ngữ cảnh áp dụng thực tế trong mã nguồn của dự án.
5. Bổ sung các công cụ kiểm thử tiêu chuẩn (JMeter, Selenium, Postman).

**Phiên bản tài liệu:** 1.2  
**Năm:** 2026  

*Bảng tra cứu thuật ngữ được tổng hợp dựa trên phân tích toàn diện hệ thống tài liệu dự án "Local Messenger". Mọi thuật ngữ đều được sử dụng đồng bộ và nhất quán trong toàn bộ tài liệu hướng dẫn, đề bài kỹ thuật, phân tích hệ thống, đặc tả API và các báo cáo kiểm thử.*