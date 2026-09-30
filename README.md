# HỆ THỐNG TIN NHẮN VÀ TRAO ĐỔI NỘI BỘ BẢO MẬT — PRIVALINK
## Bộ Hồ Sơ Thiết Kế Kỹ Thuật Ban Đầu, Đặc Tả Kiến Trúc & Hướng Dẫn Nghiệm Thu Dành Cho Khách Hàng

---

### Giới thiệu tổng quan & Mục đích tài liệu
Bộ hồ sơ tài liệu này được biên soạn nhằm cung cấp cho **Khách hàng, Đối tác và Ban Quản trị Dự án** cái nhìn toàn diện, chuẩn xác và minh bạch về toàn bộ các tài liệu ban đầu khi thiết kế giải pháp phần mềm **PrivaLink** (Hệ thống nhắn tin và trao đổi dữ liệu nội bộ bảo mật).

Thông qua bộ hồ sơ này, Khách hàng có thể:
1. **Nắm bắt bài toán nghiệp vụ:** Hiểu rõ mục tiêu, phạm vi chức năng và các cam kết về an toàn dữ liệu nội bộ (BRD, User Stories, Use Cases).
2. **Thẩm định giải pháp kiến trúc:** Đánh giá cấu trúc phân tầng Client - Server, thiết kế cơ sở dữ liệu và khả năng mở rộng hệ thống (SAD, SRS, API Docs).
3. **Giám sát chất lượng định lượng:** Theo dõi kế hoạch kiểm thử, ma trận truy vết yêu cầu đạt **92%** và tỷ lệ kiểm thử thành công đạt **88.5%** (RTM, Test Plan, Test Report).
4. **Trực tiếp kiểm thử & Nghiệm thu bàn giao:** Vận dụng kịch bản kiểm thử chấp nhận người dùng (**UAT Checklist 16 bước**) để đối soát và ký nhận bàn giao sản phẩm chính thức.

---

### Thông tin dự án
* **Tên giải pháp:** PrivaLink (Hệ thống nhắn tin và truyền thông mạng LAN nội bộ bảo mật)
* **Mô hình triển khai:** On-premise (vận hành 100% trong mạng cục bộ, bảo mật tuyệt đối, không gửi dữ liệu ra ngoài Internet)
* **Phiên bản phát hành:** 1.0.0 (Production Release)
* **Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống (Engineering Team)
* **Kế hoạch phát triển dự án:** [Kế hoạch triển khai & phát triển dự án (Project Development Plan)](./Project_Development_Plan.md)
* **Thời gian hoàn tất:** Tháng 01 năm 2026

---

## Cấu trúc kho lưu trữ dự án

