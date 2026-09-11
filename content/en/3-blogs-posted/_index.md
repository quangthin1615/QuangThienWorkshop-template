---
title: "3-Blogs-Posted"
weight: 3
---

During my internship, I studied and summarized **two technical blog topics related to Amazon Web Services (AWS)**, focusing on **AWS Marketplace, software procurement, serverless architecture, and procurement automation**. These topics helped strengthen my practical understanding of integrating AWS services into enterprise workflows and automating software procurement processes.

| **#** | **Topic** | **Category** | **Publication Date** | **Facebook Proof** |
|---|---|---|---|---|
| Blog 1 | **Understanding AWS Marketplace APIs: Embedding Software Procurement into Internal Workflows** | AWS Marketplace & Serverless Architecture | 09/09/2026 | [Nguyen Thau](https://www.facebook.com/profile.php?id=61592819087978) |
| Blog 2 | **Continuing the AWS Marketplace Topic: When Contract Renewal Is Also Automated** | AWS Marketplace & Procurement Automation | 11/09/2026 | [Nguyen Thau](https://www.facebook.com/profile.php?id=61592819087978) |

---

### [3.1 Blog 1 – Understanding AWS Marketplace APIs: Embedding Software Procurement into Internal Workflows](3.1-Blog-1/)

AWS Marketplace provides many benefits: consolidated billing with AWS, pre-negotiated terms, a wide range of providers, and easier compliance management. However, many customers do not want to keep opening the AWS Console every time they need to find a product or manage a subscription. They want these operations embedded directly into the tools they already use, such as a Slack chatbot, ServiceNow integration for IT request approvals, or an internal procurement reporting dashboard.

AWS introduces a sample solution based on two main APIs:

- **Discovery API**: search, filter, and compare products in the catalog.
- **Agreement API**: manage subscriptions programmatically.

The solution provides three main functions:

- **Agreement management** — view, filter, and check details of existing subscriptions.
- **Product search and subscription** — compare plans and subscribe directly through the API.
- **Reporting** — automatically generate spending reports, expiration alerts, audit compliance information, and optionally enable AI-powered analysis through Strands Agents running on Claude through Amazon Bedrock.

The solution uses a serverless architecture including **CloudFront + S3** for the frontend, **API Gateway + Lambda** for application logic, **DynamoDB** for caching data, **Cognito** for JWT authentication, and **EventBridge** for scheduled synchronization.

The product subscription process can be implemented through five main API steps:

**ListPurchaseOptions → GetOffer → GetOfferTerms → CreateAgreementRequest → AcceptAgreementRequest**

This approach transforms operations that traditionally require AWS Console access into a self-service workflow embedded directly into internal enterprise systems.

---

### [3.2 Blog 2 – Continuing the AWS Marketplace Topic: When Contract Renewal Is Also Automated](3.2-Blog-2/)

Most contract renewals are not really new decisions. The buyer is still using the service successfully and wants to continue, while the seller also wants to retain the customer. However, the renewal date can still pass simply because of administrative procedures such as creating the offer again, waiting for approval again, and signing again.

**Private Offer Auto-Renewals** provides a way to automate this process. The seller and buyer can agree on the original terms and future renewal terms once when the offer is created. After that, each cycle can renew automatically without requiring another manual acceptance.

The solution provides three pricing methods for renewal:

- **Flat renewal** — keeps exactly the same price as the original across renewal cycles.
- **Fixed percentage uplift** — increases the price by a fixed percentage for each renewal cycle, with compounding.
- **Percentage range uplift** — defines a minimum and maximum percentage increase, with the exact percentage finalized closer to the renewal date.

Both parties receive notifications at important milestones, including upcoming renewal dates, price adjustment deadlines, opt-out deadlines, and completed renewals. Renewal events can also be integrated with **Amazon EventBridge**, allowing connection with CRM, billing, and internal alerting systems.

This approach helps reduce manual work, prevent service interruptions, provide predictable renewal pricing, and make contract management more efficient.

---

## Summary

The two blog topics cover two important aspects of AWS Marketplace:

1. **AWS Marketplace APIs** — embedding software procurement into internal workflows through APIs and serverless architecture.
2. **Private Offer Auto-Renewals** — automating the renewal of existing software contracts.

Together, these topics demonstrate how AWS Marketplace can support both **new software procurement** and **ongoing contract management**, while reducing manual operational work.

The Facebook account used to publish the posts can be verified through:

[**Nguyen Thau – Facebook**](https://www.facebook.com/profile.php?id=61592819087978)