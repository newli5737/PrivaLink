# Ma trận truy vết yêu cầu (Requirements Traceability Matrix - RTM)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản tài liệu:** 1.0  
**Năm:** 2026  
**Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống

---

## 1. Giới thiệu tổng quan

Ma trận truy vết yêu cầu (RTM) là tài liệu kỹ thuật thiết lập mối liên kết xuyên suốt giữa các giai đoạn của dự án:
$$\text{Yêu cầu nghiệp vụ (BR)} \longrightarrow \text{Yêu cầu kỹ thuật (FR/NFR)} \longrightarrow \text{Mã nguồn (Code)} \longrightarrow \text{Bài kiểm thử (Test Cases)}$$

### Mục đích:
1. **Đảm bảo tính truy vết (Traceability):** Cho phép theo dõi nguồn gốc và việc hiện thực từng yêu cầu từ giai đoạn đề bài đến bài test kiểm thử.
2. **Đo lường độ hoàn thiện (Completeness):** Chứng minh toàn bộ các yêu cầu đã cam kết đều được lập trình và xác minh thực tế.
3. **Phục vụ nghiệm thu và bàn giao dự án:** Cung cấp bằng chứng kỹ thuật minh bạch giúp Khách hàng và các bên liên quan thẩm định chất lượng toàn diện của sản phẩm.

---

## 2. Ký hiệu và Quy ước

| Ký hiệu | Ý nghĩa | Trạng thái |
|:---:|---|---|
| Hoàn thành | Đã hiện thực hoàn chỉnh và kiểm thử thành công | Hoàn thành |
| Một phần | Hiện thực một phần hoặc cần tối ưu thêm | Một phần |
| Chưa hoàn thành | Chưa hiện thực | Bỏ ngỏ |
| Cao | Mức độ ưu tiên cao (Critical) | Bắt buộc |
| Trung bình | Mức độ ưu tiên trung bình (Major) | Quan trọng |
| [Online] | Mức độ ưu tiên thấp (Minor) | Tiện ích bổ sung |

---

## 3. Ma trận đối chiếu Yêu cầu Chức năng (Functional Requirements - FR)

### 3.1. Xác thực và Phân quyền

| Mã FR | Nội dung yêu cầu | Nguồn gốc | Ưu tiên | File mã nguồn hiện thực | Mã Test Case | Trạng thái |
|:---:|---|---|:---:|---|---|:---:|
| **FR-01** | Đăng ký tài khoản mới | BR-01, US-01 | Cao | `auth.py`, `user_model.py` | TC-01, TC-02 | Hoàn thành |
| **FR-02** | Đăng nhập hệ thống | BR-01, US-01 | Cao | `auth.py`, `login_dialog.py` | TC-03, TC-04 | Hoàn thành |
| **FR-03** | Xác thực phân quyền qua JWT | NFR-04 | Cao | `dependencies.py` | TC-05 | Hoàn thành |
| **FR-04** | Tài khoản đầu tiên tự động nhận quyền Admin | BR-02 | Trung bình | `auth.py`, `user_model.py` | TC-06 | Hoàn thành |
| **FR-05** | Đăng xuất khỏi hệ thống | US-01 | [Online] | `main_window.py` | TC-07 | Hoàn thành |

### 3.2. Nhắn tin & Trao đổi thông tin

| Mã FR | Nội dung yêu cầu | Nguồn gốc | Ưu tiên | File mã nguồn hiện thực | Mã Test Case | Trạng thái |
|:---:|---|---|:---:|---|---|:---:|
| **FR-06** | Gửi tin nhắn văn bản | BR-03, US-02 | Cao | `messages.py`, `chat_widget.py` | TC-08, TC-09 | Hoàn thành |
| **FR-07** | Nhận tin nhắn tức thời qua WebSocket | BR-04, US-03 | Cao | `websocket_manager.py`, `websocket_client.py` | TC-10, TC-11 | Hoàn thành |
| **FR-08** | Tải và xem lại lịch sử tin nhắn | BR-05, US-04 | Trung bình | `messages.py`, `chat_widget.py` | TC-12 | Hoàn thành |
| **FR-09** | Gửi và hiển thị hình ảnh Base64 | BR-06, US-05 | Trung bình | `messages.py`, `chat_widget.py` | TC-13, TC-14 | Hoàn thành |
| **FR-10** | Xóa tin nhắn cá nhân đã gửi | BR-07, US-06 | Trung bình | `messages.py`, `chat_widget.py` | TC-15 | Hoàn thành |

### 3.3. Danh bạ và Quản lý người dùng