```
Kho lưu trữ tài liệu thiết kế dự án PrivaLink
├── Documentation/                        # Hồ sơ 15 tài liệu thiết kế & kỹ thuật ban đầu
│   ├── Business_Requirements.md         # Yêu cầu nghiệp vụ (Business Requirements Document - BRD)
│   ├── Architecture_Documentation.md    # Tài liệu kiến trúc hệ thống (Software Architecture Document - SAD)
│   ├── Technical_Specification.md       # Đặc tả kỹ thuật phần mềm (Technical Specification - SRS)
│   ├── User_Stories.md                  # Câu chuyện người dùng (User Stories)
│   ├── Test_Plan.md                     # Kế hoạch kiểm thử chất lượng (Test Plan)
│   ├── User_Manual.md                   # Sổ tay hướng dẫn sử dụng cho người dùng cuối (User Manual)
│   ├── Use_Cases.md                     # Đặc tả chi tiết các trường hợp sử dụng (Use Cases)
│   ├── System_Analysis.md               # Báo cáo phân tích hệ thống & SWOT (System Analysis)
│   ├── Glossary.md                      # Bảng thuật ngữ chuyên ngành chuẩn hóa (Glossary)
│   ├── Installation_and_Deployment.md   # Hướng dẫn cài đặt và triển khai hệ thống (Installation Guide)
│   ├── API_Documentation.md             # Đặc tả chi tiết API REST & giao thức WebSocket
│   ├── Maintenance_Guide.md             # Sổ tay quản trị, vận hành và bảo trì máy chủ (Maintenance Guide)
│   ├── Requirements_Traceability_Matrix.md # Ma trận truy vết yêu cầu (Traceability Matrix - RTM)
│   ├── Test_Report.md                   # Báo cáo kết quả kiểm thử thực tế (Test Report)
│   └── Acceptance_Plan.md               # Kế hoạch kiểm thử chấp nhận người dùng & Biên bản nghiệm thu (UAT)
│
├── Supplementary_Files/                 # Tài liệu bổ trợ kỹ thuật & Quy chuẩn đối chiếu
│   ├── Lecture_Notes.md                 # Tóm tắt lý thuyết mô hình hóa UML và phương pháp đánh giá hệ thống
│   ├── Document_Types_List.md           # Bảng danh mục đối chiếu hơn 100 loại tài liệu kỹ nghệ phần mềm
│   └── Evaluation.puml                  # Sơ đồ PlantUML quy trình thẩm định chất lượng & nghiệm thu UAT
│
├── Project_Development_Plan.md          # Kế hoạch phát triển và triển khai dự án chi tiết
└── README.md                            # Cổng thông tin trung tâm dành cho Khách hàng & Đối tác
```

---

## Mục lục 15 tài liệu thiết kế & kỹ thuật ban đầu

### 1. [Yêu cầu nghiệp vụ (Business Requirements Document - BRD)](./Documentation/Business_Requirements.md)
**Đường dẫn file:** `Documentation/Business_Requirements.md`  
**Giá trị cho Khách hàng:** Giúp khách hàng nắm bắt rõ định vị giải pháp, bài toán cần giải quyết, phạm vi tính năng phiên bản 1.0 và các tiêu chí đánh giá thành công của dự án từ góc nhìn hiệu quả hoạt động và an toàn thông tin.

**Nội dung chính:**
- Bối cảnh và sự cần thiết của hệ thống nhắn tin nội bộ LAN độc lập
- Mục tiêu chiến lược: bảo mật dữ liệu tuyệt đối, không rò rỉ ra ngoài Internet
- Bảng phân tích phạm vi tính năng (những gì hệ thống ĐÃ LÀM và CHƯA LÀM)
- Các tính năng nổi bật: Tự động dò tìm server qua UDP Broadcast, mã hóa băm bcrypt, hỗ trợ Dark Mode
- Bảng phân tích rủi ro và giải pháp phòng ngừa

---

### 2. [Tài liệu kiến trúc hệ thống (Software Architecture Document - SAD)](./Documentation/Architecture_Documentation.md)
**Đường dẫn file:** `Documentation/Architecture_Documentation.md`  
**Giá trị cho Khách hàng:** Cung cấp bức tranh toàn cảnh về thiết kế kỹ thuật, chứng minh hệ thống được xây dựng bài bản theo chuẩn phân tầng, bảo đảm tính ổn định và khả năng nâng cấp linh hoạt trong tương lai.

**Nội dung chính:**
- Sơ đồ kiến trúc phân tầng tổng thể (Layered Architecture)
- Biểu đồ thành phần (Component Diagram) kết nối Client - Server
- Biểu đồ tuần tự (Sequence Diagram) luồng xác thực JWT và gửi nhận tin nhắn thời gian thực
- Mô hình quan hệ thực thể cơ sở dữ liệu (ERD)
- Quyết định kiến trúc: Cơ chế chuyển đổi từ SQLite sang PostgreSQL khi mở rộng quy mô

---

### 3. [Đặc tả yêu cầu kỹ thuật phần mềm (Technical Specification - SRS)](./Documentation/Technical_Specification.md)
**Đường dẫn file:** `Documentation/Technical_Specification.md`  
**Giá trị cho Khách hàng:** Là văn bản kỹ thuật cơ sở để đối soát tính năng và làm căn cứ nghiệm thu hợp đồng phát triển phần mềm giữa hai bên.

