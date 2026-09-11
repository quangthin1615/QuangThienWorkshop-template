---
title: "3-Các bài blogs đã đăng"
weight: 3
---

Trong thời gian thực tập, mình đã nghiên cứu và tổng hợp **hai chủ đề blog kỹ thuật liên quan đến Amazon Web Services (AWS)**, tập trung vào **AWS Marketplace, mua sắm phần mềm, kiến trúc serverless và tự động hóa quy trình mua sắm**. Những chủ đề này giúp củng cố hiểu biết thực tế của mình về việc tích hợp các dịch vụ AWS vào workflow doanh nghiệp và tự động hóa các quy trình mua sắm phần mềm.

| **#** | **Đề tài** | **Phạm trù** | **Ngày đăng** | **Chứng minh Facebook** |
|---|---|---|---|---|
| Blog 1 | **Tìm hiểu về AWS Marketplace APIs: Đưa quy trình mua sắm phần mềm vào ngay trong workflow nội bộ** | AWS Marketplace & Serverless Architecture | 09/09/2026 | [Nguyen Thau](https://www.facebook.com/profile.php?id=61592819087978) |
| Blog 2 | **Tiếp nối chủ đề AWS Marketplace: Khi việc gia hạn hợp đồng cũng được tự động hóa** | AWS Marketplace & Procurement Automation | 11/09/2026 | [Nguyen Thau](https://www.facebook.com/profile.php?id=61592819087978) |

---

### [3.1 Blog 1 – Tìm hiểu về AWS Marketplace APIs: Đưa quy trình mua sắm phần mềm vào ngay trong workflow nội bộ](3.1-Blog-1/)

AWS Marketplace mang lại nhiều lợi ích: gộp hóa đơn với AWS, các điều khoản được đàm phán sẵn, nhiều nhà cung cấp và quản lý tuân thủ dễ dàng hơn. Tuy nhiên, nhiều khách hàng không muốn liên tục mở AWS Console mỗi khi cần tìm một sản phẩm hoặc quản lý một subscription. Họ muốn các thao tác này được nhúng trực tiếp vào những công cụ mà họ đang sử dụng, chẳng hạn như chatbot Slack, tích hợp ServiceNow để phê duyệt các yêu cầu IT, hoặc một dashboard nội bộ để báo cáo hoạt động mua sắm.

AWS giới thiệu một solution mẫu dựa trên hai API chính:

- **Discovery API**: tìm kiếm, lọc và so sánh các sản phẩm trong catalog.
- **Agreement API**: quản lý subscription theo cách lập trình.

Giải pháp cung cấp ba chức năng chính:

- **Quản lý agreement** — xem, lọc và kiểm tra chi tiết các subscription hiện có.
- **Tìm kiếm và đăng ký sản phẩm** — so sánh các gói và subscribe trực tiếp thông qua API.
- **Báo cáo** — tự động tạo báo cáo chi tiêu, cảnh báo hết hạn, thông tin audit compliance và tùy chọn bật phân tích bằng AI thông qua Strands Agents chạy trên Claude thông qua Amazon Bedrock.

Giải pháp sử dụng kiến trúc serverless bao gồm **CloudFront + S3** cho frontend, **API Gateway + Lambda** cho logic ứng dụng, **DynamoDB** để cache dữ liệu, **Cognito** để xác thực JWT và **EventBridge** cho việc đồng bộ theo lịch.

Quy trình đăng ký sản phẩm có thể được triển khai thông qua năm bước API chính:

**ListPurchaseOptions → GetOffer → GetOfferTerms → CreateAgreementRequest → AcceptAgreementRequest**

Cách tiếp cận này biến các thao tác vốn truyền thống yêu cầu truy cập AWS Console thành một workflow self-service được nhúng trực tiếp vào các hệ thống doanh nghiệp nội bộ.

---

### [3.2 Blog 2 – Tiếp nối chủ đề AWS Marketplace: Khi việc gia hạn hợp đồng cũng được tự động hóa](3.2-Blog-2/)

Phần lớn các lần gia hạn hợp đồng thực sự không phải là những quyết định mới. Bên mua vẫn đang sử dụng dịch vụ tốt và muốn tiếp tục, trong khi bên bán cũng muốn giữ khách hàng. Tuy nhiên, ngày gia hạn vẫn có thể bị trôi qua chỉ vì các thủ tục hành chính như tạo lại offer, chờ phê duyệt lại và ký lại.

**Private Offer Auto-Renewals** cung cấp một cách để tự động hóa quy trình này. Bên bán và bên mua có thể thống nhất các điều khoản ban đầu và các điều khoản gia hạn trong tương lai một lần khi offer được tạo. Sau đó, mỗi chu kỳ có thể tự động renew mà không cần thêm một lần chấp nhận thủ công.

Giải pháp cung cấp ba phương thức tính giá khi gia hạn:

- **Flat renewal** — giữ nguyên chính xác mức giá ban đầu trong các chu kỳ gia hạn.
- **Fixed percentage uplift** — tăng giá theo một tỷ lệ phần trăm cố định cho mỗi chu kỳ gia hạn, với tính lũy kép.
- **Percentage range uplift** — xác định mức tăng phần trăm tối thiểu và tối đa, với tỷ lệ chính xác được chốt gần thời điểm gia hạn.

Cả hai bên đều nhận được thông báo tại các mốc quan trọng, bao gồm ngày gia hạn sắp tới, thời hạn điều chỉnh giá, thời hạn opt-out và khi việc gia hạn hoàn tất. Các sự kiện gia hạn cũng có thể được tích hợp với **Amazon EventBridge**, cho phép kết nối với CRM, hệ thống billing và các hệ thống cảnh báo nội bộ.

Cách tiếp cận này giúp giảm công việc thủ công, ngăn ngừa gián đoạn dịch vụ, cung cấp mức giá gia hạn có thể dự đoán và giúp việc quản lý hợp đồng hiệu quả hơn.

---

## Tổng kết

Hai chủ đề blog bao quát hai khía cạnh quan trọng của AWS Marketplace:

1. **AWS Marketplace APIs** — đưa quy trình mua sắm phần mềm vào workflow nội bộ thông qua API và kiến trúc serverless.
2. **Private Offer Auto-Renewals** — tự động hóa việc gia hạn các hợp đồng phần mềm hiện có.

Kết hợp lại, hai chủ đề cho thấy AWS Marketplace có thể hỗ trợ cả **việc mua sắm phần mềm mới** và **quản lý hợp đồng đang sử dụng**, đồng thời giảm công việc vận hành thủ công.

Tài khoản Facebook được sử dụng để đăng các bài viết có thể được xác minh thông qua:

[**Nguyen Thau – Facebook**](https://www.facebook.com/profile.php?id=61592819087978)