## Bài thực hành Lab4
### Thiết kế các ca sử dụng cho hệ thống "Payroll System" và giải thích lý do  
**1. Use case "Login"**    
**Mô tả chi tiết**  
1.1. Chức năng  
Xác thực thông tin đăng nhập của người dùng.  

1.2. Mục tiêu  
Xác thực thông tin đăng nhập của người dùng để đảm bảo quyền truy cập hợp lệ vào hệ thống, bảo vệ dữ liệu và điều hướng người dùng đến giao diện chính. 

1.3. Tác nhân   
Any User (Nhân viên/Quản lý/Quản trị viên).  

1.4. Luồng sự kiện  
B1. Người dùng truy cập màn hình đăng nhập.  
B2. Nhập thông tin đăng nhập.  
B3. Hệ thống kiểm tra thông tin:  
3a. Nếu hợp lệ: Hệ thống chuyển người dùng đến dashboard.  
3b. Nếu không hợp lệ: Hệ thống thông báo lỗi.  

1.5. Lý do thiết kế  
- Xác thực người dùng: Chỉ cho phép người dùng hợp lệ truy cập.  
- Bảo vệ dữ liệu: Ngăn chặn truy cập trái phép.  
- Khởi đầu sử dụng hệ thống: Điều kiện để sử dụng các tính năng khác.  
- Hướng dẫn người dùng: Cảnh báo lỗi giúp nhập lại chính xác.  
- Bảo mật nâng cao: Quyền truy cập giới hạn theo vai trò.  

**Sơ đồ Use case**  
Code:
```  
@startuml
actor "Any User" as User
usecase "Login" as UC1
User --> UC1 : Access Login
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aOAIOrwbGcXnQf6IGc8ncC5LMfoQd5YSgg3aav-UcGSHTpRa0iafwEhQWJWALWgEoScfnSKAO3LS3gbvAK0p0G000F__0m00

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aOAIOrwbGcXnQf6IGc8ncC5LMfoQd5YSgg3aav-UcGSHTpRa0iafwEhQWJWALWgEoScfnSKAO3LS3gbvAK0p0G000F__0m00)  
  
**2. Use case "Maintain Timecard"**  
**Mô tả chi tiết**   
2.1. Chức năng  
Quản lý, chỉnh sửa, và lưu trữ thẻ chấm công.  

2.2. Mục tiêu  
Quản lý, chỉnh sửa và lưu trữ thông tin thẻ chấm công, đồng thời hỗ trợ xác minh dữ liệu để đảm bảo tính chính xác và minh bạch trong việc ghi nhận thời gian làm việc.  

2.3. Tác nhân    
- Nhân viên: Trực tiếp thao tác trên thẻ chấm công.  
- Quản lý dự án: Có thể xem và xác minh dữ liệu (nếu cần).  

2.4. Luồng sự kiện  
B1. Người dùng khởi động quy trình Maintain Timecard  
Người dùng chọn chức năng "Quản lý thẻ chấm công" trên giao diện (TimecardForm).  
Hệ thống chuyển yêu cầu đến TimecardController.  
B2. Lấy dữ liệu thẻ chấm công  
TimecardController kiểm tra thẻ chấm công hiện tại thông qua đối tượng Timecard.  
Nếu thẻ chưa tồn tại, một thẻ mới sẽ được tạo.  
Dữ liệu được lấy từ cơ sở dữ liệu (ProjectManagementDatabase).  
B3. Hiển thị thẻ chấm công  
TimecardController gửi dữ liệu về giao diện (TimecardForm).  
Người dùng có thể xem và chỉnh sửa thông tin.  
B4. Cập nhật thẻ chấm công  
Người dùng nhập giờ làm việc hoặc mã charge code (charge numbers).  
Thông tin được gửi lại TimecardController để cập nhật dữ liệu.  
B5. Lưu thẻ chấm công  
Sau khi chỉnh sửa xong, người dùng chọn "Lưu thẻ chấm công".  
TimecardController lưu dữ liệu vào cơ sở dữ liệu thông qua ProjectManagementDatabase.  

2.5. Lý do thiết kế  
- Quản lý hiệu quả: Nhập, chỉnh sửa giờ làm việc và mã charge code dễ dàng, đảm bảo dữ liệu đầy đủ.  
- Minh bạch: Theo dõi thời gian làm việc rõ ràng, giảm sai sót trong tính lương.  
- Tự động hóa: Tạo thẻ mới và hiển thị dữ liệu từ cơ sở dữ liệu tự động.  
- Hỗ trợ quản lý: Quản lý dự án xác minh tính hợp lệ của dữ liệu.  
- Mở rộng: Dễ tích hợp thêm tính năng nhờ thiết kế module hóa.  
- Tối ưu quy trình: Giảm thời gian xử lý, tăng hiệu quả quản lý thẻ chấm công.  

**Sơ đồ Use case**  
Code:
```  
@startuml
actor "Employee" as Employee
actor "Project Manager" as Manager
usecase "Maintain Timecard" as UC1
Employee --> UC1 : Manage Timecard
Manager --> UC1 : Verify Timecard
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aOAIQsv1JdvbQggIGcAn0em3ammeoizAJIvHy4tCIqnFBGAhWRAvIejJanEBKnMKV1Cpyqg0M24aCnSeL9G2LXRgRCW5Cqv1LzSE9A1W1TKDLye5DGr9HLXgKMPQ9KA5GsfU2j2z00000F__0m00

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bTYSab-aOAIQsv1JdvbQggIGcAn0em3ammeoizAJIvHy4tCIqnFBGAhWRAvIejJanEBKnMKV1Cpyqg0M24aCnSeL9G2LXRgRCW5Cqv1LzSE9A1W1TKDLye5DGr9HLXgKMPQ9KA5GsfU2j2z00000F__0m00)  
  
