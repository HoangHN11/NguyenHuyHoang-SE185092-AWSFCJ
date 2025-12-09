---
title: "Tổng kết & Dọn dẹp"
weight: 2
chapter: false
pre: " <b> 5.6. </b> "
---

## 5.6.1 Tóm tắt

Chúng ta đã lên kế hoạch và phạm vi AWS Jewelry Web như một stack e-commerce an toàn, tối ưu chi phí:

- **Frontend**: React trên S3 + CloudFront với TLS ACM, domain Route 53.
- **Backend**: .NET API trên Lightsail; DB Lightsail (MySQL/Postgres); Secrets Manager cho mật khẩu DB/bucket.
- **Identity**: Cognito User Pool cho signup/login và verify token API.
- **Media**: Bucket S3 private; upload qua presigned PUT; CloudFront đọc object.
- **Observability**: CloudWatch log cấu trúc cho API + sự kiện nghiệp vụ; tùy chọn export S3/Athena.

Tiêu chí thành công: tải trang <2s qua CDN, API ổn định, DB an toàn, Cognito ổn định, upload an toàn, log API đầy đủ.

---

## 5.6.2 Điểm rút ra

- Không để secrets trong code: dùng Secrets Manager + IAM tối thiểu cho role API.
- Hiệu năng từ edge: CloudFront + S3 + ACM; giảm hop backend cho static.
- Ưu tiên độ tin cậy: log ý nghĩa (auth, upload, CRUD, sự kiện sản phẩm) và đặt alarm lỗi/độ trễ.
- Kiểm soát chi phí: Lightsail dự đoán được; CloudWatch retention tinh chỉnh; analytics tùy chọn khi cần.

---

## 5.6.3 Checklist dọn dẹp

- S3 + CloudFront: gỡ distribution và đối tượng nếu ngừng site.
- Cognito: xóa User Pool nếu không dùng.
- Lightsail: snapshot hoặc terminate instance API/DB; release static IP.
- Secrets Manager: xóa secrets `DB_PASSWORD`, `APP_CONFIG`.
- CloudWatch: xóa log group/alarm; tắt export.
- Route 53/ACM: gỡ record/chứng chỉ không dùng.