**Nội dung chính:**
- Mã định danh dự án và các tiêu chuẩn tuân thủ
- Danh mục chi tiết các yêu cầu chức năng (FR) và phi chức năng (NFR)
- Ngăn xếp công nghệ thực tế và phiên bản thư viện sử dụng
- Yêu cầu cấu hình phần cứng tối thiểu cho máy chủ và máy trạm
- Tiêu chuẩn hiệu năng: Độ trễ tin nhắn $\le 100$ms, tải lịch sử $\le 300$ms

---

### 4. [Câu chuyện người dùng (User Stories)](./Documentation/User_Stories.md)
**Đường dẫn file:** `Documentation/User_Stories.md`  
**Giá trị cho Khách hàng:** Giúp khách hàng hình dung rõ nét từng tình huống sử dụng thực tế của nhân viên và quản trị viên, kèm theo tiêu chí nghiệm thu cụ thể cho từng câu chuyện.

**Nội dung chính:**
- 15 câu chuyện người dùng cho nhân sự thông thường (Đăng ký, gửi tin nhắn, đính kèm ảnh, đổi chủ đề giao diện,...)
- 02 câu chuyện người dùng dành cho Quản trị viên (Admin)
- Ma trận đối soát 100% giữa User Stories với các file mã nguồn hiện thực thực tế

---

### 5. [Kế hoạch kiểm thử chất lượng (Test Plan)](./Documentation/Test_Plan.md)
**Đường dẫn file:** `Documentation/Test_Plan.md`  
**Giá trị cho Khách hàng:** Minh chứng cho quy trình kiểm soát chất lượng nghiêm ngặt trước khi sản phẩm được bàn giao đến tay người dùng.

**Nội dung chính:**
- Mục tiêu và đối tượng kiểm thử (Tầng Client GUI, Tầng Backend API, Kênh WebSocket)
- Các phương pháp kiểm thử: Chức năng (Functional), Tích hợp (Integration), Giao diện (UI) và Chịu tải (Stress)
- Danh mục 23 kịch bản kiểm thử (Test Cases) có phân bổ độ ưu tiên rõ ràng
- Tiêu chuẩn đánh giá Pass/Fail và lịch trình kiểm thử

---

### 6. [Sổ tay hướng dẫn sử dụng (User Manual)](./Documentation/User_Manual.md)
**Đường dẫn file:** `Documentation/User_Manual.md`  
**Giá trị cho Khách hàng:** Tài liệu bàn giao trực tiếp cho người dùng cuối trong tổ chức, giúp rút ngắn thời gian làm quen và làm chủ ứng dụng ngay lập tức.

**Nội dung chính:**
- Hướng dẫn khởi động nhanh trong 4 bước (Quickstart)
- Hướng dẫn đăng ký, đăng nhập tài khoản
- Hướng dẫn thao tác trò chuyện riêng 1-1, gửi và xem ảnh đính kèm
- Giải đáp 6 câu hỏi thường gặp nhất (FAQ) và cách xử lý lỗi cơ bản

---

### 7. [Đặc tả các ca sử dụng (Use Cases Document)](./Documentation/Use_Cases.md)
**Đường dẫn file:** `Documentation/Use_Cases.md`  
**Giá trị cho Khách hàng:** Cung cấp kịch bản chi tiết về luồng thao tác người dùng (luồng chính, luồng phụ, điều kiện tiên quyết và hậu điều kiện) cho từng nghiệp vụ.

**Nội dung chính:**
- Sơ đồ tổng thể Use Case trực quan hóa bằng Mermaid
- 10 ca sử dụng chức năng nghiệp vụ trọng tâm
- 03 ca sử dụng phi chức năng về hiệu năng và bảo mật
- Biểu đồ tuần tự chi tiết cho luồng gửi tin nhắn và đồng bộ hóa tức thời

