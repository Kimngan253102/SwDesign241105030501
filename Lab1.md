# Lab1 - PHÂN TÍCH KIẾN TRÚC, CƠ CHẾ, CA SỬ DỤNG

## 1. Phân tích kiến trúc
### 1.1. Đề xuất Kiến trúc
#### 1.1.1 Kiến trúc Tổng thể
- Client-Server Architecture: Sử dụng mô hình kiến trúc client-server để phân tách các yêu cầu của người dùng và các dịch vụ xử lý dữ liệu. Nhân viên sẽ sử dụng ứng dụng trên máy tính để bàn để gửi thông tin, và hệ thống sẽ xử lý dữ liệu trên máy chủ.

#### 1.1.2 Thành phần Kiến trúc
#### 1.1.2.1 Client Layer:
- Windows Desktop Application: Giao diện cho nhân viên nhập thông tin như thời gian làm việc, đơn hàng, và tùy chọn thanh toán. Giao diện thân thiện và dễ sử dụng.
Reporting Module: Cung cấp khả năng truy vấn và tạo báo cáo cho nhân viên về giờ làm việc, số tiền đã nhận, và thời gian nghỉ còn lại.

#### 1.1.2.2 Business Logic Layer:
- Payroll Processing Engine: Chịu trách nhiệm tính toán tiền lương, xử lý các yêu cầu của nhân viên và tạo báo cáo. Đảm bảo rằng lương được thanh toán chính xác và đúng hạn.
- Timecard Management: Quản lý việc ghi nhận thời gian làm việc của nhân viên, kiểm tra tính hợp lệ và lưu trữ dữ liệu.
- Commission Calculation: Tính toán hoa hồng cho nhân viên có lương cơ bản.
  
#### 1.1.2.3 Data Access Layer:
- Employee Database: Cơ sở dữ liệu chứa thông tin nhân viên, giờ làm việc, và đơn hàng. Cung cấp chức năng thêm, xóa và sửa thông tin nhân viên.
- Project Management Database (DB2): Kết nối tới cơ sở dữ liệu hiện tại để lấy thông tin về dự án và charge numbers mà không cập nhật dữ liệu.
  
#### 1.1.2.4 Integration Layer:
- Payment Processing Module: Tích hợp với các phương thức thanh toán như chuyển khoản ngân hàng và gửi thư. Đảm bảo rằng thanh toán được thực hiện đúng phương thức mà nhân viên chọn.

