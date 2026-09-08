---
title: "Xây dựng kiến trúc Event-Driven với Amazon SQS và AWS Lambda"
weight: 3
---

## 1. Tổng quan

Trong ứng dụng hiện đại, các thành phần không nhất thiết phải gọi trực tiếp nhau. Producer có thể đưa message vào Amazon SQS, sau đó consumer xử lý bất đồng bộ.

Khi kết hợp SQS với AWS Lambda, hệ thống có thể mở rộng theo lượng message mà không cần quản lý server.

![Application - SQS - Lambda](/images/blog3-01-application-sqs-lambda.png)

Luồng cơ bản:

**Application/Producer → Amazon SQS → Lambda Event Source Mapping → AWS Lambda**

## 2. Vai trò của SQS

SQS hoạt động như một lớp đệm giữa producer và consumer. Khi traffic tăng đột biến, message được xếp hàng thay vì bắt consumer xử lý ngay.

Lợi ích:
- giảm coupling;
- hấp thụ burst;
- xử lý bất đồng bộ;
- hỗ trợ retry;
- cho phép consumer mở rộng độc lập.

![SQS Queue](/images/blog3-02-sqs-queue.png)

## 3. Lambda xử lý message

Lambda có thể dùng Event Source Mapping để đọc message từ SQS. Lambda polling queue và gọi function để xử lý batch.

Developer có thể tập trung vào business logic thay vì tự xây dựng polling infrastructure.

![Lambda processing](/images/blog3-03-lambda-processing.png)

## 4. Scaling và concurrency

Khi số message tăng, Lambda có thể tăng số execution để xử lý nhanh hơn. Tuy nhiên scale quá nhanh có thể gây áp lực cho database hoặc API phía sau.

AWS cung cấp maximum concurrency cho Lambda khi SQS là event source, giúp kiểm soát tốc độ xử lý và bảo vệ downstream.

## 5. Retry và DLQ

Message có thể thất bại do lỗi ứng dụng hoặc dependency. Sau số lần retry được cấu hình, message có thể chuyển sang Dead-Letter Queue.

DLQ giúp cô lập message lỗi, tránh retry vô hạn và hỗ trợ điều tra hoặc xử lý lại.

## 6. Ví dụ thực tế

Hệ thống thương mại điện tử:

1. Người dùng đặt hàng.
2. Application tạo message.
3. Message vào SQS.
4. Lambda nhận message.
5. Lambda kiểm tra và xử lý đơn hàng.
6. Nếu lỗi, message được retry.
7. Nếu tiếp tục thất bại, message chuyển vào DLQ.

## 7. Bài học rút ra

SQS cung cấp buffering và decoupling; Lambda cung cấp serverless processing và scaling. Khi thiết kế thực tế cần quan tâm idempotency, batch size, concurrency, downstream capacity và DLQ.

## 8. Nguồn tham khảo

1. [AWS – Maximum concurrency với Lambda và SQS](https://aws.amazon.com/blogs/compute/introducing-maximum-concurrency-of-aws-lambda-functions-when-using-amazon-sqs-as-an-event-source/)

2. [AWS – Faster polling scale-up cho Lambda và SQS](https://aws.amazon.com/blogs/compute/introducing-faster-polling-scale-up-for-aws-lambda-functions-configured-with-amazon-sqs/)

3. [AWS – Designing event-driven architectures](https://aws.amazon.com/blogs/architecture/lets-architect-designing-event-driven-architectures/)