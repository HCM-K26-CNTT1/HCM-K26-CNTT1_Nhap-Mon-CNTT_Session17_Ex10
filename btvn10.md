# BÀI 10: ĐÁNH GIÁ ĐA GIẢI PHÁP QUẢN TRỊ HỆ SINH THÁI EXTENSIONS CHO BÁC SĨ

## Phần 1. Đề xuất 2 giải pháp kỹ thuật

### 1. Giải pháp 1: Mô hình mở và tự do

Cho phép nhân viên tự cài đặt mọi tiện ích từ Chrome Web Store và giữ quyền truy cập mặc định `On all sites`.

**Ưu điểm:**
- Dễ cài đặt và sử dụng.
- Tiện ích tự hoạt động trên các trang web.
- Nhân viên có thể chọn công cụ theo nhu cầu.

**Nhược điểm:**
- Tiện ích có thể đọc thông tin bệnh nhân trên nhiều trang web.
- Nhiều tiện ích chạy nền làm tốn RAM.
- Khó kiểm soát tiện ích giả mạo hoặc chứa mã độc.

### 2. Giải pháp 2: Mô hình chuẩn hóa và giới hạn quyền

Phòng khám lập danh sách Whitelisted Extensions, chỉ cho phép cài đặt các tiện ích đã được kiểm tra.

Cách thực hiện:
- Chỉ cài tiện ích có nguồn gốc rõ ràng và được kiểm duyệt.
- Ưu tiên tiện ích sử dụng Manifest V3.
- Đặt quyền Site Access là `On click` hoặc `Only on specific sites`.
- Chỉ cấp quyền trên trang cần thiết, ví dụ `*.carepulse.vn`.
- Tắt hoặc gỡ bỏ tiện ích không cần thiết để giảm RAM.

**Ưu điểm:**
- Hạn chế nguy cơ rò rỉ dữ liệu bệnh nhân.
- Giảm số tiện ích chạy nền.
- Dễ quản lý và kiểm soát máy tính của nhân viên.

**Nhược điểm:**
- Nhân viên cần thêm thao tác khi sử dụng tiện ích.
- Bộ phận CNTT phải kiểm tra và quản lý danh sách tiện ích.

---

## Phần 2. So sánh và lựa chọn giải pháp (Trade-off)

### 3. Bảng so sánh hai giải pháp

| Tiêu chí | Giải pháp 1: Mở tự do | Giải pháp 2: Chuẩn hóa |
|---|---|---|
| 1. Bảo mật dữ liệu bệnh nhân | Rất thấp, tiện ích có thể đọc dữ liệu trên nhiều trang | Cao hơn, quyền truy cập được giới hạn |
| 2. RAM và tốc độ | Tốn RAM do nhiều tiện ích chạy nền | Tiết kiệm RAM nhờ giảm và kiểm soát tiện ích |
| 3. Độ tiện lợi | Cao, tiện ích tự hoạt động | Trung bình, đôi khi cần click để cấp quyền |
| 4. Nguy cơ tiện ích độc hại | Cao, khó kiểm soát | Thấp hơn nhờ danh sách được kiểm duyệt |

**Lưu ý về Manifest V3:**

Manifest V3 là phiên bản kiến trúc mới của Chrome Extensions, giúp quản lý quyền truy cập và hoạt động nền chặt chẽ hơn. Tuy nhiên, sử dụng Manifest V3 không có nghĩa là tiện ích chắc chắn an toàn.

**Bẫy phân quyền:**

Nếu bác sĩ đồng ý cho tiện ích dịch thuật quyền `Read and change all your data on all websites that you visit`, tiện ích có thể đọc hoặc thay đổi dữ liệu trên các trang web đã truy cập, tùy theo quyền được cấp.

Khi bác sĩ nhập thông tin xét nghiệm, tiện ích độc hại có thể lấy cắp nội dung biểu mẫu và gửi ra bên ngoài. Điều này có thể làm lộ thông tin bệnh án và dữ liệu cá nhân của bệnh nhân.

### 4. Quyết định lựa chọn

CarePulse nên chọn **Giải pháp 2: Chuẩn hóa và giới hạn quyền truy cập**.

Lý do:
- Hồ sơ bệnh án là dữ liệu rất nhạy cảm, cần được bảo vệ nghiêm ngặt.
- Hạn chế quyền của Extension giúp giảm nguy cơ đọc trộm thông tin.
- Giảm số lượng tiện ích chạy nền giúp tiết kiệm RAM cho máy tính 8GB.
- Danh sách Whitelist giúp phòng khám dễ kiểm soát phần mềm được cài đặt.

Mặc dù nhân viên cần thêm thao tác khi sử dụng, nhưng bảo vệ thông tin bệnh nhân và đảm bảo an toàn trong quá trình khám chữa bệnh quan trọng hơn sự tiện lợi.

---

## Phần 3. Quy trình triển khai

### 5. Quy trình 4 bước quản lý Extension trên Chrome

**Bước 1: Kiểm tra tiện ích đã cài đặt**

- Mở Chrome và nhập `chrome://extensions`.
- Xem danh sách tất cả tiện ích đang được cài đặt.
- Kiểm tra tên, nguồn cài đặt và quyền truy cập của từng tiện ích.

**Bước 2: Gỡ bỏ tiện ích không an toàn**

- Xác định tiện ích không rõ nguồn gốc hoặc không phục vụ công việc.
- Nhấn Remove để gỡ bỏ.
- Chỉ giữ lại các tiện ích đã được phòng khám phê duyệt.

**Bước 3: Thiết lập lại quyền truy cập**

- Chọn Details tại tiện ích cần cấu hình.
- Tìm mục Site Access.
- Chọn `On click` hoặc `On specific sites`.
- Chỉ cho phép truy cập các trang cần thiết như `*.carepulse.vn`.
- Không cấp quyền truy cập tất cả trang web nếu không thực sự cần thiết.

**Bước 4: Kiểm tra và theo dõi**

- Khởi động lại Chrome và kiểm tra các tiện ích còn hoạt động.
- Kiểm tra RAM bằng Chrome Task Manager (`Shift + Esc`).
- Theo dõi hiệu năng máy tính.
- Định kỳ rà soát và gỡ bỏ tiện ích không còn sử dụng.

---

## Phần 4. Tổng kết cuối bài

Qua bài tập, em hiểu rằng cài đặt nhiều Extension giúp công việc thuận tiện hơn nhưng cũng làm tăng nguy cơ mất an toàn dữ liệu và tiêu tốn RAM.

Đối với CarePulse, em lựa chọn mô hình chuẩn hóa Extension, chỉ sử dụng tiện ích được kiểm duyệt và giới hạn quyền truy cập. Đây là cách phù hợp để bảo vệ thông tin bệnh nhân và giúp máy tính phòng khám hoạt động ổn định hơn.