#### 1.2. Biểu đồ Package
![Diagram](https://www.planttext.com/api/plantuml/png/Z9HDRi8m48NtESM8FLUe-5MB12e2MjPJPuZSE9x8Tbf55IVheaVg5Ug400aaK2_Z6RzltZpbz_jdO1qQboKgI574617qnagITZ37d4mFlWBmHoYq5dfRgKF-j30X6pjEOPYcIWfqalMniZXzc2Qfufm89kWGfjgPl7QxefIDWqVIPChcycuVx8CpnIYpKfCNdNCaHIlD4dF3Ii7IiF2LKaTUAV9TJPOnAf4fT0HhLDW0gGW8_5EmLZAr5KbTPYCJ4cX2MA3sQ8atfodmYag6nIjRDd51ySIPiRM2jMD3Vch19cnJ67EII3y0wnFibQFdAMhLEpOdgssBYQNxGo5A7riSRApf3Us5SmVkKz5CxxXEj7gPm7DQhR1jBh-OTnAkPbo7q8gSaVH1SEmeobhccMb7qK6lAn6bIYqH2mupTI4tGXt3ng2sEpArxmkK2getpkgtKz_lFznAud-wsm8Mt4ftsNMzkw0zgWV26wkuhzKHqA0pkPs4zvIwDnWCI8V5Z-eF003__mC0)

## 2. Cơ chế phân tích
### 2.1. Đề xuất Cơ chế
### 2.1.1 Quản lý Thời gian làm việc:
- Giải thích: Cơ chế này cho phép nhân viên ghi nhận và chỉnh sửa thời gian làm việc của mình trong một khoảng thời gian nhất định. Điều này đảm bảo tính chính xác trong việc thanh toán.
### 2.1.2 Tính toán Tiền lương:
- Giải thích: Tính toán lương cho cả nhân viên theo giờ và lương cố định, bao gồm việc tính toán lương ngoài giờ cho nhân viên làm việc trên 8 giờ.

### 2.1.3 Quản lý Hoa hồng:
- Giải thích: Tính toán hoa hồng cho nhân viên có lương cố định dựa trên doanh thu từ đơn hàng. Cơ chế này đảm bảo nhân viên được thưởng công bằng dựa trên hiệu suất làm việc.

### 2.1.4 Tích hợp Cơ sở dữ liệu:
- Giải thích: Kết nối tới cơ sở dữ liệu dự án hiện tại để lấy thông tin charge numbers mà không cần phải thay thế hệ thống hiện tại. Điều này giảm thiểu chi phí và rủi ro.

### 2.1.5 Chọn Phương thức Thanh toán:
- Giải thích: Cho phép nhân viên lựa chọn giữa các phương thức thanh toán khác nhau (mail, chuyển khoản, hoặc nhận trực tiếp). Đảm bảo tính linh hoạt cho nhân viên.

### 2.1.6 Báo cáo cho Nhân viên:
- Giải thích: Cung cấp khả năng truy vấn và tạo báo cáo cho nhân viên về giờ làm việc, tổng tiền đã nhận và thời gian nghỉ còn lại. Điều này giúp nhân viên theo dõi thông tin của họ một cách dễ dàng.

### 2.1.7 Tự động hóa Quy trình Thanh toán:
- Giải thích: Thiết lập quy trình thanh toán tự động hàng tuần và vào cuối tháng, giúp giảm thiểu sự can thiệp của con người và tăng tính chính xác.

### 2.2. Kết quả Mong đợi
- Danh sách các cơ chế phù hợp sẽ hỗ trợ trong việc phát triển hệ thống payroll mới, đảm bảo tính chính xác, an toàn, và dễ sử dụng cho nhân viên và quản trị viên.

## 3. Phân tích ca sử dụng Payment
### 3.1. Xác định các lớp phân tích
#### 3.1.1. Các lớp chính
- **Employee**
  - Nhiệm vụ: Đại diện cho nhân viên trong hệ thống, có khả năng chọn phương thức thanh toán.
  - Thuộc tính: employeeID, name, paymentMethod, address, bankName, accountNumber.
    
- **PaymentMethod**
  - Nhiệm vụ: Đại diện cho các phương thức thanh toán có sẵn cho nhân viên.
  - Thuộc tính: methodID, methodName (pick-up, mail, direct deposit).
    
- **PaymentService**
  - Nhiệm vụ: Xử lý các yêu cầu liên quan đến việc chọn phương thức thanh toán và cập nhật thông tin nhân viên.
  - Thuộc tính: None.

### 3.2. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/T5AxJiCm5Dtz5LVi_O58GPLQ92GUGe81HjUniANM3ebJAJC30s9WPA91GeWA10CBoT31gF_XB-0Ni9EwDAKirtPqphdddfllQjPD5KvKDXeYJ9HCO6SK3sLEAOhjPqvuZ8M2hIESZwXGnpGPSqAt0AUmk6_47L35P5J3cciRvNlqiS83d3Pw_e5G6C8UCzKzXwzRKzs9SxZ8Sb29VX4CmX1vEdIslOi0plGq0sBA9rij-KP0pERlyyAobNq_4tjWorTI5m8jQ4wXCHZ0lYaVSuWS9jK5OK1iNHT1g853PxLt_vVq1s-7EMJwGS2OwwdupvkTQiMI7p20NMwgIr6ZhbUzAVsPBxGsnz7RsAUsqpFbQmo2sKF1M4yaa7a1gGqS8bEzmT3slChMBFdj16swOlh3gNFHYjUZsp6Tka1hed2RMgeq6pVbhDOhoTgwbovQoPmqdGUwaC2adZW3jZBKfI9ol_CF0000__y30000)
  
### 3.3 Quan hệ giữa các lớp
- Employee có một phương thức thanh toán PaymentMethod.
- PaymentService xử lý việc chọn phương thức thanh toán và cập nhật thông tin cho Employee.
  
### 3.4. Biểu đồ lớp
 ![Diagram](https://www.planttext.com/api/plantuml/png/X5DBJiCm4Dtd55PM1OaAjXQgYYWIbQ2gL2umiKV14DkLFOduY9Enu4XS0UTRfn6GHQ9vCnc_Ds_y_Vcrz0IEIbqa_bcPFJZGJ1JW_HMHKrb9k1RMxDGRilCaQJBiHkyB-uh8tXDMFzZ5wnLdob0B6j38cGzDJDuYpXP7I67p7ENQx0Yez9nbDfI0QPCWvOFIAC396GdE-k24iyegcNpqTFf4JuUwU4IdaRa22WpgTqVSo6F8bvbMH3XDT1nZ_cG9YbjREX-T52Yft5m_Wijn9feFPssuANM6RY8WJlOYH8IDXEoTVK91cybueG9LG5PWH6WuOjl-TGy6SjHewb501dxmC9XiGe6oWnaZwp04M67CrC-2a3lbwJ965rDVTkWg9OQJDBmq3BVe-aMAVO8A_xGzSkc_zHZsDBr8sTdPWgMdwM5RU61IJyCd0nJNZKpXOGB2EdcexKNDvukuPN17eFSuBQpx_ku27qRicGnWiWoxMT_A7m000F__0m00)
 
### 3.5. Giải thích
 - Nhân viên (Nhân viên): Quản lý và bổ sung các thẻ thời gian ( Timecard ).
- Timecard : Ghi nhận thông tin về số giờ làm việc, trạng thái và liên kết với nhiều ChargeNumber để ghi nhận chi tiết dự án mà nhân viên đã tham gia.
- ChargeNumber : Giao diện cho các dự án mã hóa, cung cấp thông tin về thời gian làm việc được phân bổ cho các dự án cụ thể.
- TimecardService : Dịch vụ xử lý các thao tác liên quan đến thẻ thời gian như lưu và gửi thẻ lên hệ thống.
## 4. Phân tích ca sử dụng Maintain Timecard
### 4.1. Xác định các lớp phân tích
### 4.1.1. Các lớp chính
- **Employee**
  - Nhiệm vụ: Đại diện cho người sử dụng hệ thống, có khả năng nhập và gửi thông tin thời gian.
  - Thuộc tính: employeeID, name, role, loggedInStatus.
    
- **Timecard**
Nhiệm vụ: Lưu trữ thông tin thời gian làm việc của nhân viên cho từng kỳ trả lương.
  - Thuộc tính: timecardID, employeeID, startDate, endDate, submittedDate, status, totalHours.
    
- **ChargeNumber**
  - Nhiệm vụ: Đại diện cho các dự án mà nhân viên có thể ghi nhận giờ làm việc.
  - Thuộc tính: chargeNumberID, projectName, availableHours.

- **ProjectManagementDatabase**
  - Nhiệm vụ: Cung cấp danh sách charge numbers cho hệ thống.
  - Thuộc tính: connectionStatus.
    
- **TimecardService**
- Nhiệm vụ: Xử lý các thao tác liên quan đến thời gian làm việc của nhân viên (lưu, gửi).
  - Thuộc tính: maxHoursPerEmployee.
    
### 4.2. Biểu đồ Sequence
 ![Diagram](https://www.planttext.com/api/plantuml/png/R95DJiGm38NtFeNL_LoW2pIqPGS8qRc0ctY6eFoKnAaqPsF1aRW2dM62MjIidkBFpy_9z-VNFWb5oSu2AGaH7znemvaPnldQA3EI5wmEnh6Yg7kEar5S8IMywJNu4iCxAtaYJoTsxAKZeO7IRqlNRDjM06KkxkwASurjP1B6Wi6jS66wfiPN_iYS1DitYYT-pcxWY8yc2NGDxfP6Swp9QDuWWQpWlTQhKWASps9QIL1VKPUjcD7olnxs6c2pgQTfiKKHwuXjy4SJtPLTsPINgVySiC-3CocPu6Uf5ATqp1RsSu3BH_u0003__mC0)
 
### 4.3. Quan hệ giữa các lớp
- Employee có một hoặc nhiều Timecard.
- Timecard chứa một hoặc nhiều ChargeNumber.
- ProjectManagementDatabase cung cấp danh sách ChargeNumber cho Timecard.
- TimecardService tương tác với Timecard và ProjectManagementDatabase để thực hiện các thao tác.
  
### 4.4. Biểu đồ lớp
 ![Diagram](https://www.planttext.com/api/plantuml/png/V5DBJiCm4Dtd5ADiA4YLO1kXgeWYKGagKBd0n1cbXjY9x4aG8DOSWXKdu01PiE0aFG5Nm6a-JLjA5f7c-SrxapVEJ_arjeo6SvLuza7g30qg40bQUyPiP9WpJKMgv_APuDZpLYTmeR8aVIA25m-gXvfwEWb0Qgv1ZOe2i4v4npLYqcIDlBPYTrAHG1ErOjpK6sAh8IV8hhzwDxOwseOuPKmkqzpOkhbpEL-WYMcMgv1CwoHws8PRPj9x4ZpR-G8iK2OO9lINnKtTTOqQOrAagtanHDl551Ftnx23mm2kfENJFZhQJMPEff2Yax5OK7iqO15qF2TNf39gM7ce9F_BSqO7S9kZXiMoV8DOBijF1F7z8I1Pbk-Pr-tPF_5XE1o1V-IlznL0-gYjrzLzqaRS0RWRn2WTUNz6LMTFsgsWa16jvTiGjdXk0sHGyD_4_NRzJc_iRbBr1_m2003__mC0)
 
### 4.5. Giải thích
- Employee là người tương tác với hệ thống để quản lý thời gian làm việc.
- Timecard lưu giữ tất cả thông tin liên quan đến thời gian làm việc của nhân viên cho một kỳ trả lương nhất định.
- ChargeNumber cho phép nhân viên ghi nhận giờ làm việc theo các dự án cụ thể.
- ProjectManagementDatabase cung cấp dữ liệu cần thiết cho hệ thống.
- TimecardService thực hiện các thao tác cần thiết cho việc xử lý thời gian làm việc và đảm bảo các quy tắc nghiệp vụ được tuân thủ.

## 5. Hợp nhất kết quả phân tích
### 5.1. Hợp Nhất 2 Ca Sử Dụng: Select Payment Method và Maintain Timecard
#### 5.1.1. Các Lớp
- Employee: Là lớp trung tâm trong cả hai ca sử dụng, chứa thông tin của nhân viên và liên kết với cả Timecard và PaymentMethod.
- TimecardService và PaymentService: Hai dịch vụ này chịu trách nhiệm xử lý yêu cầu và cập nhật thông tin cho nhân viên.

#### 5.1.1.2. Luồng Hoạt Động Chung
- Nhân viên đăng nhập vào hệ thống.
- Nhân viên có thể chọn giữa việc duy trì thẻ thời gian hoặc lựa chọn phương thức thanh toán.
- Dữ liệu của nhân viên sẽ được cập nhật dựa trên các hành động mà họ thực hiện trong từng ca sử dụng.

### 5.2. Giới thiệu
- Tài liệu mô tả hai ca sử dụng chính trong hệ thống quản lý nhân viên: "Select Payment Method" và "Maintain Timecard."

### 5.3. Ca Sử Dụng 1: Select Payment Method
#### 5.3.1. Mô tả
- Cho phép nhân viên chọn phương thức thanh toán cho lương (nhận tiền mặt, qua thư, hoặc chuyển khoản).

#### 5.3.2. Luồng Sự Kiện
- Nhân viên yêu cầu chọn phương thức thanh toán.
- Hệ thống hiển thị các tùy chọn.
- Nhân viên chọn phương thức và cung cấp thông tin cần thiết.
- Hệ thống cập nhật thông tin thanh toán.
#### 5.3.3. Các Lớp Phân Tích
- Employee
- PaymentMethod
- PaymentService
  
#### 5.3.4. Biểu đồ Sequence
![Diagram](https://www.planttext.com/api/plantuml/png/R95DJiGm38NtFeNL_LoW2pIqPGS8qRc0ctY6eFoKnAaqPsF1aRW2dM62MjIidkBFpy_9z-VNFWb5oSu2AGaH7znemvaPnldQA3EI5wmEnh6Yg7kEar5S8IMywJNu4iCxAtaYJoTsxAKZeO7IRqlNRDjM06KkxkwASurjP1B6Wi6jS66wfiPN_iYS1DitYYT-pcxWY8yc2NGDxfP6Swp9QDuWWQpWlTQhKWASps9QIL1VKPUjcD7olnxs6c2pgQTfiKKHwuXjy4SJtPLTsPINgVySiC-3CocPu6Uf5ATqp1RsSu3BH_u0003__mC0)

### 5.4. Ca Sử Dụng 2: Maintain Timecard
#### 5.4.1. Mô tả
- Cho phép nhân viên cập nhật và gửi thẻ thời gian ghi lại giờ làm việc.

#### 5.4.2. Luồng Sự Kiện
- Nhân viên yêu cầu xem thẻ thời gian.
- Hệ thống hiển thị thẻ hiện tại hoặc tạo mới.
- Nhân viên nhập giờ làm và chọn charge.
- Hệ thống xác thực và lưu thông tin.
  
#### 5.4.3. Các Lớp Phân Tích
- Employee
- Timecard
- TimecardService
  
#### 5.4.4. Biểu đồ Sequence
  ![Diagram](https://www.planttext.com/api/plantuml/png/Z591JiGm3Bpd5LRl-m4EQAMg22uSs1MSJMeMYpGfZbFWRHnu4byWOJUg2elO729xDEF9MFby_rX7HT4qE8DMWq0tZ2wy4PanmsnvHA_GR7aWYz9lI2Qsr016EDJ7YOqnTHAipYlt36xeEL5Kg3o3Jg5xvQZiTpCA-HmqHLxnebTXcWZQ949UbvBQm6hfgKdyp2GN2QxfvGIxLWZr1vbylyWsipkl970NvAc4kGn98g3lysX7Lg5zHDcHEMfqYuxxOhLOp3TwIiGDJlHddFhOJ4lt0yV8mUVIMehn8RdzFgxyzDlilo4No8xs6rddg_oYBm000F__0m00)
  
### 5.5. Kết luận
Hai ca sử dụng này giúp quản lý thông tin lương bổng và thời gian làm việc của nhân viên, đảm bảo tính chính xác và hiệu quả trong quy trình xử lý.
