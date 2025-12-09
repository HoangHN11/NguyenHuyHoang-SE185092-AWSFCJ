---
title: "Xây dựng lớp phân tích riêng tư"
weight: 2
chapter: false
pre: " <b> 5.4. </b> "
---

## 5.4.1 Cách tiếp cận analytics tối giản (phù hợp chi phí)

- **Nguồn dữ liệu**: CloudWatch structured API logs (sự kiện và metric request).
- **Lưu trữ**: Giữ log trong CloudWatch với retention hợp lý (30–90 ngày).
- **Xuất**: Bật export CloudWatch → S3 khi cần phân tích.
- **Truy vấn**: CloudWatch Log Insights cho truy vấn nhanh; Athena trên log xuất S3 cho phân tích sâu.

Không cần DWH riêng nhưng vẫn quan sát được hành vi và độ tin cậy.

---

## 5.4.2 ETL nhẹ (tùy chọn)

- Tạo **export task** hàng ngày CloudWatch Logs sang S3 (`logs/<yyyy>/<mm>/<dd>/`).
- Trong Athena, tạo external table trên JSON xuất; partition theo ngày.
- Dẫn xuất view `events` với trường chính: `eventName`, `userId`, `sessionId`, `productId`, `statusCode`, `latencyMs`, `timestamp`.
- Tiết kiệm chi phí:
  - Nén (GZIP) khi export.
  - Loại bỏ trường nhiễu high-cardinality.
  - Lifecycle S3 (Glacier hoặc expire sau X ngày).

---

## 5.4.3 Bảo mật và truy cập

- **Không công khai endpoint analytics**: export nằm trong bucket S3 private.
- **IAM tối thiểu**:
  - Role API: Secrets Manager read, CloudWatch logs write, S3 put (nếu export).
  - CloudFront chỉ đọc bucket ảnh; upload luôn qua presigned PUT.
- **Secrets**: Mật khẩu DB + bucket trong Secrets Manager; xoay khóa theo runbook.
- **Mã hóa**: HTTPS toàn tuyến; mã hóa bucket; export bucket private.

---

## 5.4.4 Kiểm tra vận hành

- Alarm lỗi 5xx, độ trễ p95, lỗi auth.
- Định kỳ xác nhận:
  - Job export CloudWatch thành công (nếu bật).
  - JWT Cognito vẫn verify sau khi đổi cấu hình.
  - Quyền presigned upload còn đúng (content-type, prefix).

---

## 5.4.5 Mở rộng tương lai (vượt phạm vi hiện tại)

- Thêm RDS read-replica hoặc DB analytics riêng nếu truy vấn tăng.
- Thêm Lambda transform hằng ngày chuẩn hóa vào bảng `events`.
- Thêm BI (QuickSight) trên Athena/DB analytics cho dashboard phong phú hơn.
---
