## Bài thực hành Lab6 
## THIẾT KẾ LỚP, HỆ THỐNG PAYROLL SYSTEM
---
## 1. **Thiết kế chi tiết cho các lớp trong Hệ thống Xác thực (Authentication System)**
### 1.1: Xác Định Các Operations

| Lớp                 | Phương thức                                        |
|---------------------|----------------------------------------------------|
| **LoginController**  | `login(username: String, password: String): boolean`|
| **UserManager**      | `validateCredentials(username: String, password: String): boolean` |
| **AuthenticationService** | `generateJWT(user: User): String`                |

### 1.2: **Xác định các trạng thái**

| Trạng thái   | Mô tả                                                  |
|--------------|--------------------------------------------------------|
| **LoggedOut** | Người dùng chưa đăng nhập.                             |
| **LoggedIn**  | Người dùng đã đăng nhập và có quyền truy cập hệ thống. |

### 1.3: **Xác định các thuộc tính**

| Lớp                     | Thuộc tính                              | Mô tả                                                      |
|-------------------------|-----------------------------------------|------------------------------------------------------------|
| **UserManager**          | `username: String`                      | Tên người dùng.                                             |
|                         | `password: String`                      | Mật khẩu người dùng (được mã hóa).                          |
| **AuthenticationService** | `jwtToken: String`                     | Token JWT được tạo sau khi xác thực thành công.             |

### 1.4: **Xác định các phụ thuộc, quan hệ kết hợp**
Sơ đồ:

