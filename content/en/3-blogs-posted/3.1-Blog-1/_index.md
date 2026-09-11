---
title: "blog-1"
weight: 1
---

# UNDERSTANDING AWS MARKETPLACE APIs: EMBEDDING SOFTWARE PROCUREMENT INTO INTERNAL WORKFLOWS

🔹 **The problem**

AWS Marketplace provides many benefits: consolidated billing with AWS, pre-negotiated terms, a wide range of providers, and easier compliance management. However, many customers do not want to keep opening the AWS Console every time they need to find a product or manage a subscription. They want these operations embedded directly into the tools they already use, such as a Slack chatbot, ServiceNow integration for IT request approvals, or an internal procurement reporting dashboard.

🔹 **Solution: MP-Buyer Portal**

AWS introduces a sample solution based on two main APIs:

- Discovery API: search, filter, and compare products in the catalog.
- Agreement API: manage subscriptions programmatically.

Three main functions:

1️⃣ Agreement management — view, filter, and check details of existing subscriptions.

2️⃣ Product search & subscription — compare plans and subscribe directly through the API.

3️⃣ Reporting — automatically generate spending reports, expiration alerts, audit compliance information, and optionally enable AI-powered analysis through Strands Agents (running on Claude through Amazon Bedrock).

🔹 **Solution architecture**

What I like most is the fully serverless architecture, with almost no cost when the system is idle: CloudFront + S3 serves the frontend, API Gateway + Lambda handles the logic (agreement/search/subscription, AI reporting, and data synchronization), DynamoDB caches data, Cognito authenticates users through JWT, and EventBridge triggers synchronization every 6 hours.

![MP-Buyer Portal Architecture](/QuangThienWorkshop-template/images/mp-buyer-architecture6-3v2fig1.drawio-1024x714.png)

🔹 **Product subscription flow (5 API steps)**

ListPurchaseOptions → GetOffer → GetOfferTerms → CreateAgreementRequest → AcceptAgreementRequest.

In essence, it works the same way as AWS Console, except that everything runs through APIs on a self-built interface — allowing even users without direct Console access to use the workflow.

🔹 **Personal impression**

This is a practical example of transforming an operation that traditionally "requires access to the Console" into a self-service workflow for the procurement team, while preserving the core benefits of AWS Marketplace. The integration of AI to automatically generate summarized reports is also an interesting direction for applying AI to daily operations, rather than limiting AI usage to chatbots.

📌 **Source:** Kenneth Walsh, "How you can embed procurement into your workflows with AWS Marketplace APIs", AWS Marketplace Blog, 04/09/2026.

🔗 [https://aws.amazon.com/blogs/awsmarketplace/how-you-can-embed-procurement-into-your-workflows-with-aws-marketplace-apis/](https://aws.amazon.com/blogs/awsmarketplace/how-you-can-embed-procurement-into-your-workflows-with-aws-marketplace-apis/)

**#AWS** **#AWSMarketplace** **#CloudComputing** **#Internship** **#Serverless**