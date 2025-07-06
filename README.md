# Ứng Dụng Gửi File Âm Thanh An Toàn

Ứng dụng web để gửi và nhận file âm thanh an toàn qua mạng LAN với mã hóa và xác thực.

## Tính Năng

- 🔐 **Mã hóa RSA + DES3**: Bảo mật file với khóa công khai/riêng tư
- ✍️ **Chữ ký số**: Xác thực tính toàn vẹn của file và metadata
- 🌐 **Giao diện Web**: Dễ sử dụng với giao diện web hiện đại
- 📡 **Kết nối LAN**: Có thể gửi file cho người dùng trong cùng mạng LAN
- 📋 **Log chi tiết**: Theo dõi quá trình gửi/nhận file
- 🎵 **Hỗ trợ nhiều định dạng**: MP3, WAV, FLAC, AAC, OGG, M4A

## Cài Đặt

### Yêu cầu hệ thống
- Python 3.7+
- Thư viện: Flask, pycryptodome

### Cài đặt thư viện
```bash
pip install flask pycryptodome
```

### Chuẩn bị khóa
Đảm bảo có các file khóa sau trong thư mục:
- `sender_private.pem` - Khóa riêng tư của người gửi
- `receiver_public.pem` - Khóa công khai của người nhận
- `receiver_private.pem` - Khóa riêng tư của người nhận  
- `sender_public.pem` - Khóa công khai của người gửi

## Sử Dụng

### 1. Khởi động Receiver (Người nhận)

```bash
python receiver_web.py
```

Receiver sẽ chạy trên:
- **URL**: http://localhost:5001
- **Port socket**: 12345

### 2. Khởi động Sender (Người gửi)

```bash
python sender_web.py
```

Sender sẽ chạy trên:
- **URL**: http://localhost:5000

### 3. Kết nối qua mạng LAN

#### Trên máy Receiver:
1. Mở trình duyệt và truy cập: `http://[IP_LOCAL]:5001`
2. Nhấn "Bắt Đầu Lắng Nghe"
3. Ghi nhớ địa chỉ IP hiển thị (ví dụ: 192.168.1.100)

#### Trên máy Sender:
1. Mở trình duyệt và truy cập: `http://[IP_LOCAL]:5000`
2. Nhập địa chỉ IP của Receiver vào ô "Địa chỉ IP Receiver"
3. Nhấn "Thiết Lập IP"
4. Chọn file âm thanh cần gửi
5. Nhấn "Bắt Đầu Kết Nối"
6. Sau khi kết nối thành công, nhấn "Gửi File"

## Cách Tìm IP Local

### Windows:
```cmd
ipconfig
```
Tìm dòng "IPv4 Address" trong adapter mạng đang sử dụng.

### macOS/Linux:
```bash
ifconfig
# hoặc
ip addr show
```

## Cấu Trúc File

```
btl2/
├── sender_web.py          # Server web cho người gửi
├── receiver_web.py        # Server web cho người nhận
├── templates/
│   ├── sender.html        # Giao diện người gửi
│   └── receiver.html      # Giao diện người nhận
├── sender_private.pem     # Khóa riêng tư sender
├── receiver_public.pem    # Khóa công khai receiver
├── receiver_private.pem   # Khóa riêng tư receiver
├── sender_public.pem      # Khóa công khai sender
└── README.md
```

## Bảo Mật

- **Mã hóa RSA**: Bảo vệ khóa phiên (session key)
- **Mã hóa DES3**: Mã hóa nội dung file
- **Chữ ký SHA512**: Xác thực tính toàn vẹn
- **Xác thực metadata**: Đảm bảo thông tin file không bị giả mạo

## Xử Lý Lỗi

### Lỗi kết nối:
- Kiểm tra firewall Windows
- Đảm bảo cả 2 máy trong cùng mạng LAN
- Kiểm tra địa chỉ IP chính xác

### Lỗi khóa:
- Đảm bảo các file .pem tồn tại
- Kiểm tra quyền đọc file khóa

### Lỗi port:
- Đảm bảo port 12345 không bị sử dụng bởi ứng dụng khác
- Thay đổi port trong code nếu cần

## Ghi Chú

- File được chia thành 3 đoạn để gửi
- Mỗi đoạn được mã hóa và ký riêng biệt
- File nhận được sẽ được lưu trong thư mục hiện tại
- Log chi tiết được hiển thị trong giao diện web
Kết Quả Chạy Chương Trình

Dưới đây là ảnh chụp màn hình minh họa quá trình gửi và nhận file âm thanh an toàn thông qua giao diện web:

Giao diện Người Gửi :
![Sender_web](https://github.com/bac-debug/Du-an-gui-file-an-toan/blob/main/Screenshot%202025-07-06%20165517.png)
Giao diện Người Nhận khi nhận file :
![Receiver_web](https://github.com/bac-debug/Du-an-gui-file-an-toan/raw/main/Screenshot%202025-07-06%20165504.png)
