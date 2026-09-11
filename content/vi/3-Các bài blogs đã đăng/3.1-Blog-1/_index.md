---
title: "blog-1"
weight: 1
---

# TÌM HIỂU VỀ AWS MARKETPLACE APIs: ĐƯA QUY TRÌNH MUA SẮM PHẦN MỀM VÀO NGAY TRONG WORKFLOW NỘI BỘ

🔹 **Vấn đề đặt ra**

AWS Marketplace vốn mang lại nhiều lợi ích: gộp hóa đơn với AWS, điều khoản đàm phán sẵn, đa dạng nhà cung cấp, dễ kiểm soát tuân thủ. Nhưng nhiều khách hàng không muốn cứ phải mở AWS Console mỗi lần cần tìm sản phẩm hay quản lý subscription. Họ muốn các thao tác này được nhúng thẳng vào công cụ họ đang dùng, ví dụ chatbot Slack, tích hợp ServiceNow để duyệt yêu cầu IT, hay dashboard nội bộ báo cáo mua sắm.

🔹 **Giải pháp: MP-Buyer Portal**

AWS giới thiệu một solution mẫu dựa trên hai API chính:

- Discovery API: tìm kiếm, lọc, so sánh sản phẩm trong catalog.
- Agreement API: quản lý subscription theo cách lập trình.

Ba chức năng chính:

1️⃣ Quản lý agreement — xem, lọc, kiểm tra chi tiết subscription hiện có.

2️⃣ Tìm kiếm & đăng ký sản phẩm — so sánh gói, subscribe trực tiếp qua API.

3️⃣ Báo cáo — tự động tạo báo cáo chi tiêu, cảnh báo hết hạn, audit compliance, có thể bật thêm phân tích AI qua Strands Agents (chạy trên Claude, thông qua Amazon Bedrock).

🔹 **Kiến trúc giải pháp**

Điểm mình thích nhất là kiến trúc hoàn toàn serverless, gần như không tốn chi phí khi hệ thống idle: CloudFront + S3 phục vụ frontend, API Gateway + Lambda xử lý logic (agreement/tìm kiếm/đăng ký, báo cáo AI, đồng bộ dữ liệu), DynamoDB cache dữ liệu, Cognito xác thực JWT, EventBridge kích hoạt đồng bộ mỗi 6 tiếng.

![Kiến trúc MP-Buyer Portal](/QuangThienWorkshop-template/images/mp-buyer-architecture6-3v2fig1.drawio-1024x714.png)

🔹 **Luồng đăng ký sản phẩm (5 bước qua API)**

ListPurchaseOptions → GetOffer → GetOfferTerms → CreateAgreementRequest → AcceptAgreementRequest.

Về bản chất giống hệt AWS Console làm, chỉ khác là chạy hoàn toàn qua API trên giao diện tự xây dựng — cho phép cả người không có quyền truy cập Console cũng dùng được.

🔹 **Cảm nhận cá nhân**

Đây là ví dụ thực tế về cách biến thao tác "bắt buộc vào Console" thành workflow tự phục vụ cho team procurement, mà vẫn giữ nguyên lợi ích gốc của Marketplace. Phần tích hợp AI để tự sinh báo cáo tóm tắt cũng là hướng hay để áp dụng AI vào vận hành hằng ngày, không chỉ dừng ở chatbot.

📌 **Nguồn:** Kenneth Walsh, "How you can embed procurement into your workflows with AWS Marketplace APIs", AWS Marketplace Blog, 04/09/2026.

🔗 [https://aws.amazon.com/blogs/awsmarketplace/how-you-can-embed-procurement-into-your-workflows-with-aws-marketplace-apis/](https://aws.amazon.com/blogs/awsmarketplace/how-you-can-embed-procurement-into-your-workflows-with-aws-marketplace-apis/)

**#AWS** **#AWSMarketplace** **#CloudComputing** **#Internship** **#Serverless**