---
title: "Triển khai Clickstream Ingestion"
weight: 2
chapter: false
pre: " <b> 5.3. </b> "
---

## 5.3.1 “Ingestion” trong AWS Jewelry Web

Giữ nhẹ nhàng bằng cách tận dụng Lightsail API + CloudWatch structured logs, không dựng pipeline riêng.

- Frontend React phát các sự kiện: `page_view`, `product_view`, `add_to_cart`, `checkout_start`, `checkout_complete`.
- Sự kiện POST tới **Lightsail API**, được validate và log JSON vào **CloudWatch Logs**.
- Upload ảnh dùng **presigned URL** từ API; CloudFront đọc ảnh trong bucket S3 private.

Đủ nhu cầu quan sát, vẫn nằm trong phạm vi/chi phí dự án.

---

## 5.3.2 Schema sự kiện/log (đề xuất)

- Danh tính: `userId` (nếu đã đăng nhập), `clientId`, `sessionId`, `userLoginState`, `identitySource`.
- Sự kiện: `eventName`, `eventTimestamp`.
- Ngữ cảnh sản phẩm: `productId`, `name`, `category`, `brand`, `price`, `discountPrice`, `urlPath`.
- Request/meta: `path`, `method`, `statusCode`, `latencyMs`, `userAgent`, `sourceIp`, `requestId`.

Lưu JSON cấu trúc trong CloudWatch để xuất/đọc lại sau.

---

## 5.3.3 Trách nhiệm API

- `/events`: nhận payload hợp lệ; từ chối loại sự kiện lạ.
- Presigned uploads: cấp PUT URL kèm ràng buộc content-type và key.
- Secrets: lấy `DB_PASSWORD`, `APP_CONFIG` (bucket) từ **Secrets Manager**; không hardcode.
- Logging: ghi CloudWatch cho auth thành/không, CRUD, upload, và sự kiện business.

---

## 5.3.4 Kết nối Frontend

- Dùng JWT Cognito cho request bảo vệ; khách dùng `clientId` + `sessionId` sinh cục bộ.
- Lưu `clientId` (localStorage) và `sessionId` (sessionStorage) với timeout.
- Gửi POST không chặn UI; retry tùy chọn nhưng không gây lag.
- Luồng upload: xin presigned URL → PUT file lên S3 → gửi metadata/key về API.

---

## 5.3.5 Checklist kiểm thử

1. Gây sự kiện (duyệt, xem sản phẩm, thêm giỏ, bắt đầu/hoàn tất checkout).  
2. Đảm bảo API trả 2xx; kiểm PUT S3 thành công qua presigned URL.  
3. Kiểm CloudWatch Logs có JSON đầy đủ trường danh tính/sản phẩm.  
4. Xác nhận đọc Secrets Manager (không hardcode DB/bucket).  
5. Kiểm CORS + HTTPS end-to-end; CloudFront đọc bucket ảnh, upload vẫn private.
6. 