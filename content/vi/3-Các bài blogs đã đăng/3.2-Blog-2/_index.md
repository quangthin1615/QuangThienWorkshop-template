---
title: "blog-2"
weight: 2
---
## TIẾP NỐI CHỦ ĐỀ AWS MARKETPLACE: KHI VIỆC GIA HẠN HỢP ĐỒNG CŨNG ĐƯỢC TỰ ĐỘNG HÓA
🔹 **Vấn đề đặt ra**

Theo bài viết, phần lớn các lần gia hạn hợp đồng không phải là một quyết định mới — bên mua vẫn đang dùng tốt và muốn tiếp tục, bên bán cũng muốn giữ khách. Không bên nào thật sự muốn dừng, nhưng ngày gia hạn vẫn có thể bị trôi qua chỉ vì thủ tục: phải tạo lại offer, chờ duyệt lại, ký lại. Vấn đề càng lớn khi số lượng hợp đồng cần gia hạn tăng lên.

🔹 **Cách hoạt động**

Người bán và người mua chỉ cần thống nhất điều khoản gốc VÀ điều khoản gia hạn tương lai một lần duy nhất, ngay khi tạo offer. Sau đó mỗi chu kỳ sẽ tự động renew — giữ nguyên giá, thời hạn, tiền tệ, điều khoản thanh toán, và cả hợp đồng license đính kèm — mà không cần ai bấm "Accept" lại. Cả hai bên vẫn có quyền từ chối gia hạn (opt-out) nếu muốn dừng.

🔹 **3 kiểu tính giá khi gia hạn**

- Flat renewal: giữ nguyên giá y hệt ban đầu qua các chu kỳ.
- Fixed percentage uplift: tăng giá theo % cố định mỗi lần renew (có tính lũy kép — ví dụ tăng 2%/năm, hợp đồng 10.000 đô sẽ thành 10.200 rồi 10.404 ở chu kỳ tiếp theo).
- Percentage range uplift: đặt trước một khoảng % tăng (min–max), sát ngày renew mới chốt số % cụ thể — phù hợp khi giá cần bám theo lạm phát hoặc chỉ số CPI.

🔹 **Thông báo & tích hợp**

Cả hai bên được thông báo tại các mốc quan trọng: sắp đến hạn renew, hạn chót điều chỉnh giá, hạn chót opt-out, và khi renew hoàn tất. Các sự kiện này còn được đẩy qua Amazon EventBridge, nên có thể tự nối vào hệ thống CRM, billing hoặc cảnh báo nội bộ của công ty — khá liền mạch với cách MP-Buyer Portal ở bài trước dùng EventBridge để đồng bộ dữ liệu mỗi 6 tiếng.

🔹 **Lợi ích cho bên mua**

Dịch vụ không bị gián đoạn giữa các kỳ hợp đồng, xem được toàn bộ lịch renew ở một nơi, giá cả biết trước từ đầu (không phải đàm phán lại), và các giao dịch renew vẫn được tính vào committed spend đã cam kết với AWS.

🔹 **Cảm nhận cá nhân**

Ghép với bài MP-Buyer Portal tuần trước, mình thấy AWS đang giải quyết bài toán "mua sắm phần mềm" ở cả hai đầu: một bên là làm cho việc tìm và mua sản phẩm mới dễ dàng hơn qua API, một bên là làm cho việc duy trì hợp đồng đã có bớt tốn công sức thủ công. Cả hai đều theo cùng một tinh thần — giảm phần "phải làm tay" xuống, để đội procurement dành thời gian cho quyết định thật sự, thay vì chạy theo deadline giấy tờ.


![Giao diện cấu hình renewal terms khi tạo private offer trên AWS Marketplace](/QuangThienWorkshop-template/images/private-offer-auto-renewals-renewal-terms.png)

*Giao diện cấu hình renewal terms khi tạo private offer trên AWS Marketplace - trích từ bài viết gốc, nguồn AWS Marketplace Blog.*

📌 **Nguồn:** Erin Smith và Alastair Campbell, "Private offer auto-renewals: Scale predictable revenue with AWS Marketplace", AWS Marketplace Blog, 02/09/2026.

🔗 [https://aws.amazon.com/blogs/awsmarketplace/private-offer-auto-renewals-scale-predictable-revenue-with-aws-marketplace/](https://aws.amazon.com/blogs/awsmarketplace/private-offer-auto-renewals-scale-predictable-revenue-with-aws-marketplace/)

**#AWS** **#AWSMarketplace** **#CloudComputing** **#Internship** **#Procurement**
