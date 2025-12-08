---
title: "Blog 1"
date: 2025-10-08
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
---

# Cách iFood xây dựng nền tảng để chạy hàng trăm mô hình machine learning với Amazon SageMaker Inference

*Bởi Daniel Vieira, Debora Fanin, Gopi Mudiyala và Saurabh Trikande – ngày 08 tháng 4 năm 2025, trong chuyên mục Nâng cao (300), Amazon SageMaker Data & AI Governance, Customer Solutions.*

---

## Giới thiệu

Có trụ sở chính tại São Paulo, Brazil, **iFood** là một công ty tư nhân quốc gia và là công ty hàng đầu trong lĩnh vực công nghệ thực phẩm ở Mỹ Latinh, xử lý hàng triệu đơn đặt hàng hàng tháng. iFood nổi bật với chiến lược kết hợp công nghệ tiên tiến vào hoạt động của mình. Với sự hỗ trợ của **AWS**, iFood đã phát triển cơ sở hạ tầng suy luận **machine learning (ML)** mạnh mẽ, sử dụng các dịch vụ như **Amazon SageMaker** để tạo và triển khai các mô hình ML một cách hiệu quả. Sự hợp tác này đã cho phép iFood không chỉ tối ưu hóa các quy trình nội bộ mà còn cung cấp các giải pháp sáng tạo cho các đối tác giao hàng và nhà hàng của mình.

Nền tảng ML của iFood bao gồm một tập hợp các công cụ, quy trình và workflow được phát triển với các mục tiêu chính:
- Đẩy nhanh quá trình phát triển và đào tạo các mô hình AI/ML, làm cho chúng đáng tin cậy và dễ tái tạo hơn.
- Đảm bảo rằng việc triển khai các mô hình này vào sản xuất là đáng tin cậy, có thể mở rộng và có thể truy xuất nguồn gốc.
- Tạo điều kiện thuận lợi cho việc thử nghiệm, giám sát và đánh giá các mô hình trong sản xuất một cách minh bạch, dễ tiếp cận và tiêu chuẩn hóa.

![Ảnh blog 1 - 1](/images/3-BlogImage/blog1-1.png)
> *Hình 1. Minh họa tổng quan — iFood và ứng dụng AI/ML trong hệ thống sản phẩm.*

---

## Mục tiêu và cách tiếp cận

Để đạt được những mục tiêu trên, iFood tận dụng **SageMaker** để đơn giản hóa việc huấn luyện và triển khai mô hình. Việc tích hợp các tính năng của SageMaker trong cơ sở hạ tầng của iFood tự động hóa các bước quan trọng — từ tạo dataset huấn luyện, huấn luyện mô hình, triển khai mô hình vào production đến liên tục theo dõi hiệu suất.

Bài viết này trình bày cách iFood sử dụng SageMaker để cải tiến toàn bộ vòng đời ML — từ huấn luyện đến suy luận — đồng thời mô tả những thay đổi kiến trúc và các khả năng mà đội ngũ đã phát triển.

---

## Suy luận AI tại iFood

iFood khai thác nền tảng AI/ML để nâng cao trải nghiệm khách hàng trên nhiều điểm tiếp xúc. Một số trường hợp sử dụng điển hình:

- **Đề xuất cá nhân hóa** — Mô hình phân tích lịch sử đặt hàng, sở thích và ngữ cảnh để đề xuất nhà hàng và món ăn phù hợp, giúp tăng mức độ hài lòng và số lượng đơn hàng.
- **Theo dõi đơn hàng thông minh** — Hệ thống dự đoán thời gian giao hàng theo thời gian thực bằng cách kết hợp dữ liệu giao thông, thời gian chuẩn bị nhà hàng và vị trí shipper, từ đó thông báo chủ động cho khách.
- **Dịch vụ khách hàng tự động** — Chatbot AI xử lý hàng nghìn yêu cầu phổ biến mỗi ngày, cung cấp phản hồi nhanh và có thể truy xuất dữ liệu liên quan để hỗ trợ cá nhân hóa.
- **Hỗ trợ mua sắm hàng tạp hóa** — Ứng dụng tích hợp mô hình ngôn ngữ giúp khách hàng tạo danh sách mua sắm từ yêu cầu bằng giọng nói hoặc văn bản.

Nhờ những sáng kiến này, iFood có thể dự đoán nhu cầu, tối ưu hoá quy trình và cung cấp trải nghiệm nhất quán cho người dùng.

---

## Tổng quan về giải pháp (Kiến trúc kế thừa)

Sơ đồ dưới đây minh họa kiến trúc kế thừa của iFood, trong đó các nhóm Data Science và Engineering có workflow tách biệt — chính điều này gây ra thách thức khi triển khai mô hình ML thời gian thực vào production.

