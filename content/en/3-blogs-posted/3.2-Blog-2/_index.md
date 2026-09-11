---
title: "blog-2"
weight: 2
---

## AWS MARKETPLACE: WHEN CONTRACT RENEWAL IS ALSO AUTOMATED

🔹 **The problem**

According to the article, most contract renewals are not really a new decision — the buyer is still using the service successfully and wants to continue, while the seller also wants to retain the customer. Neither side actually wants to stop, but the renewal date can still pass simply because of administrative procedures: creating the offer again, waiting for approval again, and signing again. The problem becomes even greater as the number of contracts that need to be renewed increases.

🔹 **How it works**

The seller and buyer only need to agree on the original terms AND the future renewal terms once, at the time the offer is created. After that, each cycle renews automatically — keeping the price, duration, currency, payment terms, and attached license agreement unchanged — without anyone having to click "Accept" again. Both sides still have the right to opt out of the renewal if they want to stop.

🔹 **3 pricing methods for renewal**

- Flat renewal: keeps exactly the same price as the original across renewal cycles.
- Fixed percentage uplift: increases the price by a fixed percentage each time it renews (with compounding — for example, with a 2% annual increase, a $10,000 contract becomes $10,200 and then $10,404 in the next cycle).
- Percentage range uplift: sets a predefined percentage increase range (min–max), with the exact percentage finalized closer to the renewal date — suitable when pricing needs to follow inflation or an index such as CPI.

🔹 **Notifications & integration**

Both parties are notified at important milestones: an upcoming renewal, the price adjustment deadline, the opt-out deadline, and when the renewal is completed. These events can also be sent through Amazon EventBridge, so they can be connected to the company’s CRM, billing system, or internal alerting — quite seamless with the way the MP-Buyer Portal in the previous article uses EventBridge to synchronize data every 6 hours.

🔹 **Benefits for buyers**

The service does not get interrupted between contract periods, the full renewal schedule can be viewed in one place, pricing is known in advance (there is no need to negotiate again), and renewal transactions still count toward the committed spend with AWS.

🔹 **Personal impression**

When combined with the MP-Buyer Portal article from last week, I feel AWS is addressing the "software procurement" problem from both ends: on one side, making it easier to find and purchase new products through APIs; on the other side, making it less labor-intensive to maintain existing contracts. Both follow the same spirit — reduce the amount of "manual work" so that procurement teams can spend more time on real decisions instead of chasing paperwork deadlines.


![Renewal terms configuration interface when creating a private offer on AWS Marketplace](/QuangThienWorkshop-template/images/private-offer-auto-renewals-renewal-terms.png)

*Renewal terms configuration interface when creating a private offer on AWS Marketplace — excerpt from the original article, source: AWS Marketplace Blog.*

📌 **Source:** Erin Smith and Alastair Campbell, "Private offer auto-renewals: Scale predictable revenue with AWS Marketplace", AWS Marketplace Blog, 02/09/2026.

🔗 [https://aws.amazon.com/blogs/awsmarketplace/private-offer-auto-renewals-scale-predictable-revenue-with-aws-marketplace/](https://aws.amazon.com/blogs/awsmarketplace/private-offer-auto-renewals-scale-predictable-revenue-with-aws-marketplace/)

**#AWS** **#AWSMarketplace** **#CloudComputing** **#Internship** **#Procurement**