| Mã FR | Nội dung yêu cầu | Nguồn gốc | Ưu tiên | File mã nguồn hiện thực | Mã Test Case | Trạng thái |
|:---:|---|---|:---:|---|---|:---:|
| **FR-11** | Hiển thị danh bạ mọi người dùng | BR-08, US-07 | Cao | `users.py`, `main_window.py` | TC-16 | Hoàn thành |
| **FR-12** | Chấm trạng thái Online/Offline trực quan | BR-09, US-08 | Trung bình | `websocket_manager.py`, `main_window.py` | TC-17 | Hoàn thành |
| **FR-13** | Tự động làm mới danh bạ mỗi 10 giây | US-08 | [Online] | `websocket_client.py`, QTimer | TC-18 | Hoàn thành |
| **FR-14** | Mở cuộc trò chuyện riêng khi click danh bạ | US-09 | Cao | `main_window.py`, `chat_widget.py` | TC-19 | Hoàn thành |
| **FR-15** | Mở nhiều tab chat cùng lúc | US-17 | Trung bình | `main_window.py` | TC-20 | Hoàn thành |

### 3.4. Chức năng Quản trị (Admin) & Giao diện

| Mã FR | Nội dung yêu cầu | Nguồn gốc | Ưu tiên | File mã nguồn hiện thực | Mã Test Case | Trạng thái |
|:---:|---|---|:---:|---|---|:---:|
| **FR-16** | Xem toàn bộ tài khoản người dùng qua API | US-10 | Trung bình | `admin.py` | TC-21 | Hoàn thành |
| **FR-17** | Xem toàn bộ tin nhắn hệ thống qua API | US-11 | Trung bình | `admin.py` | TC-22 | Hoàn thành |
| **FR-18** | Giao diện điều hướng dạng Tab | US-17 | Trung bình | `main_window.py` | TC-24 | Hoàn thành |
| **FR-19** | Ảnh thumbnail xem trước kích thước 200px | US-18 | [Online] | `chat_widget.py` | TC-25 | Hoàn thành |

---

## 4. Ma trận đối chiếu Yêu cầu Phi chức năng (Non-Functional Requirements - NFR)

| Mã NFR | Nội dung | Tiêu chí kỹ thuật | Giải pháp kỹ thuật | Đánh giá |
|:---:|---|---|---|:---:|
| **NFR-01** | Hỗ trợ tải đồng thời | $\ge 20$ kết nối đồng thời | FastAPI bất đồng bộ + SQLite WAL | Đạt |
| **NFR-02** | Độ trễ phản hồi tin nhắn | $\le 500$ ms trong LAN | Kênh WebSocket hai chiều thời gian thực | Đạt |
| **NFR-03** | Bảo mật mật khẩu | Không lưu văn bản thô | Băm bcrypt kết hợp chuỗi muối ngẫu nhiên (salt) | Đạt |
| **NFR-04** | Chống tấn công SQL Injection | 100% truy vấn an toàn | Sử dụng SQLAlchemy ORM và Parameterized query | Đạt |
| **NFR-05** | Đa nền tảng (Cross-platform) | Chạy được trên Win/Linux | Python 3 + thư viện PyQt5 đa nền tảng | Đạt |
| **NFR-06** | Hoạt động độc lập | Không cần kết nối Internet | Kiến trúc Client-Server chạy trong mạng nội bộ LAN | Đạt |
| **NFR-07** | Sao lưu dữ liệu tự động | Backup định kỳ CSDL | *Chưa tích hợp tự động (mới hỗ trợ sao lưu thủ công)*| Lưu ý |

---

## 5. Thống kê tỷ lệ hoàn thành và độ bao phủ (Coverage Analysis)

```
┌────────────────────────────────────────────────────────┐
│ BẢNG TỔNG KẾT MỨC ĐỘ BAO PHỦ YÊU CẦU DỰ ÁN             │
├─────────────────────────┬─────────┬──────────┬─────────┤
│ Phân loại               │ Chỉ tiêu│ Đạt được │ Tỷ lệ % │
├─────────────────────────┼─────────┼──────────┼─────────┤
│ Yêu cầu chức năng (FR)  │   20    │    20    │  100%   │
│ Yêu cầu phi chức năng   │    7    │     6    │ 85.7%   │
│ User Stories            │   15    │    15    │  100%   │
│ Use Cases               │   10    │    10    │  100%   │
├─────────────────────────┼─────────┼──────────┼─────────┤
│ TỔNG THỂ DỰ ÁN          │   52    │    51    │  98.1%  │
└─────────────────────────┴─────────┴──────────┴─────────┘
```

---

## 6. Kết luận

Ma trận truy vết yêu cầu khẳng định:
1. Dự án đã hiện thực đầy đủ **100% các tính năng cốt lõi** theo đúng hồ sơ đặc tả yêu cầu ban đầu.
2. Mọi tính năng trong mã nguồn đều có tài liệu thiết kế và kịch bản kiểm thử đối soát tương ứng.
3. Dự án đạt độ hoàn thiện cao, minh bạch và hoàn toàn đủ điều kiện để tiến hành nghiệm thu UAT và bàn giao chính thức cho khách hàng.

---

*Tài liệu Ma trận truy vết yêu cầu - Ban Dự án Local Messenger (2026)*
