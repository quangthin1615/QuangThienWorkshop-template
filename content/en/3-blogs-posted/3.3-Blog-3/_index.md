---
title: "Building an Event-Driven Architecture with Amazon SQS and AWS Lambda"
weight: 3
---

## 1. Overview

Modern applications do not always need direct synchronous communication. A producer can place a message in Amazon SQS and a consumer can process it asynchronously.

When combined with AWS Lambda, SQS enables event-driven processing without managing servers.

![Application - SQS - Lambda](/images/blog3-01-application-sqs-lambda.png)

Basic flow:

**Application/Producer → Amazon SQS → Lambda Event Source Mapping → AWS Lambda**

## 2. The role of SQS

SQS acts as a buffer between producers and consumers. When traffic suddenly increases, messages can queue instead of forcing the consumer to process everything immediately.

Benefits:
- reduced coupling;
- burst absorption;
- asynchronous processing;
- retry support;
- independent consumer scaling.

![SQS Queue](/images/blog3-02-sqs-queue.png)

## 3. Lambda message processing

Lambda can use Event Source Mapping to consume messages from SQS. Lambda polls the queue and invokes the function to process batches.

Developers can focus on business logic instead of implementing polling infrastructure.

![Lambda processing](/images/blog3-03-lambda-processing.png)

## 4. Scaling and concurrency

As message volume increases, Lambda can increase executions to process the queue faster. However, aggressive scaling can put pressure on downstream databases or APIs.

AWS provides maximum concurrency controls for Lambda when SQS is the event source, helping control processing rate and protect downstream services.

## 5. Retry and DLQ

Messages can fail because of application errors or dependency failures. After the configured retry behavior, a message can be moved to a Dead-Letter Queue.

DLQs help isolate failed messages, prevent endless retries, and support troubleshooting or controlled reprocessing.

## 6. Practical example

An e-commerce system:

1. A customer places an order.
2. The application creates a message.
3. The message is sent to SQS.
4. Lambda receives the message.
5. Lambda validates and processes the order.
6. A failed message is retried.
7. Repeated failures send the message to the DLQ.

## 7. Key takeaway

SQS provides buffering and decoupling, while Lambda provides serverless processing and scaling. Production designs should consider idempotency, batch size, concurrency, downstream capacity, and DLQ requirements.

## 8. References

1. [AWS – Maximum concurrency với Lambda và SQS](https://aws.amazon.com/blogs/compute/introducing-maximum-concurrency-of-aws-lambda-functions-when-using-amazon-sqs-as-an-event-source/)

2. [AWS – Faster polling scale-up cho Lambda và SQS](https://aws.amazon.com/blogs/compute/introducing-faster-polling-scale-up-for-aws-lambda-functions-configured-with-amazon-sqs/)

3. [AWS – Designing event-driven architectures](https://aws.amazon.com/blogs/architecture/lets-architect-designing-event-driven-architectures/)