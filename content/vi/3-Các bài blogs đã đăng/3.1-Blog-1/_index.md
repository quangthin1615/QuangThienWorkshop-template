---
title: "Giám sát Amazon EC2 bằng Amazon CloudWatch và cảnh báo tự động"
weight: 1
---


## 1. Tổng quan

Khi triển khai ứng dụng trên Amazon EC2, việc instance đang chạy không đồng nghĩa hệ thống luôn khỏe mạnh. CPU có thể tăng đột biến, lưu lượng mạng bất thường hoặc tài nguyên tiến gần giới hạn. Vì vậy cần một cơ chế theo dõi, phát hiện và cảnh báo.

Amazon CloudWatch cung cấp khả năng thu thập, trực quan hóa metric, xây dựng dashboard và tạo CloudWatch Alarm. Với EC2, các metric thường được theo dõi gồm CPUUtilization, NetworkIn, NetworkOut, DiskReadOps và DiskWriteOps.

![Kiến trúc EC2 và CloudWatch](/images/blog1-01-ec2-cloudwatch.png)

## 2. Kiến trúc

Luồng cơ bản:

**Amazon EC2 → CloudWatch Metrics → CloudWatch Dashboard/Alarm → thông báo hoặc hành động vận hành**

EC2 phát sinh metric; CloudWatch tiếp nhận và lưu trữ metric. Alarm đánh giá metric theo điều kiện đã cấu hình và thay đổi trạng thái khi điều kiện được đáp ứng.

![Luồng metric EC2 vào CloudWatch](/images/blog1-02-cloudwatch-metric.png)

## 3. Theo dõi CPU

CPUUtilization là metric dễ sử dụng để bắt đầu giám sát. Ví dụ, CPU duy trì trên 80% trong một khoảng thời gian có thể là dấu hiệu workload tăng hoặc ứng dụng gặp vấn đề.

Biểu đồ giúp xác định mức bình thường, thời điểm tải tăng, các spike và xu hướng dài hạn. Ngưỡng nên dựa trên workload thực tế thay vì đặt tùy ý.

## 4. CloudWatch Alarm

Một alarm có thể sử dụng:

- Metric: EC2 CPUUtilization
- Statistic: Average
- Period: 5 phút
- Threshold: lớn hơn 80%
- Action: gửi thông báo qua SNS

Khi điều kiện thỏa mãn, alarm chuyển sang **ALARM**. Khi metric trở lại vùng an toàn, alarm có thể trở về **OK**.

![CloudWatch Alarm](/images/blog1-03-cloudwatch-alarm.png)

## 5. Ví dụ thực tế

Một web server bình thường sử dụng CPU 20–40%. Khi có lượng truy cập lớn, CPU vượt 80%.

Quy trình:

1. EC2 phát sinh CPU cao.
2. CloudWatch ghi nhận metric.
3. Alarm đánh giá điều kiện.
4. Alarm chuyển sang ALARM.
5. SNS có thể gửi thông báo.
6. Quản trị viên kiểm tra ứng dụng và log.
7. Khi tải giảm, alarm trở về OK.

## 6. Bài học rút ra

Giám sát không chỉ là xem biểu đồ. Giá trị nằm ở việc biến metric thành thông tin có thể hành động, tạo thành chu trình **monitor → detect → alert → respond**.

## 7. Nguồn tham khảo

- [AWS News Blog – Amazon CloudWatch – Alarm Actions](https://aws.amazon.com/blogs/aws/amazon-cloudwatch-alarm-actions/)

- [AWS Compute Blog – Automating Amazon EC2-Windows EBS Volumes monitoring and creating alarms](https://aws.amazon.com/blogs/compute/automating-amazon-ec2-windows-ebs-volumes-monitoring-and-creating-alarms/)