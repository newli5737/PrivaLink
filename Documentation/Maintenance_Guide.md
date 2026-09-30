# Sổ tay vận hành và bảo trì hệ thống (Maintenance Guide)
## Hệ thống tin nhắn và trao đổi nội bộ bảo mật (Local Messenger)

**Phiên bản tài liệu:** 1.0  
**Năm:** 2026  
**Đơn vị phát triển:** Ban Dự án Phần mềm & Kỹ thuật Hệ thống  
**Đối tượng sử dụng:** Quản trị viên hệ thống (System Administrator) & Đội ngũ kỹ thuật vận hành

---

## Mục lục

1. [Giới thiệu](#gioi-thieu)
2. [Cấu trúc kiến trúc vận hành](#cau-truc-van-hanh)
3. [Quy trình bảo trì định kỳ](#quy-trinh-dinh-ky)
4. [Giám sát và Chẩn đoán hệ thống](#giam-sat)
5. [Sao lưu (Backup) và Phục hồi dữ liệu](#sao-luu-phuc-hoi)
6. [Quy trình nâng cấp và cập nhật phiên bản](#nang-cap)
7. [Xử lý sự cố khẩn cấp (Troubleshooting)](#xu-ly-su-co)
8. [Chính sách an toàn thông tin](#an-toan)
9. [Các kịch bản tự động hóa hữu ích](#scripts)

---

<a name="gioi-thieu"></a>
## 1. Giới thiệu

Tài liệu này cung cấp hướng dẫn toàn diện cho người quản trị phòng máy / hệ thống mạng tại cơ sở giáo dục nhằm duy trì, vận hành và khắc phục sự cố ứng dụng "Local Messenger".

### Phân công trách nhiệm vận hành:
* **Máy chủ Server (FastAPI + SQLite):** Quản trị viên hệ thống kiểm tra hàng ngày.
* **Cơ sở dữ liệu (`messenger.db`):** Kiểm tra tính toàn vẹn và sao lưu hàng tuần.
* **Mạng nội bộ LAN:** Quản trị mạng kiểm tra định kỳ.
* **Ứng dụng Client (PyQt5):** Hỗ trợ người dùng khi có yêu cầu.

---

<a name="cau-truc-van-hanh"></a>
## 2. Cấu trúc kiến trúc vận hành

```
┌────────────────────────────────────────────────────────┐
│ Mạng LAN trường học (192.168.1.0/24)                   │
│                                                        │
│  [Client Win11]       [Client Ubuntu]    [Client macOS]│
│         ▲                    ▲                 ▲       │
│         └──────────────┬─────┴─────────────────┘       │
│                        │ HTTP / WebSocket              │
│                        ▼                               │
│             ┌───────────────────────┐                  │
│             │ Máy chủ Server        │                  │
│             │ IP: 192.168.1.100:8000│                  │
│             │ - Tiến trình: FastAPI │                  │
│             │ - CSDL: messenger.db  │                  │
│             │ - Log: server.log     │                  │
│             └───────────────────────┘                  │
└────────────────────────────────────────────────────────┘
```

---

<a name="quy-trinh-dinh-ky"></a>
## 3. Quy trình bảo trì định kỳ

### 3.1. Công việc hàng ngày (Daily Check)
1. **Kiểm tra tiến trình Server:**
```bash
# Trên Linux Server
ps aux | grep python
netstat -tuln | grep 8000
```
2. **Kiểm tra file log phát hiện lỗi bất thường:**
```bash
tail -n 50 /path/to/messenger/server/server.log
```

### 3.2. Công việc hàng tuần (Weekly Check)
1. **Kiểm tra kích thước và độ toàn vẹn CSDL:**
```bash
cd messenger/server
ls -lh messenger.db
sqlite3 messenger.db "PRAGMA integrity_check;"
# Kết quả mong đợi: ok
```
2. **Kiểm tra dung lượng đĩa trống máy chủ:**
```bash
df -h
```

---

<a name="giam-sat"></a>
## 4. Giám sát và Chẩn đoán hệ thống

### 4.1. Giám sát tài nguyên hệ thống (Linux)
* Theo dõi CPU & RAM: Chạy lệnh `htop` hoặc `top`.
* Theo dõi kết nối mạng tới cổng 8000:
```bash
netstat -an | grep :8000 | wc -l
```

### 4.2. Kiểm tra Health Check qua HTTP
Sử dụng cURL hoặc trình duyệt để kiểm tra trạng thái phản hồi của Server:
```bash
curl -I http://localhost:8000/docs
# Phản hồi mong đợi: HTTP/1.1 200 OK
```

---

<a name="sao-luu-phuc-hoi"></a>
## 5. Sao lưu (Backup) và Phục hồi dữ liệu

### 5.1. Quy trình sao lưu thủ công CSDL SQLite
Trước khi sao lưu, đảm bảo dữ liệu ghi từ bộ đệm đã được đẩy xuống đĩa:
```bash
cd messenger/server
# Tạo bản snapshot an toàn
sqlite3 messenger.db ".backup 'backup_messenger_$(date +%Y%m%d_%H%M%S).db'"
```

### 5.2. Quy trình phục hồi dữ liệu (Restore)
Nếu file `messenger.db` bị lỗi hoặc mất dữ liệu:
1. Tắt tiến trình server: `kill -9 <PID_SERVER>`
2. Đổi tên file db lỗi: `mv messenger.db messenger_corrupted.db`
3. Sao chép bản backup gần nhất về:
```bash
cp backup_messenger_20260119.db messenger.db
```
4. Khởi động lại Server: `python3 main.py`

---

<a name="nang-cap"></a>
## 6. Quy trình nâng cấp và cập nhật phiên bản

1. **Thông báo bảo trì:** Nhắc nhở người dùng lưu dữ liệu và tạm ngưng chat.
2. **Sao lưu toàn bộ thư mục dự án:**
```bash
tar -czvf messenger_backup_before_update.tar.gz messenger/
```
3. **Kéo mã nguồn mới nhất từ kho Git:**
```bash
git pull origin main
```
4. **Cập nhật các gói thư viện phụ thuộc (nếu có thay đổi):**
```bash
pip install -r requirements.txt --upgrade
```
5. **Khởi chạy lại Server và kiểm tra hoạt động.**

---

<a name="xu-ly-su-co"></a>
## 7. Xử lý sự cố khẩn cấp (Troubleshooting)

| Tình huống sự cố | Nguyên nhân khả dĩ | Phương án xử lý ngay |
|---|---|---|
| **Server không bật được (Port 8000 in use)** | Có một tiến trình uvicorn/python cũ đang chiếm cổng | Chạy `lsof -i :8000` $\rightarrow$ `kill -9 <PID>` |
| **Client không kết nối được** | Sai IP trong `config.py` hoặc tường lửa chặn | Kiểm tra IP server, tắt tạm firewall: `sudo ufw disable` để kiểm tra |
| **CSDL báo lỗi database disk image is malformed** | Mất điện đột ngột làm hỏng cấu trúc SQLite | Chạy script phục hồi: `sqlite3 messenger.db ".dump" \| sqlite3 restored.db` rồi trỏ sang `restored.db` |
| **WebSocket liên tục bị ngắt kết nối** | Mạng Wi-Fi chập chờn hoặc card mạng sleep mode | Chuyển sang cắm dây LAN cho máy chủ, tắt tính năng tiết kiệm pin card mạng |

---

<a name="an-toan"></a>
## 8. Chính sách an toàn thông tin

1. **Phân vùng mạng:** Đặt máy chủ Server trong dải mạng LAN nội bộ có quyền kiểm soát.
2. **Quyền truy cập thư mục:**
   * File `messenger.db` chỉ cấp quyền đọc/ghi cho user chạy ứng dụng (ví dụ: `chmod 600 messenger.db`).
3. **Bảo mật token:** Thời hạn JWT token là 24 giờ, tự động hết hạn khi quá phiên làm việc.

---

<a name="scripts"></a>
## 9. Các kịch bản tự động hóa hữu ích

### File `backup_cron.sh` (Tự động sao lưu mỗi đêm):
```bash
#!/bin/bash
BACKUP_DIR="/home/newli5737/Desktop/sample/backups"
DB_PATH="/home/newli5737/Desktop/sample/messenger/server/messenger.db"
mkdir -p "$BACKUP_DIR"
sqlite3 "$DB_PATH" ".backup '$BACKUP_DIR/db_$(date +%Y%m%d).db'"
# Xóa các bản sao lưu cũ hơn 14 ngày
find "$BACKUP_DIR" -type f -name "*.db" -mtime +14 -delete
```

---

*Tài liệu hướng dẫn vận hành và bảo trì - Local Messenger 2026*