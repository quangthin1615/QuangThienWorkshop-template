---
title: "Kết nối Amazon S3 từ VPC bằng VPC Endpoint"
weight: 2
---

## 1. Tổng quan

Workload trong Amazon VPC thường cần đọc hoặc ghi dữ liệu vào Amazon S3. VPC Endpoint cung cấp điểm truy cập riêng từ VPC đến dịch vụ AWS được hỗ trợ.

Đối với S3, hai lựa chọn quan trọng là **Gateway VPC Endpoint** và **Interface VPC Endpoint**.

![VPC kết nối S3](/images/blog2-01-vpc-s3.png)

## 2. Gateway VPC Endpoint

Gateway endpoint là lựa chọn phổ biến cho workload trong VPC truy cập S3 trong Region. Route table được cấu hình để traffic đến S3 sử dụng endpoint.

Mô hình này không cần Internet Gateway hoặc NAT Gateway chỉ để truy cập S3.

![Gateway VPC Endpoint](/images/blog2-02-gateway-endpoint.png)

Ưu điểm:
- đơn giản;
- phù hợp với EC2 trong VPC;
- có thể dùng endpoint policy;
- thường có lợi thế về chi phí.

## 3. Interface VPC Endpoint

Interface endpoint sử dụng AWS PrivateLink. AWS tạo Elastic Network Interface với private IP trong subnet được chọn.

Workload kết nối đến private IP của endpoint và traffic đi qua mạng AWS.

![Interface VPC Endpoint](/images/blog2-03-interface-endpoint.png)

Mô hình này phù hợp với các yêu cầu private connectivity rộng hơn, bao gồm một số kiến trúc có on-premises và PrivateLink.

## 4. So sánh

| Tiêu chí | Gateway Endpoint | Interface Endpoint |
|---|---|---|
| Công nghệ | Route table | AWS PrivateLink |
| S3 | Có | Có |
| Thành phần | Route table | ENI/private IP |
| Phù hợp | Workload trong VPC | PrivateLink/private connectivity |
| Chi phí | Thường tiết kiệm hơn | Có phí endpoint và data processing |

## 5. Security

Private connectivity không đồng nghĩa với quyền truy cập không giới hạn. Nên kết hợp IAM policy, S3 bucket policy, endpoint policy và nguyên tắc least privilege. Với interface endpoint, security group cũng là thành phần quan trọng.

## 6. Ví dụ

**EC2 private subnet → Route Table → S3 Gateway Endpoint → Amazon S3**

EC2 không cần public IP hoặc NAT Gateway chỉ để truy cập S3.

## 7. Bài học rút ra

VPC Endpoint là thành phần quan trọng trong thiết kế mạng AWS theo hướng private-by-design. Gateway endpoint thường phù hợp cho workload trong VPC truy cập S3, trong khi interface endpoint phục vụ các yêu cầu PrivateLink rộng hơn.
## 8. Tài liệu tham khảo

1. [Choosing Your VPC Endpoint Strategy for Amazon S3 – AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/choosing-your-vpc-endpoint-strategy-for-amazon-s3/)

2. [Reduce Cost and Increase Security with Amazon VPC Endpoints – AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/reduce-cost-and-increase-security-with-amazon-vpc-endpoints/)

3. [Introducing private DNS support for Amazon S3 with AWS PrivateLink – AWS Storage Blog](https://aws.amazon.com/blogs/storage/introducing-private-dns-support-for-amazon-s3-with-aws-privatelink/)