![Diagram](https://www.planttext.com/api/plantuml/png/d92n2i8m48RtF4NePC6-G0QfT114fohEPtlKG7gHIre7ySaSV2HVmRIqejB9R3dk_xwxUzuVgVF0lgcDA0mu9pUsqfHPycoDGPPN8VjdklgiSSW4DIgPUzPKpUKvX2wMox4IAtcqrY2Gk8c1kG-fBH1K7xmMZ2x1OyPO8daDnlr9NpR-r14AyDfIZjpg0j-U2WavUDQ7NSzN_JJn2EmmloidoU9hP2MZy7NHPEEqFKHMWzZ9e8v4YbI6Axy0003__mC0)
---

## 2. **Thiết kế chi tiết cho các lớp trong Hệ thống Quản lý Thẻ chấm công (Timecard Management System)**
### 2.1: **Xác định các Operations**
| Lớp                 | Phương thức                                            |
|---------------------|--------------------------------------------------------|
| **TimecardController** | `createTimecard(employeeID: String, date: Date): Timecard` |
| **TimecardService**   | `addHours(timecardID: String, hours: Integer): void`   |
| **TimecardRepository**| `save(timecard: Timecard): void`                       |

### 2.2: **Xác định các trạng thái**

| Trạng thái   | Mô tả                                                |
|--------------|------------------------------------------------------|
| **Draft**    | Thẻ chấm công được tạo nhưng chưa được gửi.         |
| **Submitted**| Thẻ chấm công đã được gửi và chờ phê duyệt.          |
| **Approved** | Thẻ chấm công đã được phê duyệt.                     |

### 2.3: **Xác định các thuộc tính**

| Lớp               | Thuộc tính                              | Mô tả                                                      |
|-------------------|-----------------------------------------|------------------------------------------------------------|
| **Timecard**      | `timecardID: String`                    | Mã thẻ chấm công.                                          |
|                   | `employeeID: String`                    | Mã nhân viên.                                               |
|                   | `date: Date`                            | Ngày của thẻ chấm công.                                    |
|                   | `hoursWorked: Integer`                  | Số giờ làm việc.                                           |

### 2.4: **Xác định các phụ thuộc, quan hệ kết hợp**
Sơ đồ:

![Diagram](https://www.planttext.com/api/plantuml/png/R9112i8m44NtEKLmLS5U80ifs8NTMZr0I8OQI9iocHQAU38N7iah64LZgCrYDlFcpPyyRlV2aqGQMikKbTxpesb1ITGxrn4wQm7vXV7tKmYIu0jaqFRMJG1LANXDQBfcmtK012z3NOkeObSsazU0er4GpLBhlHlGP_G1KkVvrH6ywWWQmE0TdLbm7g1ttf33AMgz724gVtaInSArURxzooduwkJ1hzYyaS99WC3NONSOAA3JuNEV0000__y30000)
---
## 3. **Thiết kế chi tiết cho các lớp trong Hệ thống Xử lý Lương (Payroll Processing System)**

### 3.1: **Xác định các Operations**

| Lớp                 | Phương thức                                           |
|---------------------|-------------------------------------------------------|
| **PayrollController**  | `processPayroll(timecard: Timecard): void`            |
| **PayrollCalculator**  | `calculateSalary(timecard: Timecard): Double`         |
| **PaymentService**     | `processPayment(amount: Double): void`                |
| **ReportGenerator**    | `generatePayrollReport(): Report`                     |

### 3.2: **Xác định các trạng thái**

| Trạng thái   | Mô tả                                                  |
|--------------|--------------------------------------------------------|
| **Pending**  | Lương chưa được tính toán.                             |
| **Calculated**| Lương đã được tính toán.                               |
| **Paid**     | Lương đã được thanh toán.                              |

### 3.3: **Xác định các thuộc tính**

| Lớp                 | Thuộc tính                                    | Mô tả                                                 |
|---------------------|-----------------------------------------------|-------------------------------------------------------|
| **PayrollController**  | `payrollService: PayrollService`               | Dịch vụ xử lý lương.                                   |
| **PayrollCalculator**  | `hourlyRate: Double`                          | Mức lương theo giờ.                                   |
| **PaymentService**     | `paymentMethod: String`                       | Phương thức thanh toán (chuyển khoản hoặc paycheck).  |

### 3.4: **Xác định các phụ thuộc, quan hệ kết hợp**
Sơ đồ:

![Diagram](https://www.planttext.com/api/plantuml/png/T5512i8m4Bpt5Q6dUkW7Uf22WdWJgmzOqqK2QIARRQ68B_FWa_o2gKtHrffBTZSpavdaUN_aZe6uhdGaDJWdTj2IrNfb3NSxahX6uhqkP2Kw5m09gmebK9c9GwWMcMYiAgDRDD42BMiDR3zQCeom00tKpekjRNtIE9Ahq721r2Y9CxwwqmGgMniUs3-UzdYnn1iqI2D7vtw2mNCFIpozhpg1twT9q-LCo4p4HuSk_a_uZk7HMwDO-Rl_KgQcFISqE2Jot1nDwJ_o1G00__y30000)
---
## 4. **Thiết kế chi tiết cho các lớp trong Hệ thống Thanh toán (Payment System)**

### 4.1: **Xác định các Operations**

| Lớp                 | Phương thức                                    |
|---------------------|------------------------------------------------|
| **BankInterface**    | `transferFunds(amount: Double): void`          |
| **PrintService**     | `generatePaycheck(): void`                     |

### 4.2: **Xác định các trạng thái**

| Trạng thái   | Mô tả                                               |
|--------------|-----------------------------------------------------|
| **Pending**  | Thanh toán chưa được thực hiện.                    |
| **Processed**| Thanh toán đã được xử lý.                           |
| **Completed**| Thanh toán đã được hoàn tất.                        |

### 4.3: **Xác định các thuộc tính**

| Lớp                | Thuộc tính                              | Mô tả                                           |
|--------------------|-----------------------------------------|-------------------------------------------------|
| **BankInterface**   | `bankAccount: String`                   | Số tài khoản ngân hàng.                        |
| **PrintService**    | `paycheckAmount: Double`                | Số tiền paycheck cần in.                       |

### 4.4: **Xác định các phụ thuộc, quan hệ kết hợp**
Sơ đồ:

![Diagram](https://www.planttext.com/api/plantuml/png/LCv12i8m40NGVKuHkggBNY0BAIA2kw8d69EfXgOJd9aKH3oP2u_a5HHnqVxzV_-_dwzM55ZBc8nF868tGCEU5Ba7Z_Pkx2_AGD8Zxme5gM7CXTJPRIwdX2jdfno3UPW_qN4aFI9FSIQSaP11iOERlw0VwbbjkTaqwoNXR7N0Qq5HgKoB5BvlFm000F__0m00)
---
## 5. **Thiết kế chi tiết cho các lớp trong Hệ thống Báo cáo (Reporting System)**

### 5.1: **Xác định các Operations**

| Lớp                 | Phương thức                                           |
|---------------------|-------------------------------------------------------|
| **ReportController** | `generateReport(): Report`                            |
| **ReportService**    | `generatePayrollReport(): Report`                     |
| **ExportService**    | `exportToPDF(report: Report): void`                   |
|                     | `exportToExcel(report: Report): void`                 |
|                     | `exportToCSV(report: Report): void`                   |

### 5.2: **Xác định các trạng thái**

| Trạng thái   | Mô tả                                                  |
|--------------|--------------------------------------------------------|
| **Created**  | Báo cáo đã được tạo nhưng chưa xuất.                  |
| **Generated**| Báo cáo đã được tạo và sẵn sàng xuất.                  |
| **Exported** | Báo cáo đã được xuất thành công.                      |

### 5.3: **Xác định các thuộc tính**

| Lớp               | Thuộc tính                              | Mô tả                                                      |
|-------------------|-----------------------------------------|------------------------------------------------------------|
| **Report**        | `reportContent: String`                 | Nội dung báo cáo.                                          |
|                   | `reportID: String`                      | Mã báo cáo.                                                |
|                   | `exportFormat: String`                  | Định dạng xuất báo cáo (PDF, Excel, CSV).                  |
| **ExportService** | `fileFormat: String`                    | Định dạng xuất báo cáo (PDF, Excel, CSV).                  |

### 5.4: **Xác định các phụ thuộc, quan hệ kết hợp**
Sơ đồ:

![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niK9GQa5-KObpVbv9KNvEJcgHGZMN0XYaf-Qb5YMMf48KQ6XQGPLorNAXQ0rEBIhBJ4x5q1UGM0ao4RTsrmfisbF1eY7v0Ivk6aLW7J2TG2FAyZDJqDIvLYIdvX2bqZau38Swe9CmWa5NrmxDWrOAIg75gSLANAZ288MeNW4gX0W0rJgavgK00ni0003__mC0)
---
## 6. **Thiết kế chi tiết cho các lớp trong Hệ thống Lập lịch (Scheduler System)**

### 6.1: **Xác định các Operations**

| Lớp                     | Phương thức                                         |
|-------------------------|-----------------------------------------------------|
| **SystemClockInterface** | `getCurrentTime(): Date`                           |
| **JobScheduler**         | `scheduleJob(job: Job, time: Date): void`           |
|                         | `executeScheduledJob(job: Job): void`               |

### 6.2: **Xác định các trạng thái**

| Trạng thái   | Mô tả                                                   |
|--------------|---------------------------------------------------------|
| **Idle**     | Hệ thống chưa có công việc nào được lên lịch.           |
| **Scheduled**| Công việc đã được lên lịch và chờ thực thi.             |
| **Executed** | Công việc đã được thực thi.                             |

### 6.3: **Xác định các thuộc tính**

| Lớp                      | Thuộc tính                              | Mô tả                                                   |
|--------------------------|-----------------------------------------|---------------------------------------------------------|
| **SystemClockInterface**  | `currentTime: Date`                    | Thời gian hiện tại của hệ thống.                        |
| **JobScheduler**          | `scheduledJobs: List<Job>`             | Danh sách các công việc đã lên lịch.                    |
|                          | `jobExecutionTime: Date`               | Thời gian thực thi công việc.                           |

### 6.4: **Xác định các phụ thuộc, quan hệ kết hợp**
Sơ đồ:

![Diagram](https://www.planttext.com/api/plantuml/png/UhzxlqDnIM9HIMbk3bToJc9niK9mPN59QgvpJdvojcTUIMfHMc9oga8rbm8OfAUME9SM5QNcbOHavgPgQ5efk2IMf7BLSa4rU-Kd1ITdfAQKvgGMmJKLGqM0aXfP-KbM85Kw2YL00o3QWQQKvMUcG5MdLgGcbvQamen9GTO5Kmcq3wipTNNjK9rWfQ0KMfnQhCJba9gN0lGZ0000__y30000)
