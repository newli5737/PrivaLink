**Đề bài:**
```
Cung cấp danh mục tất cả các loại tài liệu dự án được xây dựng trong suốt vòng đời phát triển phần mềm ở tất cả các giai đoạn, không dưới 100 loại tài liệu. Thể hiện chúng theo cấu trúc phân cấp rõ ràng cho từng loại tài liệu, nêu rõ các nguồn tài liệu gốc (các loại tài liệu khác) cần thiết để phát triển loại tài liệu đó. Trình bày toàn bộ danh mục dưới dạng bảng. Tối thiểu 100 loại tài liệu.
```
Dưới đây là bảng phân cấp đầy đủ và chi tiết các loại tài liệu dự án phần mềm (100+ hạng mục) kèm theo tài liệu nguồn và phân tích hiện trạng đối với dự án này:

---

## **Bảng phân loại các loại tài liệu dự án phần mềm**

| STT | Phân loại | Loại tài liệu | Mục đích sử dụng | Tài liệu nguồn để xây dựng | Hiện trạng trong dự án này |
|:---:|:---|:---|:---|:---|:---|
| **1. Tài liệu chiến lược và khởi tạo** |
| 1.1 | Khởi tạo | Business Case (Hồ sơ kinh doanh) | Biện minh cho tính cần thiết của dự án, ROI, mục tiêu | Phân tích thị trường, yêu cầu của các bên liên quan | Dự án học tập, không có mục tiêu kinh doanh thương mại |
| 1.2 | Khởi tạo | Project Charter (Hiến chương dự án) | Phê duyệt chính thức dự án, chỉ định quyền hạn | Business Case, yêu cầu của nhà tài trợ | Không có nhà tài trợ/khách hàng doanh nghiệp chính thức |
| 1.3 | Khởi tạo | Feasibility Study (Nghiên cứu tính khả thi) | Đánh giá tính khả thi về kỹ thuật, tài chính, thời gian | Phân tích nguồn lực, công nghệ | Dự án học tập, phạm vi và ràng buộc tối thiểu |
| 1.4 | Khởi tạo | Market Requirements Document (MRD) | Yêu cầu và nhu cầu thị trường mục tiêu | Nghiên cứu thị trường, phân tích đối thủ | Không phải sản phẩm thương mại cạnh tranh |
| 1.5 | Khởi tạo | Vision Document (Tài liệu tầm nhìn sản phẩm) | Định hình khái niệm, phạm vi và tầm nhìn sản phẩm | Ý tưởng cốt lõi, MRD, kỳ vọng các bên liên quan | Tương đương trong `Business_Requirements.md` |
| **2. Quản lý yêu cầu** |
| 2.1 | Yêu cầu nghiệp vụ | Business Requirements Document (BRD) | Đặc tả yêu cầu nghiệp vụ cấp cao | MRD, Vision Document | **ĐÃ CÓ** (`Business_Requirements.md`) |
| 2.2 | Yêu cầu nghiệp vụ | Stakeholder Analysis (Phân tích các bên liên quan) | Xác định vai trò, mức độ ảnh hưởng của các bên | Phỏng vấn, khảo sát | Một bên liên quan chính (Đại diện Khách hàng & Chủ đầu tư) |
| 2.3 | Yêu cầu nghiệp vụ | Context Diagram (Biểu đồ ngữ cảnh hệ thống) | Xác định ranh giới hệ thống và các thực thể ngoại vi | BRD, biên bản phỏng vấn | Không xây dựng biểu đồ riêng biệt |
| 2.4 | Yêu cầu người dùng | User Requirements Document | Nhu cầu, mong đợi và hành vi của người dùng | BRD, kịch bản nghiệp vụ | **ĐÃ CÓ** (`User_Stories.md`) |
| 2.5 | Yêu cầu người dùng | User Stories (Câu chuyện người dùng) | Yêu cầu theo định dạng "Là [vai trò] tôi muốn [hành động] để [lợi ích]" | User Requirements, phỏng vấn | **ĐÃ CÓ** (17 User Stories) |
| 2.6 | Yêu cầu người dùng | Use Case Diagram (Biểu đồ ca sử dụng) | Trực quan hóa các mối tương tác người dùng - hệ thống | User Stories, yêu cầu người dùng | **ĐÃ CÓ** (`Use_Cases.md`) |
| 2.7 | Yêu cầu người dùng | Use Case Specification (Đặc tả chi tiết UC) | Mô tả chi tiết các luồng chính, luồng phụ của ca sử dụng | Use Case Diagram | **ĐÃ CÓ** (10 Use Cases chi tiết) |
| 2.8 | Yêu cầu chức năng | Functional Requirements Document | Chi tiết từng chức năng cụ thể của hệ thống | Use Cases, User Stories | **ĐÃ CÓ** (Tích hợp trong Use Cases và Đề bài kỹ thuật) |
| 2.9 | Yêu cầu chức năng | Software Requirements Specification (SRS) | Toàn văn đặc tả kỹ thuật yêu cầu phần mềm | Tất cả các tài liệu yêu cầu | **ĐÃ CÓ** (`Technical_Specification.md`) |
| 2.10 | Yêu cầu chức năng | Requirements Traceability Matrix (RTM) | Ma trận truy vết từ yêu cầu đến thiết kế và kiểm thử | SRS, tài liệu thiết kế, kịch bản kiểm thử | **ĐÃ CÓ** (`Requirements_Traceability_Matrix.md`) |
| 2.11 | Yêu cầu phi chức năng | Non-Functional Requirements (NFR) | Hiệu năng, bảo mật, độ tin cậy, tính khả dụng | Yêu cầu nghiệp vụ, tiêu chuẩn kỹ thuật | **ĐÃ CÓ** (Trong SRS và Use Cases) |
| 2.12 | Yêu cầu phi chức năng | Security Requirements (Yêu cầu an toàn thông tin) | Các tiêu chuẩn và cơ chế bảo mật cần tuân thủ | NFR, tiêu chuẩn an toàn thông tin | Đã tích hợp trong SRS và Phân tích hệ thống |
| 2.13 | Yêu cầu phi chức năng | Performance Requirements (Yêu cầu hiệu năng) | Chỉ số thời gian phản hồi, thông lượng, tải đồng thời | NFR, kết quả benchmark | Đã tích hợp một phần trong SRS |
| **3. Phân tích và thiết kế hệ thống** |
| 3.1 | Phân tích hệ thống | System Analysis Document | Phân tích quy trình, hiện trạng và giải pháp | Yêu cầu, phỏng vấn nghiệp vụ | **ĐÃ CÓ** (`System_Analysis.md`) |
| 3.2 | Phân tích hệ thống | SWOT Analysis (Phân tích SWOT) | Đánh giá Điểm mạnh, Điểm yếu, Cơ hội, Thách thức | Phân tích môi trường nội bộ và bên ngoài | **ĐÃ CÓ** (Trong Phân tích hệ thống) |
| 3.3 | Phân tích hệ thống | Gap Analysis (Phân tích khoảng cách) | Đo lường độ chênh lệch giữa hiện trạng và mục tiêu | Yêu cầu, phân tích quy trình | Không áp dụng do xây dựng mới hoàn toàn |
| 3.4 | Kiến trúc phần mềm | Architecture Vision Document | Định hướng và tầm nhìn kiến trúc tổng thể | Yêu cầu, các ràng buộc công nghệ | Đã tích hợp trong Tài liệu kiến trúc |
| 3.5 | Kiến trúc phần mềm | Solution Architecture Document (SAD) | Kiến trúc tổng thể của giải pháp | Yêu cầu, ngăn xếp công nghệ được chọn | **ĐÃ CÓ** (`Architecture_Documentation.md`) |
| 3.6 | Kiến trúc phần mềm | Application Architecture Document | Cấu trúc phân tầng và module hóa ứng dụng | Solution Architecture, yêu cầu chức năng | **ĐÃ CÓ** (FastAPI backend + PyQt5 client) |
| 3.7 | Kiến trúc phần mềm | Data Architecture Document | Cấu trúc dữ liệu và luồng dữ liệu | Yêu cầu dữ liệu, mô hình thực thể | Đã tích hợp trong Tài liệu kiến trúc |
| 3.8 | Kiến trúc phần mềm | Integration Architecture Document | Kiến trúc kết nối tích hợp liên hệ thống | Yêu cầu tích hợp, đặc tả API | Không có tích hợp hệ thống bên ngoài |
| 3.9 | Kiến trúc phần mềm | Deployment Architecture Document | Kiến trúc môi trường triển khai thực tế | Yêu cầu hạ tầng, mô hình mạng LAN | **ĐÃ CÓ** (Mô tả chi tiết trong hướng dẫn cài đặt) |
| 3.10 | Kiến trúc phần mềm | Security Architecture Document | Kiến trúc an toàn và phân quyền người dùng | Yêu cầu bảo mật, mô hình JWT | Đã tích hợp trong phân tích và kiến trúc |
| 3.11 | Thiết kế hệ thống | System Design Document (SDD) | Thiết kế kỹ thuật chi tiết của hệ thống | Kiến trúc, SRS | **ĐÃ CÓ** (Tích hợp trong SRS và Kiến trúc) |
| 3.12 | Thiết kế hệ thống | High-Level Design (HLD) | Thiết kế mức cao (các khối chức năng chính) | Kiến trúc giải pháp, SRS | **ĐÃ CÓ** |
| 3.13 | Thiết kế hệ thống | Low-Level Design (LLD) | Thiết kế mức thấp (class, method, tham số) | HLD, quy chuẩn mã nguồn | Thể hiện trực tiếp trong mã nguồn |
| 3.14 | Thiết kế hệ thống | Interface Design Document | Thiết kế giao diện đồ họa (UI) và API | SRS, HLD | API đã có đặc tả; UI thể hiện qua Use Cases |
| 3.15 | Thiết kế hệ thống | Database Design Document | Thiết kế cấu trúc cơ sở dữ liệu chi tiết | Yêu cầu dữ liệu, ERD | **ĐÃ CÓ** (Trong tài liệu kiến trúc) |
| 3.16 | Thiết kế hệ thống | Network Design Document | Bản vẽ thiết kế hạ tầng mạng kết nối | Yêu cầu băng thông, topology mạng | Tích hợp trong tài liệu cài đặt và triển khai |
| 3.17 | Sơ đồ kỹ thuật | UML Diagrams (Nhiều loại) | Mô hình hóa trực quan tương tác và cấu trúc | Yêu cầu, tài liệu thiết kế | **ĐÃ CÓ** (Use Case, Sequence, ERD) |
| 3.18 | Sơ đồ kỹ thuật | ERD (Entity-Relationship Diagram) | Sơ đồ thực thể - mối quan hệ CSDL | Yêu cầu dữ liệu nghiệp vụ | **ĐÃ CÓ** (Bảng Users và Messages) |
| 3.19 | Sơ đồ kỹ thuật | Data Flow Diagram (DFD) | Sơ đồ luồng dữ liệu giữa các tiến trình | Yêu cầu, quy trình nghiệp vụ | Không vẽ sơ đồ DFD độc lập |
| 3.20 | Sơ đồ kỹ thuật | Activity Diagram (Sơ đồ hoạt động) | Luồng nghiệp vụ và quy trình thao tác | Use Cases | Không vẽ sơ đồ Activity độc lập |
| 3.21 | Sơ đồ kỹ thuật | State Machine Diagram (Sơ đồ trạng thái) | Biểu diễn chu kỳ vòng đời và trạng thái đối tượng | Yêu cầu, thiết kế logic | Không vẽ sơ đồ trạng thái độc lập |
| **4. Đặc tả kỹ thuật chi tiết** |
| 4.1 | Đặc tả kỹ thuật | Technical Requirements Document | Ràng buộc kỹ thuật, môi trường thực thi | Kiến trúc hệ thống, NFR | Nằm trong SRS và Tài liệu kiến trúc |
| 4.2 | Đặc tả kỹ thuật | API Specification (Đặc tả API) | Chi tiết endpoint, HTTP method, payload, response | Thiết kế giao diện lập trình | **ĐÃ CÓ** (`API_Documentation.md`) |
| 4.3 | Đặc tả kỹ thuật | SDK Documentation | Hướng dẫn sử dụng bộ công cụ phát triển phần mềm | API Specification, mã nguồn SDK | Hệ thống không phát triển SDK bên ngoài |
| 4.4 | Đặc tả kỹ thuật | Interface Control Document (ICD) | Kiểm soát chuẩn giao tiếp giữa các hệ thống phụ | API Spec, thỏa thuận tích hợp | Không có hệ thống phụ bên ngoài |
| 4.5 | Đặc tả kỹ thuật | Protocol Specification (Đặc tả giao thức) | Quy tắc giao thức truyền thông tùy biến | Yêu cầu kỹ thuật mạng | Giao thức WebSocket đã được mô tả kỹ trong kiến trúc |
| 4.6 | Đặc tả chi tiết | Detailed Design Document | Chi tiết thuật toán triển khai mã nguồn | LLD, yêu cầu kỹ thuật | Thể hiện trong source code và docstrings |
| 4.7 | Đặc tả chi tiết | Algorithm Specification (Đặc tả thuật toán) | Mô tả các thuật toán xử lý dữ liệu đặc thù | Thiết kế logic | Thuật toán đơn giản, không viết tài liệu riêng |
| 4.8 | Đặc tả chi tiết | Data Dictionary (Từ điển dữ liệu) | Giải thích tường tận từng trường dữ liệu, kiểu, độ dài | ERD, lược đồ CSDL | Đã tích hợp trong lược đồ DB và tài liệu API |
| **5. Lập kế hoạch và quản lý dự án** |
| 5.1 | Kế hoạch dự án | Project Management Plan (PMP) | Kế hoạch tổng thể điều hành dự án | Hiến chương dự án, yêu cầu | Dự án nội bộ quy mô tinh gọn (Agile Lean Team) |
| 5.2 | Kế hoạch dự án | Scope Management Plan | Kế hoạch quản lý và kiểm soát phạm vi dự án | SRS, WBS | Không yêu cầu quy trình phức tạp |
| 5.3 | Kế hoạch dự án | Schedule Management Plan | Kế hoạch quản lý tiến độ thời gian | WBS, ước lượng khối lượng | Quản lý theo các mốc bàn giao Sprint và kế hoạch phát triển |
| 5.4 | Kế hoạch dự án | Cost Management Plan | Kế hoạch dự toán và kiểm soát chi phí | Dự toán ngân sách | Dự án phát triển nội bộ phục vụ hạ tầng On-premise |
| 5.5 | Kế hoạch dự án | Quality Management Plan | Kế hoạch đảm bảo chất lượng sản phẩm | Yêu cầu chất lượng, quy chuẩn | Đảm bảo qua kế hoạch kiểm thử |
| 5.6 | Kế hoạch dự án | Resource Management Plan | Kế hoạch phân bổ nhân sự và thiết bị | Ước lượng công việc | Đội ngũ kỹ thuật tinh gọn đảm trách trọn gói giải pháp |
| 5.7 | Kế hoạch dự án | Communication Plan | Kế hoạch trao đổi thông tin trong nhóm | Phân tích các bên liên quan | Trao đổi định kỳ trực tiếp giữa Khách hàng và Trưởng dự án |
| 5.8 | Kế hoạch dự án | Risk Management Plan | Kế hoạch nhận diện và giảm thiểu rủi ro | Phân tích rủi ro hệ thống | **ĐÃ CÓ** (Nêu rõ trong Yêu cầu nghiệp vụ) |
| 5.9 | Kế hoạch dự án | Procurement Plan | Kế hoạch mua sắm trang thiết bị, bản quyền | Yêu cầu phần cứng/phần mềm | Không có hoạt động mua sắm ngoài phần mềm mở |
| 5.10 | Kế hoạch dự án | Stakeholder Engagement Plan | Kế hoạch tương tác với các bên liên quan | Phân tích các bên liên quan | Tập trung vào đại diện chủ chốt của Khách hàng |
| 5.11 | Tiến độ & Phân rã | Work Breakdown Structure (WBS) | Cấu trúc phân rã công việc theo cấp bậc | Yêu cầu, Scope Plan | Không lập cây WBS hình thức |
| 5.12 | Tiến độ & Phân rã | Project Schedule (Lịch trình dự án) | Lịch trình thực hiện từng giai đoạn | WBS, thời hạn đề ra | Thể hiện trong `Project_Development_Plan.md` |
| 5.13 | Tiến độ & Phân rã | Milestone Plan (Kế hoạch mốc quan trọng) | Các mốc then chốt cần nghiệm thu | Lịch trình dự án | Các mốc hoàn thành Sprint và kiểm thử UAT |
| 5.14 | Tiến độ & Phân rã | Gantt Chart (Biểu đồ Gantt) | Biểu đồ trực quan hóa tiến độ theo thời gian | Lịch trình chi tiết | Không lập biểu đồ Gantt riêng |
| 5.15 | Ước lượng | Cost Estimate (Dự toán chi phí) | Bảng tính toán chi phí tài chính dự kiến | WBS, giá thành tài nguyên | Chi phí được tối ưu hóa trong phạm vi dự án nội bộ |
| 5.16 | Ước lượng | Effort Estimation (Ước lượng công sức) | Tính toán số giờ công (man-hours) lập trình | WBS, dự án tương tự | Thể hiện trong kế hoạch phân bổ thời gian |
| 5.17 | Báo cáo quản lý | Status Report (Báo cáo tình trạng định kỳ) | Tình hình tổng quan theo tuần/tháng | Kế hoạch, tiến độ thực tế | Báo cáo cập nhật tiến độ trực tiếp cho Khách hàng |
| 5.18 | Báo cáo quản lý | Progress Report (Báo cáo tiến độ) | Chi tiết các đầu việc đã hoàn thành | Kế hoạch công việc | Không lập văn bản định kỳ riêng |
| 5.19 | Báo cáo quản lý | Variance Report (Báo cáo sai lệch) | Phân tích chênh lệch giữa kế hoạch và thực tế | Kế hoạch ban đầu, số liệu thực | Tiến độ bám sát kế hoạch phát triển cam kết |
| **6. Phát triển và cấu hình phần mềm** |
| 6.1 | Tiêu chuẩn mã nguồn | Coding Standards (Quy chuẩn viết mã) | Quy tắc định dạng code, đặt tên biến, comment | Yêu cầu chất lượng, hướng dẫn ngôn ngữ | Tuân thủ chuẩn PEP 8 cho Python |
| 6.2 | Tiêu chuẩn mã nguồn | Code Review Checklist | Danh mục tiêu chí kiểm tra chéo mã nguồn | Quy chuẩn viết mã | Quy trình kiểm tra chéo nội bộ trong nhóm kỹ thuật |
| 6.3 | Quản lý cấu hình | Configuration Management Plan | Kế hoạch quản trị phiên bản và cấu hình | Yêu cầu, hạ tầng lưu trữ | Sử dụng hệ thống Git |
| 6.4 | Quản lý cấu hình | Version Control Strategy | Chiến lược phân nhánh git (Gitflow/Trunk-based) | Kế hoạch quản trị cấu hình | Mô hình nhánh Git chuẩn hóa cho dự án |
| 6.5 | Quản lý cấu hình | Build Configuration Document | Cấu hình đóng gói và biên dịch phần mềm | Mã nguồn, file phụ thuộc | Định nghĩa qua `requirements.txt` |
| 6.6 | Quản lý cấu hình | Deployment Configuration | Cấu hình cài đặt môi trường triển khai | Hạ tầng, dependencies | **ĐÃ CÓ** (`Installation_and_Deployment.md`) |
| 6.7 | Quản lý cấu hình | Environment Configuration | Cấu hình các biến môi trường (Dev/Staging/Prod) | Yêu cầu kiểm thử, triển khai | Chỉ vận hành trên một môi trường nội bộ |
| 6.8 | Tài liệu mã nguồn | Code Documentation (Docstrings) | Giải thích chức năng hàm, class ngay trong code | Chuẩn mã nguồn Python | Đã viết comment và docstring trực tiếp trong code |
| 6.9 | Tài liệu mã nguồn | API Documentation (Tài liệu API) | Tài liệu kỹ thuật các hàm và endpoint | Mã nguồn, OpenAPI schema | **ĐÃ CÓ** (`API_Documentation.md`) |
| 6.10 | Tài liệu mã nguồn | Library/Framework Documentation | Hướng dẫn thư viện và framework bên thứ ba | Công nghệ sử dụng | Sử dụng tài liệu chính thức của FastAPI, PyQt5 |
| **7. Kiểm thử và đảm bảo chất lượng** |
| 7.1 | Chiến lược & Kế hoạch | Test Strategy (Chiến lược kiểm thử) | Phương pháp luận, phạm vi và mục tiêu kiểm thử | SRS, phân tích rủi ro | **ĐÃ CÓ** (Tích hợp trong Kế hoạch kiểm thử) |
| 7.2 | Chiến lược & Kế hoạch | Test Plan (Kế hoạch kiểm thử) | Lịch trình, tài nguyên và danh mục test case | Chiến lược kiểm thử, yêu cầu chức năng | **ĐÃ CÓ** (`Test_Plan.md`) |
| 7.3 | Chiến lược & Kế hoạch | Test Estimation (Ước lượng thời gian test) | Tính toán công sức và thời gian kiểm thử | Danh mục test case | Đã phân bổ trong Kế hoạch phát triển dự án |
| 7.4 | Thiết kế kiểm thử | Test Case Specification (Đặc tả ca kiểm thử) | Các bước thực hiện, dữ liệu test, kết quả mong đợi | SRS, kịch bản ca sử dụng | **ĐÃ CÓ** (Gồm 23 test case chi tiết) |
| 7.5 | Thiết kế kiểm thử | Test Scenario (Kịch bản kiểm thử) | Kịch bản kiểm tra tổng hợp luồng nghiệp vụ | Use Cases, User Stories | **ĐÃ CÓ** |
| 7.6 | Thiết kế kiểm thử | Test Data Specification | Tập dữ liệu mẫu dùng cho quá trình kiểm thử | Kịch bản kiểm thử | Tích hợp trực tiếp trong các test case |
| 7.7 | Thiết kế kiểm thử | Traceability Matrix (Ma trận truy vết kiểm thử) | Liên kết ca kiểm thử với yêu cầu phần mềm | SRS, Test Cases | Đã thể hiện trong tài liệu Ma trận truy vết |
| 7.8 | Tự động hóa kiểm thử | Test Automation Strategy | Chiến lược lựa chọn công cụ và kịch bản tự động | Test Plan, tài nguyên kiểm thử | Kiểm thử thủ công là chủ yếu |
| 7.9 | Tự động hóa kiểm thử | Automation Test Scripts | Mã kịch bản chạy test tự động | Test Cases, framework kiểm thử | Bộ script kiểm thử tự động nội bộ |
| 7.10 | Thực thi & Báo cáo | Test Execution Report (Báo cáo thực thi test) | Ghi nhận chi tiết kết quả chạy từng ca kiểm thử | Kịch bản kiểm thử, log thực tế | **ĐÃ CÓ** (`Test_Report.md`) |
| 7.11 | Thực thi & Báo cáo | Defect Report (Báo cáo lỗi/khiếm khuyết) | Danh sách và mức độ nghiêm trọng các lỗi tìm thấy | Kết quả kiểm thử | Đã tích hợp trong Báo cáo kiểm thử |
| 7.12 | Thực thi & Báo cáo | Test Summary Report (Báo cáo tổng kết test) | Tổng quan tỷ lệ đạt, đánh giá chất lượng cuối cùng | Toàn bộ kết quả thực thi | **ĐÃ CÓ** |
| 7.13 | Kiểm thử chuyên biệt | Performance Test Plan | Kế hoạch kiểm thử chịu tải và tốc độ xử lý | Yêu cầu hiệu năng | Kiểm tra cơ bản theo kịch bản đồng thời |
| 7.14 | Kiểm thử chuyên biệt | Security Test Plan | Kế hoạch kiểm tra lỗ hổng bảo mật | Yêu cầu an toàn thông tin | Kiểm tra cơ bản chống SQLi và xác thực JWT |
| 7.15 | Kiểm thử chuyên biệt | Usability Test Plan | Kế hoạch đánh giá trải nghiệm người dùng | Chuẩn UI/UX, User Stories | Đánh giá thông qua dùng thử thực tế |
| 7.16 | Kiểm thử chuyên biệt | Compatibility Test Plan | Kế hoạch kiểm thử tính tương thích nền tảng | Yêu cầu đa nền tảng | Đã kiểm thử trên Windows và Linux |
| **8. Triển khai và đưa vào sử dụng** |
| 8.1 | Kế hoạch triển khai | Deployment Plan (Kế hoạch triển khai) | Các bước cài đặt và cấu hình đưa hệ thống vào chạy | Tài liệu kiến trúc, file cấu hình | **ĐÃ CÓ** (`Installation_and_Deployment.md`) |
| 8.2 | Kế hoạch triển khai | Migration Plan (Kế hoạch chuyển đổi dữ liệu) | Phương án di chuyển dữ liệu từ hệ thống cũ | Cấu trúc dữ liệu cũ và mới | Hệ thống phát triển mới, không có dữ liệu cũ |
| 8.3 | Kế hoạch triển khai | Rollback Plan (Kế hoạch khôi phục khi lỗi) | Quy trình hủy bỏ triển khai và quay về trạng thái cũ | Kế hoạch triển khai, rủi ro | Chỉ cần khôi phục lại file CSDL sao lưu |
| 8.4 | Kế hoạch triển khai | Cutover Plan (Kế hoạch chuyển đổi vận hành) | Thời điểm và quy trình chuyển đổi chính thức | Kế hoạch triển khai | Bật máy chủ và cấp tài khoản cho người dùng |
| 8.5 | Hướng dẫn triển khai | Installation Guide (Hướng dẫn cài đặt) | Trình tự cài đặt từng bước cho server và client | Kế hoạch triển khai | **ĐÃ CÓ** (`Installation_and_Deployment.md`) |
| 8.6 | Hướng dẫn triển khai | Configuration Guide (Hướng dẫn cấu hình) | Hướng dẫn tinh chỉnh file cấu hình sau khi cài | Tài liệu kiến trúc mạng | **ĐÃ CÓ** (Hướng dẫn chỉnh sửa IP và port) |
| 8.7 | Hướng dẫn triển khai | Operations Guide (Hướng dẫn vận hành hàng ngày) | Quy trình khởi động, tắt và giám sát dịch vụ | Tài liệu hệ thống | **ĐÃ CÓ** (Trong Hướng dẫn bảo trì) |
| 8.8 | Hướng dẫn triển khai | Maintenance Guide (Hướng dẫn bảo trì) | Quy trình bảo dưỡng kỹ thuật, tối ưu định kỳ | Kiến trúc hệ thống, mã nguồn | **ĐÃ CÓ** (`Maintenance_Guide.md`) |
| 8.9 | Nghiệm thu triển khai | Go/No-Go Checklist (Bảng kiểm tra sẵn sàng) | Tiêu chí quyết định cho phép hệ thống hoạt động | Kết quả kiểm thử, hạ tầng | Đã tích hợp trong `Acceptance_Plan.md` |
| 8.10 | Báo cáo triển khai | Deployment Report (Báo cáo kết quả triển khai) | Tổng kết quá trình cài đặt thực tế | Kế hoạch và kết quả triển khai | Được ghi nhận trong biên bản bàn giao triển khai |
| **9. Vận hành và bảo trì hệ thống** |
| 9.1 | Quy trình chuẩn | Standard Operating Procedures (SOP) | Quy trình thao tác tiêu chuẩn cho đội vận hành | Tài liệu vận hành hệ thống | Hệ thống nhỏ gọn, áp dụng hướng dẫn bảo trì |
| 9.2 | Giám sát hệ thống | Monitoring Plan (Kế hoạch giám sát) | Danh mục các chỉ số CPU, RAM, Disk cần theo dõi | Kiến trúc, yêu cầu hiệu năng | Theo dõi thủ công qua Task Manager / System Monitor |
| 9.3 | Cảnh báo sự cố | Alerting Rules (Quy tắc phát cảnh báo) | Ngưỡng chỉ số và phương thức gửi thông báo sự cố | Kế hoạch giám sát | Không cấu hình hệ thống cảnh báo tự động phức tạp |
| 9.4 | Quản lý sự cố | Incident Management Plan | Quy trình tiếp nhận, phân loại và xử lý sự cố | Phân tích rủi ro, cam kết SLA | Người trực tiếp khắc phục là tác giả phần mềm |
| 9.5 | Xử lý sự cố | Incident Response Procedures | Các bước thao tác kỹ thuật ứng phó khẩn cấp | Kế hoạch quản lý sự cố | Hướng dẫn xử lý lỗi trong tài liệu bảo trì |
| 9.6 | Quản lý thay đổi | Change Management Plan | Quy trình đánh giá và phê duyệt các yêu cầu thay đổi | Vòng đời phần mềm | Không áp dụng thủ tục hành chính phức tạp |
| 9.7 | Quản lý thay đổi | Change Request Form (Phiếu yêu cầu thay đổi) | Biểu mẫu đề xuất nâng cấp hoặc chỉnh sửa tính năng | Kế hoạch quản lý thay đổi | Ghi nhận phản hồi trực tiếp từ người dùng thử nghiệm |
| 9.8 | Sao lưu và phục hồi | Backup and Recovery Plan | Kế hoạch và lịch trình sao lưu dữ liệu CSDL | Yêu cầu nghiệp vụ, cơ sở dữ liệu | **ĐÃ CÓ** (Kịch bản sao lưu file `messenger.db`) |
| 9.9 | Báo cáo vận hành | Performance Monitoring Report | Báo cáo đánh giá hiệu năng trong quá trình chạy thực tế | Nhật ký giám sát | Ghi nhận trong Báo cáo kết quả kiểm thử và nghiệm thu |
| 9.10 | Báo cáo vận hành | Security Monitoring Report | Báo cáo tình hình an ninh, các nỗ lực xâm nhập | Log hệ thống | Mạng nội bộ (LAN) cô lập an toàn, tách biệt Internet |
| **10. Hỗ trợ người dùng** |
| 10.1 | Hướng dẫn sử dụng | User Manual (Sách hướng dẫn sử dụng) | Hướng dẫn chi tiết từng chức năng cho người dùng cuối | Giao diện, tính năng phần mềm | **ĐÃ CÓ** (`User_Manual.md`) |
| 10.2 | Hướng dẫn sử dụng | Administrator Guide (Sách hướng dẫn quản trị) | Hướng dẫn quản lý tài khoản, giám sát cho admin | Kiến trúc, chức năng admin | Đã tích hợp trong hướng dẫn cài đặt và vận hành |
| 10.3 | Hướng dẫn sử dụng | Quick Start Guide (Hướng dẫn bắt đầu nhanh) | Các bước ngắn gọn để người mới dùng được ngay | Hướng dẫn sử dụng | **ĐÃ CÓ** (Phần đầu tài liệu người dùng) |
| 10.4 | Hướng dẫn sử dụng | Troubleshooting Guide (Hướng dẫn xử lý sự cố) | Cách tự khắc phục 10 lỗi thường gặp nhất | Nhật ký lỗi kiểm thử | **ĐÃ CÓ** (Tích hợp trong tài liệu người dùng & cài đặt) |
| 10.5 | Tài liệu tra cứu | FAQ (Các câu hỏi thường gặp) | Giải đáp các thắc mắc phổ biến của người dùng | Ý kiến phản hồi của người dùng | **ĐÃ CÓ** (Có trong hướng dẫn người dùng) |
| 10.6 | Tài liệu tra cứu | Glossary (Bảng thuật ngữ) | Định nghĩa và giải nghĩa chuẩn xác các thuật ngữ | Toàn bộ tài liệu dự án | **ĐÃ CÓ** (`Glossary.md`) |
| 10.7 | Đào tạo người dùng | Training Plan (Kế hoạch đào tạo) | Kế hoạch tập huấn sử dụng cho các phòng ban | Hướng dẫn sử dụng | Giao diện trực quan, không cần khóa học riêng |
| 10.8 | Đào tạo người dùng | Training Materials (Tài liệu tập huấn) | Slide trình chiếu, video hướng dẫn thao tác | Hướng dẫn sử dụng, demo | Bản chụp màn hình trong hướng dẫn sử dụng |
| 10.9 | Hỗ trợ kỹ thuật | Support Plan (Kế hoạch hỗ trợ kỹ thuật) | Quy trình và các kênh hỗ trợ kỹ thuật | Yêu cầu dịch vụ, SLA | Hỗ trợ kỹ thuật trực tiếp theo cam kết bàn giao |
| 10.10 | Hỗ trợ kỹ thuật | Service Level Agreement (SLA) | Cam kết chất lượng dịch vụ (thời gian phản hồi) | Thỏa thuận với khách hàng | Không có hợp đồng dịch vụ thương mại |
| **11. Kết thúc và bàn giao dự án** |
| 11.1 | Đóng dự án | Project Closure Report (Báo cáo đóng dự án) | Tổng kết kết quả, đánh giá mức độ đạt mục tiêu | Toàn bộ hồ sơ tài liệu | Tương đương Kế hoạch phát triển và nghiệm thu dự án |
| 11.2 | Đóng dự án | Lessons Learned Document (Bài học kinh nghiệm) | Những điều làm tốt, các điểm hạn chế cần cải thiện | Quá trình triển khai thực tế | Nêu trong phần kết luận tài liệu phân tích hệ thống |
| 11.3 | Đóng dự án | Final Project Documentation (Bộ hồ sơ hoàn công) | Trọn bộ tất cả tài liệu kỹ thuật của dự án | Toàn bộ tài liệu đã lập | **ĐÃ CÓ ĐẦY ĐỦ** (Toàn bộ bộ hồ sơ hiện tại) |
| 11.4 | Đóng dự án | Handover Document (Biên bản bàn giao sản phẩm) | Biên bản bàn giao mã nguồn và tài liệu quản trị | Mã nguồn, tài liệu hướng dẫn | Nghiệm thu và bàn giao chính thức cho đại diện Khách hàng |
| 11.5 | Đóng dự án | Post-Implementation Review | Đánh giá giá trị thực tế sau khi đưa vào dùng thử | Mục tiêu ban đầu, số liệu thực tế | Đã ghi nhận trong kế hoạch nghiệm thu |
| **12. Tài liệu bổ trợ và quy trình** |
| 12.1 | Bổ trợ | Meeting Minutes (Biên bản cuộc họp) | Ghi nhận nội dung thảo luận và thống nhất | Cuộc họp định kỳ | Biên bản các buổi họp rà soát kỹ thuật với Khách hàng |
| 12.2 | Bổ trợ | Decision Log (Nhật ký quyết định kiến trúc) | Lưu vết các quyết định kỹ thuật quan trọng | Biên bản họp, đề xuất kỹ thuật | Thể hiện qua các quyết định chọn thư viện trong tài liệu |
| 12.3 | Bổ trợ | Action Item Register (Sổ theo dõi đầu việc) | Danh sách các đầu việc phát sinh cần giải quyết | Cuộc họp, bug tracker | Theo dõi trên danh sách công việc cá nhân |
| 12.4 | Bổ trợ | Risk Register (Bảng theo dõi rủi ro) | Danh sách rủi ro và các biện pháp ứng phó | Phân tích rủi ro ban đầu | Đã tích hợp trong Yêu cầu nghiệp vụ |
| 12.5 | Bổ trợ | Issue Log (Nhật ký theo dõi sự cố) | Ghi chép các sự cố phát sinh ngoài ý muốn | Báo cáo kiểm thử, vận hành | Đã ghi nhận trong báo cáo kiểm thử |
| 12.6 | Bổ trợ | Correspondence Log (Nhật ký trao đổi) | Lưu trữ các trao đổi bằng văn bản, email | Hộp thư điện tử, tin nhắn | Trao đổi trực tiếp qua các kênh liên lạc chính thức |
| 12.7 | Phương pháp luận | Process Definition Document | Định nghĩa quy trình phát triển phần mềm | Mô hình phát triển (Agile/Waterfall) | Áp dụng mô hình Agile/Scrum linh hoạt cho dự án |
| 12.8 | Phương pháp luận | Team Charter (Quy ước nhóm) | Nguyên tắc làm việc, vai trò của từng thành viên | Thành viên nhóm | Đội ngũ kỹ thuật tinh gọn |
| 12.9 | Pháp lý & Bản quyền | Legal Compliance Document | Tuân thủ các quy định pháp luật và an toàn dữ liệu | Luật sở tại, tiêu chuẩn ngành | Mạng LAN nội bộ doanh nghiệp khép kín |
| 12.10 | Pháp lý & Bản quyền | License Agreement (Thỏa thuận cấp phép mã nguồn) | Giấy phép sử dụng phần mềm và thư viện | Loại giấy phép (MIT, Apache, GPL) | Sử dụng mã nguồn mở với giấy phép tương thích |