![Ảnh blog 1 - 2](/images/3-BlogImage/blog1-2.jpg)
> *Hình 2. Kiến trúc kế thừa — mô tả luồng dữ liệu và rào cản giữa các nhóm.*

Trước đây, các nhà khoa học dữ liệu thường phát triển mô hình trong notebook, tinh chỉnh và xuất bản artifact. Các kỹ sư sau đó phải tích hợp các artifact này vào hệ thống production, dẫn tới độ trễ và lỗi tích hợp. Để khắc phục, iFood đã phát triển một nền tảng ML nội bộ nhằm hợp nhất quy trình từ phát triển đến triển khai, tạo trải nghiệm liền mạch cho cả hai bên.

---

## Kiến trúc cập nhật và ML Go!

Một trong các khả năng cốt lõi của nền tảng ML của iFood là cung cấp cơ sở hạ tầng để phục vụ dự đoán. Nền tảng nội bộ (gọi là **ML Go!**) chịu trách nhiệm triển khai quy trình, quản lý SageMaker Endpoints và Jobs. ML Go! hỗ trợ cả dự đoán ngoại tuyến (batch) và dự đoán thời gian thực (online), đồng thời quản lý lifecycle của mô hình (registry, versioning, monitoring).

![Ảnh blog 1 - 3](/images/3-BlogImage/blog1-3.jpg)
> *Hình 3. Kiến trúc cập nhật — bao gồm pipeline, model registry và component cho inference.*

Nền tảng cung cấp:
- ML pipelines tự động (SageMaker Pipelines) để huấn luyện và tái huấn luyện mô hình.
- ML Go! CI/CD để đẩy artifact, build Docker image, và kích hoạt pipeline.
- SageMaker Model Registry để versioning và quản lý mô hình.
- Cơ chế monitoring để phát hiện drift và cảnh báo hiệu năng suy giảm.

---

## Kiến trúc cuối cùng: inference components & ML Go! Gateway

Một cải tiến lớn là khái niệm trừu tượng hóa để kết nối với SageMaker (Endpoints & Jobs) gọi là **ML Go! Gateway**, cùng với tách biệt “inference components” trong endpoint — giúp phân chia mối quan tâm, tăng tốc phân phối và quản lý tài nguyên hiệu quả hơn. Các endpoint giờ đây quản lý nhiều thành phần suy luận (component-based inference), và ML Go! CI/CD chỉ lo phần quảng bá phiên bản mô hình (model promotion), không can thiệp sâu vào tầng hạ tầng.

![Ảnh blog 1 - 4](/images/3-BlogImage/blog1-4.jpg)
> *Hình 4. Kiến trúc cuối cùng — inference components, ML Go! Gateway và tích hợp với service accounts.*

Trong cấu trúc mới:
- Endpoints có thể chứa nhiều component inference, cho phép phân tải công việc, chia theo tải hoặc chức năng.
- ML Go! Dispatcher/ Gateway đóng vai trò chuyển tiếp yêu cầu tới đúng endpoint hoặc job.
- CI/CD xử lý artifacts (Docker images, configs), SageMaker Pipeline orchestrates training → evaluation → registry → deployment.

---

## Sử dụng SageMaker Inference Model Serving Containers

Tiêu chuẩn hóa môi trường bằng container là yếu tố quyết định của nền tảng ML hiện đại. SageMaker cung cấp các container dựng sẵn cho TensorFlow, PyTorch, XGBoost… đồng thời cho phép đưa container tùy chỉnh.

iFood tập trung sử dụng **container tùy chỉnh** (custom containers) để:
- Chuẩn hóa mã ML (không dùng trực tiếp notebook vào production).
- Đóng gói dependency, thư viện và logic inference trong image (ví dụ: BruceML scaffolding).
- Dễ dàng tái tạo môi trường huấn luyện và phục vụ, theo dõi kết quả và debug.

BruceML giúp chuẩn hóa cách viết mã huấn luyện và phục vụ, tạo scaffold tương thích với SageMaker (autotuning, deployment hooks, monitoring).

---

## Tự động hóa triển khai và đào tạo lại (ML pipelines & CI/CD)

iFood dùng **SageMaker Pipelines** để xây dựng CI/CD cho ML: pipelines chịu trách nhiệm orchestrate toàn bộ luồng dữ liệu — từ data preprocessing, training, evaluation, tới promotion vào Model Registry và deployment. ML Go! CI/CD tích hợp với hệ thống CI/CD của tổ chức để:
- Đẩy artifact (code + container image).
- Kích hoạt pipeline huấn luyện và đánh giá.
- Tự động đăng ký mô hình đạt chuẩn vào Model Registry.
- Triển khai hoặc promote mô hình lên endpoint phù hợp (online / batch).

Tùy theo SLA:
- **Batch inference**: sử dụng SageMaker Transform jobs cho dự đoán quy mô lớn.
- **Real-time inference**: triển khai mô hình tới SageMaker Endpoint với cấu hình container/instance phù hợp.

