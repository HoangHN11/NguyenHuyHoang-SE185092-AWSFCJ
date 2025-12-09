---
title: "Đề xuất dự án"
date: 2025-11-10
weight: 1
chapter: false
pre: " <b> 2. </b> "
---

# **Nền tảng thương mại điện tử trang sức**

## **Hệ thống bán hàng trực tuyến dựa trên đám mây sử dụng React, .NET và MySQL trên AWS Lightsail**



# Hành trình AWS First Cloud AI – **Kế hoạch dự án**

#

# T1VN – FPT University – Video Share

# 03/12/2025

# Mục lục

**[1 NỀN TẢNG VÀ ĐỘNG LỰC 3](#background-and-motivation)**

[1.1 TÓM TẮT CHỦ ĐỀ 3](#executive-summary)

[1.2 TIÊU CHÍ THÀNH CÔNG DỰ ÁN 3](#heading=)

[1.3 CÁC GIẢ ĐỊNH 3](#heading=)

[**2 KIẾN TRÚC GIẢI PHÁP / SƠ ĐỒ KIẾN TRÚC 4**](#heading=)

[2.1 SƠ ĐỒ KIẾN TRÚC KỸ THUẬT 4](#technical-architecture-diagram)

[2.2 KẾ HOẠCH KỸ THUẬT 4](#technical-plan)

[2.3 KẾ HOẠCH DỰ ÁN 5](#heading=)

[2.4 CÁC KHÍA CẠNH AN TOÀN 5](#security-considerations)

[**3 CÁC HOẠT ĐỘNG VÀ DELIVERABLES 6**](#activities-and-deliverables)

[3.1 CÁC HOẠT ĐỘNG VÀ DELIVERABLES 6](#activities-and-deliverables-1)

[3.2 NGOÀI PHẠM VI 8](#out-of-scope)

[3.3 CON ĐƯỜNG ĐI VÀO PRODUCTION 8](#path-to-production)

[**4 DỰ TÍNH CHI PHÍ AWS CHI TIẾT THEO DỊCH VỤ 9**](#expected-aws-cost-breakdown-by-services)

[**5 ĐỘI TẠO 10**](#team)

[**6 NGUỒN LỰC & ƯỚC TÍNH CHI PHÍ 10**](#resources-&-cost-estimates)

[**7 CHẤP NHẬN 11**](#acceptance)

# 1. **NỀN TẢNG VÀ ĐỘNG LỰC**

# 1.1 **TÓM TẮT CHỦ ĐỀ**

Dự án Trang web Trang sức AWS bao gồm phát triển Nền tảng thương mại điện tử trang sức toàn diện. Kiến trúc hệ thống bao gồm cơ sở hạ tầng backend và cơ sở dữ liệu được lưu trữ trên AWS Lightsail, kết hợp với frontend dựa trên React được triển khai thông qua Amazon S3 và CloudFront. Kiến trúc này được thiết kế để đảm bảo khả năng mở rộng, bảo mật cao và tối ưu hóa chi phí vận hành bằng cách tận dụng các dịch vụ đám mây thiết yếu nhưng hiệu quả.

**Hệ thống cung cấp các tính năng chính như:**

- Quản lý sản phẩm trang sức.
- Khả năng tải lên hình ảnh sản phẩm.
- Chức năng giỏ hàng.
- Đăng ký người dùng và xác thực thông qua AWS Cognito.
- Các hoạt động API backend trên Lightsail với lưu trữ dữ liệu MySQL/Postgres.
- Tăng tốc độ cung cấp nội dung và xử lý SSL tiêu chuẩn quốc tế thông qua CDN.

  # 1.2 **TIÊU CHÍ THÀNH CÔNG DỰ ÁN**

- **Hiệu suất:** Thời gian tải trang web dưới 2 giây cho truy cập quốc tế, được hỗ trợ bởi CDN CloudFront.
- **Tính ổn định:** Backend hoạt động ổn định trên Lightsail trong điều kiện lưu lượng thực tế.
- **Tính toàn vẹn dữ liệu:** Các hoạt động cơ sở dữ liệu an toàn với tốc độ truy xuất nhanh.
- **Quản lý người dùng:** Quản lý người dùng ổn định và an toàn thông qua Amazon Cognito.
- **Bảo mật:** Các quy trình tải lên hình ảnh an toàn thông qua Amazon S3.
- **Giám sát:** Ghi nhật ký API toàn diện thông qua Amazon CloudWatch.

  # 1.3 **CÁC GIẢ ĐỊNH**

- **Khối lượng lưu lượng:** Mức lưu lượng vừa phải (dưới 100.000 yêu cầu/tháng).
- **Mở rộng quy mô:** Không yêu cầu cấu hình tự động mở rộng quy mô nâng cao.
- **Miền:** Tên miền được mua trước hoặc sẽ được mua thông qua Amazon Route 53\.
- **Năng lực:** Đội phát triển có kỹ năng thành thạo Node.js và React.

# 2. **KIẾN TRÚC GIẢI PHÁP / SƠ ĐỒ KIẾN TRÚC**

# 2.1 **SƠ ĐỒ KIẾN TRÚC KỸ THUẬT**

![Architecture](/images/Diagram.drawio.png)

# 2.2 **KẾ HOẠCH KỸ THUẬT**

- **Frontend:** Được lưu trữ trên Amazon S3 với CDN Amazon CloudFront và HTTPS được bật thông qua AWS Certificate Manager (ACM).
- **API Backend:** Môi trường runtime .NET trên AWS Lightsail.
- **Cơ sở dữ liệu:** MySQL/PostgreSQL được lưu trữ trên AWS Lightsail.
- **Xác thực:** Amazon Cognito User Pool.
- **Lưu trữ hình ảnh:** Amazon S3.
- **Ghi nhật ký:** Amazon CloudWatch.
- **Quản lý Secrets:** AWS Secrets Manager.

# 2.3 **KẾ HOẠCH DỰ ÁN**

Thời gian triển khai ước tính từ 6 đến 12 tuần, tùy thuộc vào phạm vi dự án cuối cùng.

# 2.4 **CÁC KHÍA CẠNH AN TOÀN**

- **Kiểm soát truy cập:** Truy cập riêng tư S3 được cấu hình, cấp quyền đọc độc quyền cho CloudFront.
- **Quản lý thông tin đăng nhập:** API sử dụng các khóa riêng được lưu trữ an toàn trong AWS Secrets Manager.
- **Mã hóa:** Triển khai HTTPS trên toàn bộ hệ thống.
- **Bảo mật xác thực:** Đăng nhập người dùng được bảo vệ bởi Amazon Cognito.

# 3. **CÁC HOẠT ĐỘNG VÀ DELIVERABLES**

# 3.1 **CÁC HOẠT ĐỘNG VÀ DELIVERABLES**

|         Project Phase         | Timeline | Activities                                                                                                                                                                                                                                                                                                                                                                                                             | Deliverables / Milestones                                                                                                                                                          |  MD   |
| :---------------------------: | :------: | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
|        **Assessment**         |  Week 1  | \- Analyze the Jewelry Web system requirements. \- Draft the Architecture Diagram. **\-** Design the Database Schema (Lightsail MySQL/Postgres). \- Identify necessary secrets (DB password, bucket name).                                                                                                                                                                                                             | \- Architecture Diagram \- DB Schema \- List of Secrets                                                                                                                            | **5** |
| **Setup Base Infrastructure** |  Week 2  | \- Configure S3 hosting and React build. \- Configure CloudFront CDN and ACM SSL. \- Map domain via Route 53\. \- Provision Lightsail API instance. \- Provision Lightsail Database. \- Configure Cognito Login. \- Create Secrets Manager entries:   + Secret 1: DB_PASSWORD   + Secret 2: APP_CONFIG (bucket-name) \- Assign IAM roles to API instances for secret retrieval permissions. \- Enable CloudWatch logs. | \- Functional Frontend CDN \- Operational Backend API \- Database connectivity established \- Functional Cognito login \- Secrets Manager populated with DB password & bucket name | **7** |

|    Setup Component 1 – Backend API     | Week 3 | \- Implement API logic to retrieve DB password from Secrets Manager. \- Implement API logic to retrieve bucket names from Secrets Manager. \- Implement image upload to S3 (via presigned URL). \- Develop CRUD operations for jewelry products. \- Integrate Cognito authentication. \- Implement log transmission to CloudWatch. | \- Stable API operations \- Successful image upload functionality \- Successful Login functionality \- Hardcoded configurations fully replaced by Secrets Manager |   7   |
| :------------------------------------: | :----: | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---: |
| **Setup Component 2 – Frontend React** | Week 4 | \- Develop Jewelry Shop UI. \- Implement Cognito Login interface. \- Implement jewelry image upload interface. \- Fetch data from API. \- Build and deploy to S3 \+ CloudFront.                                                                                                                                                    | \- Complete User Interface (UI) \- API Integration established                                                                                                    | **7** |
|         **Testing & Go-live**          | Week 5 | \- Integration testing (FE ↔ BE ↔ S3 ↔ DB). \- Security testing (IAM \+ Secrets Manager). \- End-to-end testing.                                                                                                                                                                                                                   | \- Test Report \- Security checklist                                                                                                                              | **5** |
|              **Handover**              | Week 6 | \- Provide instruction on using Secrets Manager for updating bucket names/DB passwords. \- Transfer AWS account ownership. \- Provide Runbook Documentation.                                                                                                                                                                       | \- Comprehensive Runbook \- Project Closure                                                                                                                       | **5** |

##

# 3.2 **NGOÀI PHẠM VI**

- AI/Machine Learning features.
- Complex E-commerce functionalities.
- Advanced image processing capabilities.
- Multi-region deployment or Disaster Recovery (DR) sites.
- Complex administrative systems.
- Integration with third-party systems.

# 3.3 **CON ĐƯỜNG ĐI VÀO PRODUCTION**

- Tối ưu hóa Sự xuất sắc trong hoạt động.
- Quản lý Secrets – Làm cứng Production.
- Xử lý lỗi mở rộng.
- Triển khai & Xác minh Production.
- Kế hoạch Phục hồi thảm họa.
- Bàn giao Production.

# 4. **DỰ TÍNH CHI PHÍ AWS CHI TIẾT THEO DỊCH VỤ**

| Tên dịch vụ                    | Chi phí trước mặt | Chi phí hàng tháng | Khu vực                            |
| :----------------------------- | :---------------- | :----------------- | :--------------------------------- |
| Amazon S3                      | 0.00 USD          | 0.26 USD           | Châu Á Thái Bình Dương (Singapore) |
| Amazon CloudFront (CDN cho FE) | 0.00 USD          | 0.17 USD           | Châu Á Thái Bình Dương (Singapore) |
| AWS ACM                        | 0.00 USD          | 0 USD              | Châu Á Thái Bình Dương (Singapore) |
| Amazon Route 53                | 0.00 USD          | 0.50–1.00 USD      | Châu Á Thái Bình Dương (Singapore) |
| AWS Lightsail – Cơ sở dữ liệu  | 0.00 USD          | 10–15 USD          | Châu Á Thái Bình Dương (Singapore) |
| Amazon Cognito                 | 0.00 USD          | 2.00 USD           | Châu Á Thái Bình Dương (Singapore) |
| AWS Secrets Manager            | 0.00 USD          | 0.40 USD           | Châu Á Thái Bình Dương (Singapore) |
| Amazon CloudWatch              | 0.00 USD          | 0.30 USD           | Châu Á Thái Bình Dương (Singapore) |
| AWS Lightsail – Máy chủ API    | 0.00 USD          | 5 \- 10 USD        | Châu Á Thái Bình Dương (Singapore) |

# 5. **ĐỘI TẠO**

**Bảo trợ điều hành của Đối tác**

| Tên | Chức danh | Mô tả | Email / Thông tin liên hệ |
| :-- | :-------- | :---- | :------------------------ |
|     |           |       |                           |

**Các bên liên quan của dự án**

| Tên | Chức danh | Bên liên quan cho | Email / Thông tin liên hệ |
| :-- | :-------- | :---------------- | :------------------------ |
|     |           |                   |                           |

**Đội dự án của Đối tác**

| Tên                  | Chức danh               | Vai trò             | Email / Thông tin liên hệ    |
| :------------------- | :---------------------- | :------------------ | :--------------------------- |
| Nguyễn Duy Hiếu      | Chủ sản phẩm            | Quản lý dự án (BE)  | Hieundse185047@fpt.edu.vn    |
| Lưu Ngọc Ngân Giang  | Nhà phát triển phần mềm | Nhà phát triển (BE) | luungocngangiang25@gmail.com |
| Nguyễn Huy Hoàng     | Nhà phát triển phần mềm | Nhà phát triển (FE) | Hoangnhse185092@fpt.edu.vn   |
| Trần Hồ Phương Khanh | Nhà phát triển phần mềm | Nhà phát triển (FE) | khanhthpse185070@fpt.edu.vn  |
| Tăng Khanh Nhi       | Nhà phát triển phần mềm | Nhà phát triển (FE) | tangkhanhnhi111@gmail.com    |

**Danh sách liên hệ căng thẳng của dự án**

| Tên | Chức danh | Vai trò | Email / Thông tin liên hệ |
| :-- | :-------- | :------ | :------------------------ |
|     |           |         |                           |

# 6. **NGUỒN LỰC & ƯỚC TÍNH CHI PHÍ**

| Nguồn lực                                                 | Trách nhiệm                                                                                                                                                                                           | Tỷ lệ (USD) / Giờ |
| :-------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- |
| Kiến trúc sư giải pháp \[số lượng nhân sự được chỉ định\] | \- Thiết kế kiến trúc AWS (S3, CloudFront, Lightsail, ACM, Route 53, Secrets Manager) \- Tư vấn bảo mật & tối ưu chi phí \- Review triển khai & best practices                                        | 12                |
| Kỹ sư \[số lượng nhân sự được chỉ định\]                  | \- Triển khai cơ sở hạ tầng: S3, CloudFront, Route 53, ACM, Lightsail \- Cấu hình CI/CD, upload FE lên S3 \- Triển khai Node.js API trên Lightsail \- Cấu hình Secrets Manager, logging và CloudWatch | 6                 |
| Khác (Vui lòng chỉ rõ)                                    | \- Kiểm thử hệ thống sau triển khai \- Tư vấn hỗ trợ khách hàng                                                                                                                                       | 0                 |

\* Ghi chú: Tham khảo phần "các hoạt động & deliverables" để xem danh sách các giai đoạn dự án

|   Giai đoạn dự án    | Kiến trúc sư giải pháp | Kỹ sư | Khác (Vui lòng chỉ rõ) | Tổng số giờ |
| :------------------: | :--------------------: | :---: | :--------------------: | :---------: |
|   S3 \+ CloudFront   |           1            |   2   |                        |      3      |
| Lightsail API \+ DB  |           1            |   4   |                        |      4      |
|       Cognito        |           1            |   2   |                        |      5      |
| Logging & Monitoring |           1            |   1   |                        |      3      |
|     Tổng số giờ      |           4            |  12   |                        |     15      |
|     Tổng chi phí     |                        |       |                        |             |

Phân phối đóng góp chi phí giữa Đối tác, Khách hàng, AWS:

| Bên        | Đóng góp (USD) | % Đóng góp của Tổng cộng |
| :--------- | :------------- | :----------------------- |
| Khách hàng |                |                          |
| Đối tác    |                |                          |
| AWS        |                |                          |

# 7. **CHẤP NHẬN**

- Trang web chạy ổn định trên tên miền thực.

- API kết nối đầy đủ với DB.

- Tải lên hình ảnh sản phẩm hoạt động.

- CloudWatch log & Cognito login hoạt động.

- Được chấp nhận bởi khách hàng/bên liên quan.