---

### 8. [Báo cáo phân tích hệ thống (System Analysis)](./Documentation/System_Analysis.md)
**Đường dẫn file:** `Documentation/System_Analysis.md`  
**Giá trị cho Khách hàng:** Cung cấp góc nhìn chuyên sâu của kỹ sư hệ thống về điểm mạnh, điểm yếu, nợ kỹ thuật và lộ trình nâng cấp giải pháp trong tương lai.

**Nội dung chính:**
- Đánh giá mức độ phủ yêu cầu nghiệp vụ trong mã nguồn
- Phân tích tương tác thành phần và luồng dữ liệu hai chiều
- Ma trận phân tích SWOT (Điểm mạnh, Điểm yếu, Cơ hội, Thách thức)
- Lộ trình phát triển đề xuất 3 giai đoạn: UI/UX $\rightarrow$ Chat nhóm $\rightarrow$ Tích hợp mở rộng quy mô

---

### 9. [Thuật ngữ chuyên ngành chuẩn hóa (Glossary)](./Documentation/Glossary.md)
**Đường dẫn file:** `Documentation/Glossary.md`  
**Giá trị cho Khách hàng:** Giúp khách hàng và đội ngũ kỹ thuật thống nhất ngôn ngữ chung, giải thích rõ ràng hơn 80 thuật ngữ kỹ thuật và từ viết tắt xuất hiện trong dự án.

**Nội dung chính:**
- 81 thuật ngữ phân loại thành 12 nhóm chuyên đề kỹ thuật
- Giải nghĩa chi tiết các khái niệm: FastAPI, WebSocket, JWT, bcrypt, SQLite, UDP Broadcast,...
- Ngữ cảnh áp dụng thực tế của từng thuật ngữ trong mã nguồn giải pháp

---

### 10. [Hướng dẫn cài đặt và triển khai hệ thống (Installation Guide)](./Documentation/Installation_and_Deployment.md)
**Đường dẫn file:** `Documentation/Installation_and_Deployment.md`  
**Giá trị cho Khách hàng:** Cẩm nang từng bước để bộ phận IT của Khách hàng tự chủ triển khai máy chủ và phân phối ứng dụng máy trạm trong mạng nội bộ.

**Nội dung chính:**
- Hướng dẫn cài đặt Python và môi trường ảo
- Cài đặt các gói thư viện phụ thuộc (`requirements.txt`)
- Cấu hình máy chủ Server (đặt IP tĩnh, mở port firewall 8000)
- Kịch bản kiểm thử quy trình sau cài đặt
- Bảng khắc phục 10 sự cố phổ biến khi triển khai mạng LAN

---

### 11. [Đặc tả kỹ thuật API (API Documentation)](./Documentation/API_Documentation.md)
**Đường dẫn file:** `Documentation/API_Documentation.md`  
**Giá trị cho Khách hàng:** Cung cấp thông số giao tiếp chuẩn xác cho các kỹ sư lập trình muốn tích hợp giải pháp này với các phần mềm quản trị nội bộ khác của doanh nghiệp.

**Nội dung chính:**
- Đặc tả toàn bộ REST API Endpoints (Auth, Users, Messages, Admin)
- Giao thức sự kiện WebSocket thời gian thực (tin nhắn mới, cập nhật online/offline)
- Cấu trúc dữ liệu JSON Schema (Pydantic models)
- Bảng mã lỗi HTTP và code mẫu gọi API bằng Python, JavaScript, cURL

---

### 12. [Sổ tay vận hành và bảo trì máy chủ (Maintenance Guide)](./Documentation/Maintenance_Guide.md)
**Đường dẫn file:** `Documentation/Maintenance_Guide.md`  
**Giá trị cho Khách hàng:** Hướng dẫn đội ngũ quản trị hệ thống (System Admin) vận hành máy chủ bền bỉ, an toàn và xử lý kịp thời các tình huống khẩn cấp.