SageMaker Pipelines giúp tự động hóa và điều phối các workflow phức tạp, giảm sai sót và rút ngắn vòng lặp phát triển.

---

## Chạy suy luận ở các định dạng SLA khác nhau

iFood tận dụng nhiều phương thức suy luận để đáp ứng các yêu cầu khác nhau:
- **Real-time endpoints** cho các tác vụ cần latency thấp (user-facing).
- **Batch transform jobs** cho xử lý dữ liệu quy mô lớn, tính toán gợi ý định kỳ.
- **Asynchronous inference** (SageMaker Asynchronous Inference) cho các tác vụ suy luận tốn thời gian.
- **Multi-model endpoints (GPU)** để host nhiều mô hình trên cùng một GPU endpoint, tối ưu sử dụng tài nguyên.

Những cải tiến hợp tác giữa iFood và đội SageMaker Inference bao gồm:
- Tối ưu hóa chi phí và hiệu suất cho inference (giảm ~50% chi phí cho một số workloads, giảm ~20% latency trung bình khi dùng inference components).
- Cải tiến autoscaling để xử lý spikes hiệu quả hơn (rút ngắn thời gian scale, cải thiện phát hiện scale events).
- Hỗ trợ triển khai LLM / Foundation Models (FM) dễ dàng hơn.
- Tính năng **scale-to-zero** cho endpoints giúp tiết kiệm chi phí khi không có traffic.
- Multi-model GPU endpoints giúp giảm chi phí cơ sở hạ tầng cho trường hợp nhiều mô hình.

---

## Tối ưu hóa và đóng gói mô hình

Một số điểm kỹ thuật iFood tập trung:
- Chuẩn hóa container cho cả training và serving.
- Tự động hóa build/publish images lên registry (ECR).
- Đóng gói LLM / FM để triển khai nhanh hơn.
- Hỗ trợ autoscaling và scale-to-zero cho môi trường dev/test và low-traffic workloads.

---

## Lợi ích đạt được & tác động

Những lợi ích iFood thu được:
- Giảm thời gian đưa mô hình vào production (faster time-to-market).
- Tăng khả năng tái sử dụng pipeline & artifacts giữa các nhóm.
- Hạ chi phí vận hành nhờ tối ưu GPU/multi-model và scale-to-zero.
- Cải thiện độ ổn định và khả năng quản lý mô hình ở quy mô lớn.

---

## Kết luận

Sử dụng các khả năng của SageMaker, iFood đã chuyển đổi cách tiếp cận ML/AI: xây dựng nền tảng ML tập trung (ML Go!), tự động hóa luồng dữ liệu, chuẩn hóa container và hợp tác cùng nhóm SageMaker Inference để tối ưu tính hiệu quả, chi phí và khả năng mở rộng. Việc này đã giúp iFood:
- Thu hẹp khoảng cách giữa Data Science và Engineering.
- Triển khai hàng trăm mô hình ML một cách đáng tin cậy.
- Tạo nền tảng tham chiếu cho các tổ chức muốn ứng dụng inference ở quy mô lớn.

> *“Tại iFood, chúng tôi đi đầu trong việc áp dụng công nghệ AI và máy học biến đổi... Các bài học đã học được hỗ trợ chúng tôi trong việc tạo ra nền tảng nội bộ, có thể đóng vai trò như một kế hoạch chi tiết cho các tổ chức khác...”*  
> – Daniel Vieira, Giám đốc Nền tảng ML tại iFood.

---

## Giới thiệu về các tác giả

![Daniel Vieira](/images/3-BlogImage/blog1-5.png)  
**Daniel Vieira** — Giám đốc Kỹ thuật Học máy tại iFood. Có nền tảng khoa học máy tính (BSc & MSc, UFMG) và hơn một thập kỷ kinh nghiệm về kỹ thuật phần mềm và nền tảng ML. Thích âm nhạc, triết học và cà phê.

---

![Debora Fanin](/images/3-BlogImage/blog1-6.png)  
**Debora Fanin** — Giám đốc giải pháp khách hàng cấp cao, AWS (Brazil). Chuyên quản lý chuyển đổi khách hàng doanh nghiệp, thiết kế các chiến lược áp dụng đám mây hiệu quả về chi phí.

---

![Saurabh Trikande](/images/3-BlogImage/blog1-7.png)  
**Saurabh Trikande** — Giám đốc sản phẩm cấp cao, Amazon Bedrock & SageMaker Inference. Tập trung vào dân chủ hóa AI và giải pháp suy luận ở quy mô lớn.

---

![Gopi Mudiyala](/images/3-BlogImage/blog1-8.jpg)  
**Gopi Mudiyala** — Giám đốc tài khoản kỹ thuật cấp cao, AWS. Hỗ trợ khách hàng ngành dịch vụ tài chính và đam mê máy học.