**3. Usse case "Run Payroll"**  
**Mô tả chi tiết**   
3.1. Chức năng  
Tính lương và thực hiện thanh toán cho nhân viên.  

3.2. Mục tiêu  
Tự động hóa quy trình tính lương, đảm bảo thanh toán đúng hạn và chính xác thông qua các phương thức thanh toán linh hoạt.  

3.3. Tác nhân    
- System Clock: Tự động khởi động quy trình tính lương vào ngày trả lương.  
- Bank System: Hỗ trợ xử lý giao dịch chuyển khoản.  
- rinter: In bảng lương hoặc paycheck. Report.     

3.4. Luồng sự kiện    
B1. Khởi động quy trì
SystemClockInterface kiểm tra ngày hiện tại có phải ngày trả lương không.  
Nếu đúng, kích hoạt quy trình tính lương (PayrollController.runPayroll()).  
B2. Lấy dữ liệu lương  
PayrollController:  
- Lấy dữ liệu thẻ chấm công (getTimecard()).  
- Lấy các đơn đặt hàng (Purchase Orders) với nhân viên làm việc theo hoa hồng.  
B3. Tính toán lương  
Tính toán tổng lương cho từng nhân viên, dựa trên:  
- Giờ làm việc trên thẻ chấm công.  
- Hoa hồng từ đơn đặt hàng.  
- Các khoản phụ cấp và khấu trừ.  
B4. Xác định phương thức thanh toán  
PayrollController kiểm tra phương thức thanh toán của từng nhân viên:  
- Chuyển khoản: Gửi thông tin thanh toán đến BankSystem.  
- Paycheck (nhận trực tiếp): Tạo bảng lương và in qua Printer.  
B5. Thực hiện thanh toán  
Gửi lệnh thanh toán đến ngân hàng (nếu là chuyển khoản).  
In paycheck và phân phối (nếu là nhận trực tiếp).  

3.5. Lý do thiết kế    
- Tự động hóa: Tính lương tự động, giảm sai sót và tiết kiệm thời gian.  
- Chính xác: Dựa trên dữ liệu thực tế (Timecard, Purchase Orders).  
- Linh hoạt: Hỗ trợ cả chuyển khoản và paycheck.  
- Tích hợp: Kết nối với Bank System và Printer để đảm bảo quy trình mượt mà.  
- Bảo mật: Xử lý an toàn dữ liệu nhạy cảm.  
- Minh bạch: Báo cáo hoặc paycheck hỗ trợ quản lý rõ ràng.  

