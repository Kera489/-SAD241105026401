# 4. Thiết kế hệ thống con
 # 1. **Phần tử dữ liệu bệnh nhân (Patient Data Element)**

### Chức năng:
- Quản lý thông tin bệnh nhân bao gồm các thông tin cá nhân, lịch sử chẩn đoán, điều trị và hồ sơ thuốc đã kê.
- Cung cấp khả năng thêm, cập nhật, truy vấn và xóa thông tin bệnh nhân.

### Các thành phần:
- **Thuộc tính**:
  - PatientID: Mã bệnh nhân duy nhất (Kiểu dữ liệu: String).
  - Name: Tên bệnh nhân (Kiểu dữ liệu: String).
  - Addres: Địa chỉ bệnh nhân (Kiểu dữ liệu: String).
  - ContactInfo: Thông tin liên hệ bệnh nhân (Kiểu dữ liệu: String).
  - DiagnosisHistory: Lịch sử chẩn đoán (Kiểu dữ liệu: List of Diagnosis objects).
  - PrescriptionHistory: Hồ sơ thuốc đã kê (Kiểu dữ liệu: List of Prescription objects).

- **Hành vi**:
  - AddPatient(): Thêm bệnh nhân mới vào hệ thống.
  - UpdatePatient(): Cập nhật thông tin bệnh nhân.
  - RetrievePatient(): Truy vấn thông tin bệnh nhân từ hệ thống.
  - DeletePatient(): Xóa thông tin bệnh nhân khỏi hệ thống.