**Nội dung chính:**
- Quy trình bảo trì định kỳ (hàng ngày, hàng tuần, hàng tháng)
- Giám sát CPU, RAM, số lượng kết nối mạng và file log
- Quy trình sao lưu (Backup) tự động và phục hồi cơ sở dữ liệu khi gặp sự cố
- Quy trình cập nhật phiên bản phần mềm an toàn (Rollback Plan)

---

### 13. [Ma trận truy vết yêu cầu (Traceability Matrix - RTM)](./Documentation/Requirements_Traceability_Matrix.md)
**Đường dẫn file:** `Documentation/Requirements_Traceability_Matrix.md`  
**Giá trị cho Khách hàng:** Bằng chứng định lượng khẳng định 100% các yêu cầu ban đầu đều được hiện thực hóa trong code và kiểm thử đầy đủ.

**Nội dung chính:**
- Bảng đối chiếu 4 chiều: Mục tiêu $\rightarrow$ Yêu cầu kỹ thuật $\rightarrow$ File mã nguồn $\rightarrow$ Test Case
- Tỷ lệ đáp ứng yêu cầu chức năng đạt **92%**
- Thống kê chi tiết 21 yêu cầu chức năng và 17 yêu cầu phi chức năng

---

### 14. [Báo cáo kết quả kiểm thử (Test Report)](./Documentation/Test_Report.md)
**Đường dẫn file:** `Documentation/Test_Report.md`  
**Giá trị cho Khách hàng:** Báo cáo định lượng về chất lượng sản phẩm thực tế sau các đợt kiểm thử chuyên sâu.

**Nội dung chính:**
- Tổng kết kiểm thử: **88.5%** kịch bản kiểm thử đạt tiêu chuẩn (Pass)
- Không có bất kỳ lỗi nghiêm trọng nào (0 Critical Defects)
- Kết quả kiểm thử chịu tải và đo lường độ trễ mạng LAN
- Đánh giá mức độ sẵn sàng bàn giao đạt **85%**

---

### 15. [Kế hoạch kiểm thử chấp nhận người dùng & Nghiệm thu (Acceptance Plan / UAT)](./Documentation/Acceptance_Plan.md)
**Đường dẫn file:** `Documentation/Acceptance_Plan.md`  
**Giá trị cho Khách hàng:** Cung cấp kịch bản kiểm tra thực tế (Checklist 16 bước) và mẫu biên bản nghiệm thu để Khách hàng chính thức tiếp nhận sản phẩm.

**Nội dung chính:**
- Quy trình UAT 5 bước tiêu chuẩn công nghiệp
- Checklist 16 thao tác kiểm thử trực quan giữa 2 máy trạm Client
- Barem tiêu chuẩn chất lượng bàn giao theo thang điểm 100%
- Mẫu Biên bản bàn giao và nghiệm thu dự án chính thức (Sign-off)

---

## Các tài liệu bổ trợ kỹ thuật (Thư mục "Supplementary_Files")

1. **[Lecture_Notes.md](./Supplementary_Files/Lecture_Notes.md)**: Tài liệu tóm tắt lý thuyết về ngôn ngữ mô hình hóa UML (các biểu đồ cấu trúc và hành vi) và phương pháp đánh giá hệ thống phần mềm.
2. **[Evaluation.puml](./Supplementary_Files/Evaluation.puml)**: Biểu đồ PlantUML thể hiện thuật toán thẩm định chất lượng và quy trình 3 giai đoạn ra quyết định nghiệm thu bàn giao dự án.
3. **[Document_Types_List.md](./Supplementary_Files/Document_Types_List.md)**: Bảng danh mục đối chiếu hơn **100 loại tài liệu kỹ nghệ phần mềm công nghiệp**, phân tích lý do chọn lọc và mức độ đáp ứng trong giải pháp Local Messenger.

---

## Hướng dẫn khởi chạy ứng dụng để Demo / Kiểm thử nghiệm thu

