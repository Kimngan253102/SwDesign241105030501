## Bài thực hành Lab5
## 1. Authentication System (Hệ thống Xác thực)

**Yêu cầu chức năng**: Quản lý đăng nhập và xác thực người dùng.  

**Yêu cầu phi chức năng**:  
- Đảm bảo bảo mật cao (mã hóa mật khẩu).  
- Thời gian phản hồi < 2 giây.  

**Thành phần**:  
- **LoginController**: Xử lý yêu cầu đăng nhập và kiểm tra tính hợp lệ của thông tin người dùng.  
- **UserManager**: Quản lý thông tin người dùng (username, password).  
- **AuthenticationService**: Xác thực thông tin đăng nhập của người dùng, cung cấp token JWT.  

**Tương tác**:  
- Cung cấp token JWT để các hệ thống con khác có thể xác thực người dùng.  
- **RBAC System** kiểm tra vai trò của người dùng dựa trên token.  

---

## 2. Timecard Management System (Hệ thống Quản lý Thẻ chấm công)

**Yêu cầu chức năng**: Quản lý thẻ chấm công của nhân viên.  

**Yêu cầu phi chức năng**:  
- Hỗ trợ tải dữ liệu thẻ chấm công nhanh chóng (< 2 giây).  
- Đảm bảo độ chính xác trong việc ghi nhận và lưu trữ thời gian làm việc.  

**Thành phần**:  
- **TimecardController**: Xử lý yêu cầu từ giao diện người dùng.  
- **TimecardService**: Quản lý logic cập nhật thẻ chấm công.  
- **TimecardRepository**: Tương tác với cơ sở dữ liệu để lưu trữ và truy xuất dữ liệu thẻ chấm công.  

**Tương tác**:  
- Lấy thông tin từ **Authentication System** để xác định người dùng.  
- Gửi dữ liệu chấm công đến **Payroll Processing System** để tính toán lương.  

---

## 3. Payroll Processing System (Hệ thống Xử lý Lương)

**Yêu cầu chức năng**: Tính toán và xử lý lương cho nhân viên.  

**Yêu cầu phi chức năng**:  
- Tính toán nhanh và chính xác.  
- Đảm bảo thanh toán lương đúng hạn.  

**Thành phần**:  
- **PayrollController**: Quản lý yêu cầu tính toán lương từ người dùng.  
- **PayrollCalculator**: Tính toán lương dựa trên các yếu tố như giờ làm việc, hoa hồng, và phụ cấp.  
- **PaymentService**: Xử lý các phương thức thanh toán (chuyển khoản ngân hàng hoặc paycheck).  
- **ReportGenerator**: Tạo bảng lương và các báo cáo liên quan.  

**Tương tác**:  
- Lấy dữ liệu từ **Timecard Management System** để tính toán lương.  
- Gửi yêu cầu thanh toán đến **Payment System**.  
- Gửi báo cáo lương đến **Reporting System**.  

---

## 4. Payment System (Hệ thống Thanh toán)

**Yêu cầu chức năng**: Thực hiện thanh toán lương cho nhân viên.  

**Yêu cầu phi chức năng**:  
- Đảm bảo thanh toán thành công trong vòng 5 giây.  
- Kết nối an toàn với ngân hàng qua HTTPS/TLS.  

**Thành phần**:  
- **BankInterface**: Kết nối với ngân hàng để thực hiện chuyển khoản thanh toán.  
- **PrintService**: In paycheck nếu nhân viên chọn nhận tiền mặt thay vì chuyển khoản.  

**Tương tác**:  
- Nhận yêu cầu thanh toán từ **Payroll Processing System**.  
- Kết nối với ngân hàng để thực hiện giao dịch thanh toán.  
- Gửi xác nhận thanh toán đến **Notification System**.  

---

## 5. Reporting System (Hệ thống Báo cáo)

**Yêu cầu chức năng**: Tạo báo cáo về lương, thời gian làm việc và các hoạt động khác.  

**Yêu cầu phi chức năng**:  
- Báo cáo cần được tạo trong vòng 10 giây.  
- Hỗ trợ xuất báo cáo dưới nhiều định dạng (PDF, Excel, CSV).  

**Thành phần**:  
- **ReportController**: Quản lý yêu cầu báo cáo từ người dùng.  
- **ReportService**: Tạo báo cáo tổng hợp từ các dữ liệu của hệ thống.  
- **ExportService**: Xuất báo cáo dưới dạng các định dạng (PDF, Excel, CSV).  

**Tương tác**:  
- Lấy dữ liệu từ **Timecard Management System** và **Payroll Processing System** để tạo báo cáo.  
- Cung cấp báo cáo cho các bộ phận liên quan như Quản lý, Kế toán.  

---

## 6. Scheduler System (Hệ thống Lập lịch)

**Yêu cầu chức năng**: Tự động khởi chạy các quy trình định kỳ như tính lương, tạo báo cáo.  

**Yêu cầu phi chức năng**:  
- Đảm bảo độ trễ của các job định kỳ < 1 phút.  
- Cấu hình dễ dàng và hỗ trợ lịch trình linh hoạt.  

**Thành phần**:  
- **SystemClockInterface**: Xác định thời gian và ngày trả lương.  
- **JobScheduler**: Kích hoạt các quy trình như tính lương, tạo báo cáo.  

**Tương tác**:  
- Kích hoạt **Payroll Processing System** vào ngày trả lương.  
- Gửi thông báo nhắc nhở chấm công cho nhân viên qua **Notification System**.  

---

### Kết luận

Các hệ thống con trong Payroll System đều có vai trò quan trọng, từ xác thực người dùng, quản lý thẻ chấm công, tính toán lương, cho đến thanh toán và báo cáo. Các hệ thống này tương tác với nhau thông qua các API và các giao thức bảo mật, đảm bảo tính chính xác, bảo mật và hiệu quả trong việc quản lý thông tin lương, thời gian làm việc, và thanh toán cho nhân viên.
