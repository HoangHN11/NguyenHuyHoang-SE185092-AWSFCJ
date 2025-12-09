---
title: "Trực quan hóa Analytics với Shiny Dashboards"
weight: 2
chapter: false
pre: " <b> 5.5. </b> "
---

## 5.5.1 Lộ trình trực quan hóa thực dụng

Với phạm vi hiện tại, bắt đầu từ những gì sẵn có:

- **CloudWatch Log Insights**: lưu query cho latency, 5xx/4xx, lỗi auth, đếm sự kiện (`product_view`, `add_to_cart`, `checkout_*`).
- **Athena (nếu export bật)**: SQL trên log JSON xuất để dựng funnel và độ phổ biến sản phẩm.
- **QuickSight (tùy chọn)**: Dashboard nhẹ trên Athena; giữ SPICE nhỏ.

---

## 5.5.2 Gợi ý truy vấn CloudWatch

- **Độ tin cậy**: tỷ lệ lỗi, p95 theo route; endpoint lỗi nhiều; lỗi auth.
- **Hành vi**: đếm theo `eventName`; độ phổ biến sản phẩm (`productId`, `category`); tỷ lệ hoàn tất checkout.
- **Upload**: thành công vs lỗi cho presigned PUT (lọc `statusCode`, `path`).

Lưu query và ghim lên CloudWatch dashboard để theo dõi nhanh.

---

## 5.5.3 Nếu dùng Athena/QuickSight

1) Export CloudWatch logs sang S3 hằng ngày.  
2) Tạo external table trên JSON; partition theo ngày.  
3) Ví dụ metric:  
   - Số sự kiện theo thời gian, phân bổ `eventName` theo `userLoginState`.  
   - Product views vs add_to_cart vs checkout_complete.  
   - Tỷ lệ lỗi và p95 theo route.  
4) Trong QuickSight, dựng 3 biểu đồ:  
   - KPI tiles (tổng sự kiện, lỗi, p95).  
   - Funnel (product_view → add_to_cart → checkout_start → checkout_complete).  
   - Top sản phẩm (views và carts).

---

## 5.5.4 Truy cập và bảo mật

- Giữ bucket export ở trạng thái private; giới hạn quyền Athena/QuickSight cho admin dự án.
- Dùng IAM boundary: analyst read-only, ops write khi cần.
- Không public dashboard; chia sẻ qua console AWS hoặc PDF export nếu cần.