> [!NOTE]
> Kho lưu trữ này là **Bộ Hồ Sơ Thiết Kế Kỹ Thuật & Tài Liệu Bàn Giao Ban Đầu** dành cho Khách hàng. Mã nguồn giải pháp (Source Code) được quản lý độc lập tại repository nội bộ của đơn vị phát triển. Khi nhận bàn giao gói mã nguồn, quý khách thực hiện các bước sau để thiết lập môi trường chạy thử nghiệm:

### Bước 1: Chuẩn bị mã nguồn
```bash
git clone https://github.com/newli5737/PrivaLink.git
cd PrivaLink/messenger
```

### Bước 2: Thiết lập môi trường thực thi
```bash
# Tạo môi trường ảo
python3 -m venv venv

# Kích hoạt môi trường ảo:
# Trên Windows:
venv\Scripts\activate
# Trên Linux/macOS:
source venv/bin/activate

# Cài đặt toàn bộ thư viện cần thiết
pip install -r requirements.txt
```

### Bước 3: Khởi chạy Máy chủ (Server Backend)
```bash
cd server
python3 main.py
# Server sẽ tự động lắng nghe tại cổng http://0.0.0.0:8000
# Mở trình duyệt truy cập tài liệu Swagger UI: http://localhost:8000/docs
```

### Bước 4: Khởi chạy Ứng dụng Máy trạm (Desktop Client)
Mở một cửa sổ Terminal mới:
```bash
cd client
python3 main.py
```

### Bước 5: Kiểm thử luồng trao đổi thực tế
1. Đăng ký tài khoản người dùng đầu tiên (tự động nhận quyền Quản trị viên - Admin).
2. Mở thêm cửa sổ Client thứ hai, đăng ký tài khoản thành viên tiếp theo.
3. Chọn người dùng trong danh bạ và bắt đầu nhắn tin thời gian thực!

---

## Tổng quan công nghệ & Thông số kỹ thuật

* **Tên ứng dụng:** PrivaLink (Ứng dụng trao đổi nội bộ bảo mật)
* **Mô hình triển khai:** Client - Server chạy trong mạng cục bộ (LAN On-premise)
* **Backend:** Python, FastAPI (bất đồng bộ), Uvicorn ASGI, WebSockets, SQLite, SQLAlchemy ORM, JWT, bcrypt
* **Frontend GUI:** Python, PyQt5, QSS Theme Engine (Light / Dark / Custom themes)
* **Truyền thông mạng:** HTTP REST API cho dữ liệu có cấu trúc, WebSocket cho tin nhắn thời gian thực, UDP Broadcast cho tính năng tự động dò tìm máy chủ
* **Hiệu năng:** Độ trễ gửi nhận tin nhắn $< 100$ms; hỗ trợ tải lịch sử phân trang; nén và xem trước ảnh thumbnail tức thời

---

## Giá trị mang lại cho Khách hàng & Tổ chức

Giải pháp **PrivaLink** mang lại các lợi ích thiết thực:
- **Tự chủ và bảo mật dữ liệu tuyệt đối:** Toàn bộ dữ liệu nằm trọn vẹn trong máy chủ nội bộ của tổ chức, triệt tiêu hoàn toàn nguy cơ rò rỉ thông tin ra Internet.
- **Tốc độ và độ tin cậy cao:** Không bị gián đoạn khi đường truyền Internet quốc tế gặp sự cố cáp quang; hệ thống hoạt động ổn định trong mạng LAN nội bộ.
- **Tiết kiệm chi phí vận hành:** Không phải trả phí bản quyền thuê bao SaaS hàng tháng (0 đồng chi phí duy trì đám mây).
- **Hồ sơ kỹ thuật minh bạch:** Trọn bộ 15 văn bản thiết kế ban đầu chuẩn công nghiệp giúp khách hàng hoàn toàn làm chủ hệ thống và dễ dàng đào tạo, chuyển giao cho đội ngũ kế thừa.