**Sơ đồ Use case**  
Code:
```  
@startuml
actor "System Clock" as SystemClock
actor "Bank System" as BankSystem
actor "Printer" as Printer
usecase "Run Payroll" as UC1
SystemClock --> UC1 : Start Payroll Process
BankSystem --> UC1 : Process Payment
Printer --> UC1 : Print Paycheck
@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/L8yz3i8m38NtdCBgte6L0LNq0XKL1x229L3p8yNEqBCnz4XSWIHDHDdytllaPt_Usy22GQ8r2hNu0Dsyif25qNYzT80Ckr5qOwxebkeN9EjTDc8ABoSKIbfd5PaqCa5tYmucN8CtfW3tyQGEBT3tb-p16UPyN6FJ8g-9MVtg3cWDCsp9YQgjVqHoSgwVb7uPo3tItry0003__mC0  

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/L8yz3i8m38NtdCBgte6L0LNq0XKL1x229L3p8yNEqBCnz4XSWIHDHDdytllaPt_Usy22GQ8r2hNu0Dsyif25qNYzT80Ckr5qOwxebkeN9EjTDc8ABoSKIbfd5PaqCa5tYmucN8CtfW3tyQGEBT3tb-p16UPyN6FJ8g-9MVtg3cWDCsp9YQgjVqHoSgwVb7uPo3tItry0003__mC0)  
  
**Sơ đồ Use case cho toàn hệ thống**  
Code:
```  
@startuml
actor "Any User" as User
actor "Employee" as Employee
actor "Project Manager" as Manager
actor "System Clock" as SystemClock
actor "Bank System" as BankSystem
actor "Printer" as Printer

usecase "Login" as UC1
usecase "Maintain Timecard" as UC2
usecase "Run Payroll" as UC3

User --> UC1 : Access Login
Employee --> UC2 : Manage Timecard
Manager --> UC2 : Verify Timecard
SystemClock --> UC3 : Start Payroll Process
BankSystem --> UC3 : Process Payment
Printer --> UC3 : Print Paycheck

@enduml
```  
Link sơ đồ:  https://www.planttext.com/api/plantuml/png/L94zJWCn48NxESLe-nGa7GLAYEY8516W7pb3ME8VP7iBdus28t45REyOByLAC-zzw_4y_tnzRqCa7oUZWLHq7eUTJVWIs0z8eHRDU32VsYNcQhIccKVlFbX5F92bY_miTKDEAKGskDTENQi_2xLlp3tPg-WLAVtSza6ZZJ90Qe0fiAB0E3owosZdc-zlkdoW3EOFdqUJ9NyMPDsHfydYaP9tMekv0IZhusfrLqx3MzmfnI5W7G8j0V7NsPyN_Xi24i22U6K_lgLEB28GQfEfKtcITfkyfIjZeMUnGCKii64RGIBvHsIb-EgTSz2mPNikp_qB003__mC0 

Sơ đồ:  
![Diagram](https://www.planttext.com/api/plantuml/png/L94zJWCn48NxESLe-nGa7GLAYEY8516W7pb3ME8VP7iBdus28t45REyOByLAC-zzw_4y_tnzRqCa7oUZWLHq7eUTJVWIs0z8eHRDU32VsYNcQhIccKVlFbX5F92bY_miTKDEAKGskDTENQi_2xLlp3tPg-WLAVtSza6ZZJ90Qe0fiAB0E3owosZdc-zlkdoW3EOFdqUJ9NyMPDsHfydYaP9tMekv0IZhusfrLqx3MzmfnI5W7G8j0V7NsPyN_Xi24i22U6K_lgLEB28GQfEfKtcITfkyfIjZeMUnGCKii64RGIBvHsIb-EgTSz2mPNikp_qB003__mC0)  
  
