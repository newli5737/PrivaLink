# Tóm tắt lý thuyết: Ngôn ngữ mô hình hóa UML (Unified Modeling Language)

UML (Unified Modeling Language) là ngôn ngữ mô hình hóa đồ họa được chuẩn hóa, dùng để trực quan hóa, thiết kế, lập tài liệu và phân tích các hệ thống phần mềm, quy trình nghiệp vụ và các hệ thống phức tạp khác.

### Ý tưởng cốt lõi:
UML cho phép biểu diễn hệ thống dưới dạng một tập hợp các biểu đồ trực quan, giúp các nhà phát triển, chuyên viên phân tích và khách hàng dễ dàng hiểu được. Đây là "ngôn ngữ chung" để mô tả kiến trúc và hành vi của hệ thống.

---

### Các loại biểu đồ chính trong UML (Chia thành 2 nhóm):

#### 1. Biểu đồ cấu trúc (Structural Diagrams) - Thể hiện hệ thống *gồm những gì*:
* **Biểu đồ lớp (Class Diagram):** Loại biểu đồ phổ biến nhất. Thể hiện các lớp (classes), thuộc tính, phương thức và các mối quan hệ giữa chúng (kế thừa, kết tập, liên kết...).
* **Biểu đồ thành phần (Component Diagram):** Thể hiện các mô-đun phần mềm, thư viện và mối quan hệ phụ thuộc giữa chúng.
* **Biểu đồ triển khai (Deployment Diagram):** Mô tả cách các thành phần phần mềm được phân bổ trên phần cứng vật lý (server, máy trạm, thiết bị mạng).
* **Biểu đồ cấu trúc ghép (Composite Structure Diagram):** Chi tiết hóa cấu trúc nội bộ bên trong một lớp hoặc thành phần.
* **Biểu đồ đối tượng (Object Diagram):** Ảnh chụp nhanh (snapshot) của hệ thống tại một thời điểm cụ thể, thể hiện các đối tượng thực tế và liên kết giữa chúng.
* **Biểu đồ gói (Package Diagram):** Nhóm các phần tử liên quan của hệ thống thành các gói logic.

#### 2. Biểu đồ hành vi (Behavioral Diagrams) - Thể hiện hệ thống *hoạt động như thế nào*:
* **Biểu đồ ca sử dụng (Use Case Diagram):** Mô tả tương tác giữa hệ thống và các tác nhân bên ngoài (người dùng, hệ thống khác). Thể hiện các yêu cầu chức năng.
* **Biểu đồ tuần tự (Sequence Diagram):** Minh họa sự trao đổi thông điệp giữa các đối tượng theo trục thời gian.
* **Biểu đồ máy trạng thái (State Machine Diagram):** Thể hiện sự chuyển đổi trạng thái của đối tượng khi có sự kiện kích hoạt.
* **Biểu đồ hoạt động (Activity Diagram):** Tương tự lưu đồ thuật toán (flowchart), mô tả luồng điều khiển của các thao tác hoặc quy trình nghiệp vụ.
* **Biểu đồ giao tiếp (Communication Diagram):** Tập trung vào cấu trúc quan hệ tương tác giữa các đối tượng.
* **Biểu đồ tổng quan tương tác (Interaction Overview Diagram):** Kết hợp giữa biểu đồ hoạt động và biểu đồ tuần tự.
* **Biểu đồ thời gian (Timing Diagram):** Biểu đồ chuyên sâu mô tả sự thay đổi trạng thái của đối tượng theo thời gian thực.

---

### Mục đích sử dụng UML:
- Trực quan hóa kiến trúc hệ thống phức tạp.
- Hỗ trợ phân tích và thiết kế phần mềm hướng đối tượng (OOP).
- Chuẩn hóa tài liệu yêu cầu, kiến trúc và giải pháp kỹ thuật.
- Cầu nối giao tiếp thông suốt giữa các bên: Lập trình viên, Phân tích nghiệp vụ, Kiểm thử và Khách hàng.
- Mô hình hóa và tối ưu quy trình nghiệp vụ.

### Các công cụ vẽ UML phổ biến:
- **PlantUML:** Tạo biểu đồ nhanh bằng mã văn bản (code-to-diagram).
- **draw.io / Lucidchart:** Thiết kế biểu đồ trực tuyến nhanh chóng.
- **Enterprise Architect, Visual Paradigm:** Bộ công cụ thiết kế UML chuyên nghiệp cấp doanh nghiệp.
- **Visual Studio Code / JetBrains IDEs:** Các tiện ích mở rộng tích hợp trực tiếp hỗ trợ PlantUML và Mermaid.