---

### **Tóm tắt phân tích mức độ đầy đủ của bộ tài liệu:**

**Các tài liệu cốt lõi đã có đầy đủ (15+ tài liệu chuyên nghiệp):**
- Tài liệu Yêu cầu nghiệp vụ (Business Requirements Document)
- Đề bài kỹ thuật / Đặc tả kỹ thuật phần mềm (SRS)
- Tài liệu Kịch bản ca sử dụng (Use Cases) + Câu chuyện người dùng (User Stories)
- Tài liệu Kiến trúc hệ thống (System Architecture Document)
- Hướng dẫn cài đặt và triển khai (Installation & Deployment Guide)
- Sách hướng dẫn sử dụng (User Manual)
- Kế hoạch kiểm thử (Test Plan) + Báo cáo kết quả kiểm thử (Test Report)
- Tài liệu đặc tả kỹ thuật API (API Documentation)
- Bảng thuật ngữ chuyên ngành (Glossary)
- Ma trận truy vết yêu cầu (Requirements Traceability Matrix)
- Hướng dẫn vận hành và bảo trì hệ thống (Maintenance Guide)
- Phân tích hệ thống và SWOT (System Analysis Document)
- Kế hoạch và tiêu chí nghiệm thu (Acceptance Plan)

**Các tài liệu không cần lập do đặc thù dự án (Dự án phần mềm nội bộ, mạng LAN On-premise, đội ngũ tinh gọn):**
- Các kế hoạch quản lý dự án hành chính (Quản lý chi phí ngân sách, kế hoạch mua sắm trang thiết bị bên ngoài, kế hoạch truyền thông tiếp thị).
- Tài liệu pháp lý, hợp đồng thương mại và cam kết cấp độ dịch vụ (SLA) với khách hàng bên ngoài.
- Quy trình quản lý thay đổi phức tạp qua nhiều ban bệ phê duyệt.
- Báo cáo giám sát hiệu năng/bảo mật quy mô đám mây tự động.
- Biên bản họp hội đồng quản trị và sổ theo dõi trao đổi email chính thức.

**Kết luận:** Bộ tài liệu của dự án này **đạt mức độ hoàn thiện chuyên nghiệp và chuẩn mực cao đối với một dự án phần mềm**, bao phủ toàn diện mọi khía cạnh kỹ thuật từ phân tích, thiết kế ban đầu, lập trình đến kiểm thử, cài đặt, bảo trì và nghiệm thu bàn giao cho Khách hàng.
