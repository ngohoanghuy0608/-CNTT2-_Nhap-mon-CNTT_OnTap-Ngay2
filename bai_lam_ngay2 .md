# BÀI LÀM – ÔN TẬP NGÀY 2

- **Họ tên:Ngo Hoang Huy**
- **Lớp:CNTT2**
- **Link repository:**
- **Hệ điều hành (Windows/macOS):windows**

## Bài 1. Lọc log thủ công

### Lệnh đã chạy

```shell
PS C:\Users\ACER\Documents\Downloads\starter-kit(1)\starter-kit\trung-tam-tieng-anh> Get-Content .\logs\access.log | Select-String "ERROR" > .\logs\error_report.txt
PS C:\Users\ACER\Documents\Downloads\starter-kit(1)\starter-kit\trung-tam-tieng-anh> Get-Content .\logs\error_report.txt
PS C:\Users\ACER\Documents\Downloads\starter-kit(1)\starter-kit\trung-tam-tieng-anh> Get-Content .\logs\error_report.txt | Select-Object -First 2
```

### 2 dòng lỗi đầu tiên trong error_report.txt

```text

2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)
```

## Bài 2. Đếm bằng pipeline
### Lệnh

```shell

PS C:\Users\ACER\Documents\Downloads\starter-kit(1)\starter-kit\trung-tam-tieng-anh> \Get-Content .\logs\access.log | Select-String "WARNING" | Measure-Object | Select-Object -ExpandProperty Count
PS C:\Users\ACER\Documents\Downloads\starter-kit(1)\starter-kit\trung-tam-tieng-anh> Get-Content .\logs\payment.log | Select-String "ERROR" | Measure-Object | Select-Object -ExpandProperty Count
```

### Kết quả đếm (Windows: giá trị Count; macOS: con số in ra)

```text
WARNING trong access.log: 4
ERROR trong payment.log: 3
```

## Bài 3. Chạy script auto_warning (.ps1 hoặc .sh)

### Lệnh chạy (Windows: nếu dùng Phụ lục 2 thì ghi cả 2 lệnh)

```shell
notepad .\auto_warning.ps1
.\auto_warning.ps1
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
.\auto_warning.ps1
Get-Content .\logs\warning_report.txt
```

### Nội dung file logs/warning_report.txt

```text
2025-10-18 09:19:13 [WARNING] Cong thanh toan phan hoi cham
2025-10-18 09:28:16 [WARNING] Nhieu lan nhap sai ma OTP
2025-10-18 09:43:01 [WARNING] So du vi gan bang hoc phi
2025-10-18 09:46:22 [WARNING] So du vi gan bang hoc phi
2025-10-18 09:49:43 [WARNING] So du vi gan bang hoc phi

```

## Bài 4. Báo cáo tổng hợp

### Các lệnh đã chạy

```shell
"=== TONG HOP ACCESS LOG ===" | Set-Content .\logs\tong_hop_ngay2.txt -Encoding UTF8
Get-Content .\logs\access.log | Select-String "ERROR" | ForEach-Object { $_.Line } | Add-Content .\logs\tong_hop_ngay2.txt -Encoding UTF8
(Get-Content .\logs\payment.log | Select-String "WARNING" | Measure-Object).Count | Add-Content .\logs\tong_hop_ngay2.txt
Get-Content .\logs\tong_hop_ngay2.txt

```

### Nội dung file logs/tong_hop_ngay2.txt

```text
=== TONG HOP ACCESS LOG ===
2025-10-18 08:17:59 [ERROR] Khong tim thay trang /lich-thi (404)
2025-10-18 08:25:55 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:33:51 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:37:19 [ERROR] Ket noi may chu du lieu that bai
2025-10-18 08:49:43 [ERROR] Het thoi gian cho (timeout)
2025-10-18 08:53:11 [ERROR] Het thoi gian cho (timeout)

```

## Bài 5. Câu hỏi ngắn

- **a) ">" Ghi kết quả vào file, nếu file đã tồn tại thì ghi đè nội dung cũ. Còn ">>" Ghi nối kết quả vào cuối file, giữ nguyên nội dung đã có.**

- **b)Nếu lệnh thứ hai dùng > thay cho >>, nội dung cũ trong tong_hop_ngay2.txt sẽ bị ghi đè. File chỉ còn các dòng ERROR lấy từ access.log, dòng tiêu đề ban đầu sẽ mất. Nếu lệnh thứ ba vẫn dùng >>, số lượng WARNING sẽ được nối vào cuối các dòng ERROR.**

- **c)Nên dùng đường dẫn tương đối như .\logs\payment.log vì script có thể chạy trên nhiều máy khi giữ nguyên cấu trúc thư mục dự án. Đường dẫn tuyệt đối như C:\Users\An\Desktop\... phụ thuộc vào tên tài khoản và vị trí lưu file của từng máy, nên dễ bị lỗi khi chuyển sang máy khác.**

## Tự chấm (điền sau khi có đáp án)

- **Điểm tự chấm:** ..../100
- **Lỗi mình đã mắc và cách sửa:**