### Mối quan hệ:
- Liên kết với **Appointment Management** và **Risk Alert** thông qua PatientID.
- Biểu đồ PlantText  
      ![Diagram](https://www.planttext.com/plantuml/png/PP3T2i8m38Nl1tk7NYhY2moHgRrmCCRmvm7A6hV2beus5KHyTwjkmsqDXEGxXt1eR4aOSaqT1aKjh6Lv9V3Yk4iLk3rWbVcTFSE0-RTckI05I0cFs9cCmh8NCj70bEsaD63j51yqaYWemPkUIbo94hLLzgWiQVE8MEg7pO2tGmv_k32g9QLnxFrNElklhpvvkloBPS-khHG4Ctm2dmlkSu533IF_AmnYGFdzmRxU)



# 2. **Phần tử quản lý lịch hẹn (Appointment Management Element)**

### Chức năng:
- Đồng bộ lịch hẹn từ hệ thống APPOINTMENTS.
- Quản lý và ghi nhận các lịch hẹn bị bỏ lỡ, cung cấp khả năng lên lại lịch hẹn cho bệnh nhân.

### Các thành phần:
- **Thuộc tính**:
  - AppointmentID: Mã lịch hẹn duy nhất (Kiểu dữ liệu: String).
  - PatientID: Mã bệnh nhân (Kiểu dữ liệu: Foreign key liên kết với bệnh nhân).
  - DateTime: Thời gian lịch hẹn (Kiểu dữ liệu: Datetime).
  - Status: Trạng thái lịch hẹn (Kiểu dữ liệu: String, có thể là "Scheduled", "Missed", "Rescheduled").

- **Hành vi**:
  - SyncAppointments(): Đồng bộ hóa lịch hẹn từ hệ thống APPOINTMENTS.
  - TrackMissedAppointments(): Ghi nhận các lịch hẹn bị bỏ lỡ.
  - RescheduleAppointment(): Đặt lại lịch hẹn cho bệnh nhân.

### Mối quan hệ:
- Liên kết với **Patient Data Element** thông qua PatientID.
   - Biểu đồ PlantText  
      ![Diagram](https://www.planttext.com/plantuml/png/RS_D2eCm30VmUy5tw75Zx0KyEV2mWGEt-WAXXhMiHZ7fGSRUVLzqUZ2vXFp-45Amm2Yn2vco0PXrxO2QU8b0rLHvwuv8-f4f_QwzFWn3xqaw93cLkJOoUhebh47yAfGWsFWEy_-Kn0X8v3d_s--qcSWkRl5ccwGPmTxFdXdRzS0LsJfiOy25V_YPgGAf_Ruwzmi0)




# 3. **Phần tử quản lý cảnh báo nguy cơ (Risk Alert Element)**

### Chức năng:
- Phát hiện và cảnh báo các nguy cơ liên quan đến hành vi tự hại hoặc gây hại của bệnh nhân.

### Các thành phần:
- **Thuộc tính**:
  - RiskID: Mã cảnh báo nguy cơ duy nhất (Kiểu dữ liệu: String).
  - PatientID: Mã bệnh nhân liên quan đến cảnh báo (Kiểu dữ liệu: Foreign key).
  - RiskLevel: Mức độ nguy cơ (Kiểu dữ liệu: Enum với các giá trị "Low", "Medium", "High").
  - RiskDetails: Chi tiết về nguy cơ (Kiểu dữ liệu: String).

- **Hành vi**:
  - MonitorRisk(): Giám sát nguy cơ của bệnh nhân theo các yếu tố như hành vi, chẩn đoán, hồ sơ thuốc, v.v.
  - SendRiskNotification(): Gửi thông báo cảnh báo cho các nhân viên y tế hoặc bệnh nhân khi có nguy cơ.

### Mối quan hệ:
- Liên kết với **Patient Data Element** thông qua PatientID.
-  - Biểu đồ PlantText  
      ![Diagram](https://www.planttext.com/plantuml/png/SoWkIImgAStDuULApaaiBbO8o4ZC2oaDB4tCywbqJipBS4hCzqilhNJELwZcvL800bs5eCpYR4yNAuNWagBCl7IOQ41YIMPgNWcc14YvJsfPQWus2PVKaiJCd6A454HIMy4tFo-p9By8f4P34oOOd9gN0XBnoo_9JCjC1jgOdmUIhUNbSW1AWRq1Wm00)
     



# 4. **Phần tử quản lý báo cáo (Report Management Element)**

### Chức năng:
- Tạo và lưu trữ các báo cáo quản lý hoặc báo cáo ẩn danh.

### Các thành phần:
- **Thuộc tính**:
  - ReportID: Mã báo cáo duy nhất (Kiểu dữ liệu: String).
  - ReportType: Loại báo cáo (Kiểu dữ liệu: Enum với các giá trị "Management", "Anonymized").
  - CreatedBy: Người tạo báo cáo (Kiểu dữ liệu: String).
  - DateCreated: Ngày tạo báo cáo (Kiểu dữ liệu: Datetime).

- **Hành vi**:
  - GenerateReport(): Tạo báo cáo mới dựa trên các dữ liệu hiện có.
  - SaveReport(): Lưu trữ báo cáo trong hệ thống.
  - ExportReport(): Xuất báo cáo dưới dạng file (PDF, Excel, v.v.).

### Mối quan hệ:
- Có thể liên kết với **Patient Data Element** để tạo báo cáo liên quan đến bệnh nhân, nhưng không phải lúc nào cũng yêu cầu.
 - Biểu đồ PlantText  
      ![Diagram](https://www.planttext.com/plantuml/png/SoWkIImgAStDuULApaaiBbO8o4ZC2oaDB4tCywbqIintJinNgERbKW02NOMWr8ByeX9F5ok5u9AYpBnqLF6Goe9KT1ddejJ4ajGKfqfq2HUWC5JI2im9oSnDvUM2I6ihkAVcfHO1HI4cQsZ2n8CJop34N2j0V8HeBI-NGsfU2jXF40W0)

# 5. **Phần tử bảo mật và quyền riêng tư (Security and Privacy Element)**

### Chức năng:
- Bảo vệ dữ liệu và quản lý quyền truy cập hệ thống dựa trên vai trò người dùng.

### Các thành phần:
- **Thuộc tính**:
  - UserID: Mã người dùng duy nhất (Kiểu dữ liệu: String).
  - Role: Vai trò người dùng (Kiểu dữ liệu: Enum với các giá trị "Admin", "ClinicalStaff", "Manager").
  - Permissions: Danh sách quyền truy cập (Kiểu dữ liệu: List of permissions).

- **Hành vi**:
  - AuthenticateUser(): Xác thực người dùng khi đăng nhập vào hệ thống.
  - AssignRole(): Gán vai trò cho người dùng (ví dụ: Admin, ClinicalStaff).
  - LogAccess(): Ghi nhận hoạt động truy cập của người dùng vào hệ thống.

### Mối quan hệ:
- Liên quan đến tất cả các phần tử khác trong hệ thống để đảm bảo phân quyền và bảo mật thông tin người dùng.
 - Biểu đồ PlantText  
      ![Diagram](https://www.planttext.com/plantuml/png/NOx12i8m44JlWVp37XNn1uf8Arw42hLMxo4kQI3TG7Pp4F7VRIqgk7DxCpjCoMAIv25ePODXXgOtrEMTYKSZLtFATwJM8xakmqCh66yD5yPqs1TmbkJ9VMWR0_wp1jFWcNqaBg3sB9lPtserHrPGPUcHn5iZE1KlbbzdV7GqrVvO7LrbBJ9FwAbLYNHxhv_r0W00)

### Tổng quan:
Các hệ thống con này sẽ tương tác với nhau thông qua các khóa ngoại như `PatientID` và sử dụng các chức năng để quản lý thông tin bệnh nhân, lịch hẹn, cảnh báo nguy cơ, báo cáo và bảo mật. Điều này giúp hệ thống hoạt động mượt mà và bảo mật, đồng thời đảm bảo rằng dữ liệu bệnh nhân luôn được bảo vệ và truy cập một cách an toàn.
## Nguồn tham khảo:


### 1. **Phần tử dữ liệu bệnh nhân (Patient Data Element)**


- **Software Engineering: Ian Sommerville (Tenth Edition):** Phân tích thiết kế dữ liệu trong hệ thống y tế.
  
  - [Software Engineering: Ian Sommerville](https://software-engineering-book.com/case-studies/mentcare/)


### 2. **Phần tử quản lý lịch hẹn (Appointment Management Element)**

- **Mentcare Requirements Document (trang 11):** Đồng bộ hóa và theo dõi lịch hẹn từ hệ thống APPOINTMENTS.
- **Phân tích từ các bài nghiên cứu thực tế về tích hợp lịch và quản lý thời gian trong phần mềm y tế:**
  - [Module 2.2: Software System Management](https://fossvjcet.github.io/CS-S5/CST309%20-%20Management%20of%20Software%20Systems/Other%20Notes/Module%202.2.pdf)
  - [Mentcare Case Study - Ian Sommerville](https://software-engineering-book.com/case-studies/mentcare/)



### 3. **Phần tử quản lý cảnh báo nguy cơ (Risk Alert Element)**

- **Mentcare Requirements Document (trang 10-12, 15-17):** Mô tả các yêu cầu cảnh báo nguy cơ liên quan đến hành vi tự hại hoặc gây hại.
- **Software Engineering: Ian Sommerville:** Đưa ra các khái niệm thiết kế về hệ thống cảnh báo trong phần mềm an toàn.
  - [Mentcare Case Study - Ian Sommerville](https://github.com/opendesigncasestudies/Mentcare-IanSommerville)
  - [Phân tích cảnh báo nguy cơ trong phần mềm y tế](https://www.slideshare.net/slideshow/se-chapter-4-software-requirementspptx/26620533)


### 4. **Phần tử quản lý báo cáo (Report Management Element)**

- **Mentcare Requirements Document (trang 12-14):** Chi tiết các yêu cầu về tạo và lưu trữ báo cáo, đặc biệt là báo cáo ẩn danh.
- **Tài liệu về báo cáo y tế và bảo mật thông tin từ các nghiên cứu liên quan:**
  - [Mentcare Case Study - Ian Sommerville](https://github.com/opendesigncasestudies/Mentcare-IanSommerville)
  - [Module 2.2: Software System Management](https://fossvjcet.github.io/CS-S5/CST309%20-%20Management%20of%20Software%20Systems/Other%20Notes/Module%202.2.pdf)



### 5. **Phần tử bảo mật và quyền riêng tư (Security and Privacy Element)**

- **Mentcare Requirements Document (trang 16-19):** Yêu cầu bảo mật và phân quyền người dùng trong hệ thống.
- **Phân tích thiết kế hệ thống bảo mật trong tài liệu Ian Sommerville và các ví dụ tiêu chuẩn ngành:**
  - [Software Engineering: Ian Sommerville - Mentcare Case Study](https://software-engineering-book.com/case-studies/mentcare/)
  - [Phân tích bảo mật hệ thống](https://www.slideshare.net/slideshow/se-chapter-4-software-requirementspptx/266205338)



N

