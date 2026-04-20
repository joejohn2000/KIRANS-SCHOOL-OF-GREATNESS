# APRIL 20 ASSESSMENT | SYSTEM DESIGN PROBLEM SOLVING
**Date:** April 20, 2026
**Focus:** System design problem solving - architecture, trade-offs, concrete technology choices, caching, reliability, observability, and scaling
**Total Marks:** 60
**Time Allowed:** 60 minutes

---

> "Do not answer with keywords. Design the system, name the trade-off, and justify the choice."

---

## Instructions

1. This is **not** an MCQ paper. Write structured answers.
2. For every design question, include a small **text diagram** unless the question says otherwise.
3. Name concrete technologies where asked. Vague answers like "use a cache" or "add servers" score low.
4. If you choose a trade-off, say what you are gaining and what you are sacrificing.
5. If you are unsure, write the best partial design. No blanks.
6. Recommended time: about 15 minutes per question.

---

## Q1. Distributed Rate Limiter For 100 API Servers (15 marks)

You are designing a public API. It runs behind a load balancer and has **100 stateless API servers**.

Requirement:
- Each user can make at most **100 requests per minute**.
- The limit must work even when the same user sends requests to different API servers.
- The system should be fast enough to check the limit on every request.

Answer the following:

**Part A - Requirements (3 marks)**

Write:
1. Two functional requirements.
2. Two non-functional requirements.

**Part B - Algorithm and data store (4 marks)**

Choose the rate-limiting algorithm and the shared data store.

Your answer must include:
- Algorithm name.
- Data store name.
- Key format for storing per-user state.
- One reason this works across 100 API servers.

**Part C - Request flow diagram (4 marks)**

Draw a text diagram showing the request path from client to decision.

Include:
- Load balancer or API gateway.
- API server.
- Shared rate-limit store.
- Allow or reject decision.

**Part D - Failure and observability (4 marks)**

Answer:
1. If the shared store goes down, should the API fail open or fail closed? Why?
2. Name three metrics or logs you would track to know whether the limiter is healthy.

---

## Q2. Product Catalogue Stale Data Incident (15 marks)

An e-commerce product catalogue gets:
- 20,000 product reads per second.
- Product description updates a few times per day.
- Price updates a few times per hour.
- Inventory updates many times per minute during sales.

Last week, users saw an old price for 12 minutes after a price update.

Design the read and update flow.

**Part A - Cache strategy (4 marks)**

Choose a caching strategy for:
1. Product description.
2. Product price.
3. Inventory count.

For each one, say whether you would cache it, what TTL or invalidation strategy you would use, and why.

**Part B - Read path diagram (4 marks)**

Draw a text diagram for reading a product page.

Include:
- API service.
- Cache.
- Database or read replica.
- What happens on cache hit and cache miss.

**Part C - Update path (4 marks)**

A price update is made by an admin.

Explain:
1. Where the source of truth lives.
2. What happens to the cache after the update.
3. How you prevent users from seeing the old price for 12 minutes again.
4. Whether read replicas help or hurt this specific stale-price problem.

**Part D - Detection (3 marks)**

Name three metrics, logs, or alerts that would help catch stale product data quickly.

---

## Q3. Reliable Notification System (15 marks)

Design a notification system for an order platform.

Requirements:
- When an order is placed, send Email, SMS, and Push notifications.
- If a provider fails, retry the notification.
- Do not send the same notification twice to the user.
- Later, the company may add WhatsApp notifications.

Answer the following:

**Part A - Architecture diagram (4 marks)**

Draw a text diagram from `Order Service` to the notification providers.

Include:
- Event or job creation.
- Queue or stream.
- Notification workers.
- Provider APIs.

**Part B - Queue or stream choice (4 marks)**

Choose **RabbitMQ**, **Kafka**, or a combination.

Explain:
1. Why you chose it.
2. What delivery guarantee you expect.
3. Whether messages can be replayed.
4. Where ordering matters, if at all.

**Part C - Failure handling (4 marks)**

Explain how you handle:
1. Retry with backoff.
2. Dead-letter queue.
3. Duplicate messages.
4. Provider timeout.

**Part D - Adding WhatsApp later (3 marks)**

Explain how the design should change when WhatsApp is added.

Your answer should mention:
- Where the new channel code lives.
- What should not change in the core dispatch flow.
- One configuration or data-model change needed.

---

## Q4. Social Feed With Normal Users And Celebrities (15 marks)

You are designing a social feed.

Facts:
- Normal users usually have fewer than 500 followers.
- Celebrity users may have 5 million followers.
- Users expect the home feed to load quickly.
- New posts should appear reasonably soon, but exact real-time delivery is not required.

Answer the following:

**Part A - Requirements and APIs (3 marks)**

Write:
1. Two functional requirements.
2. Two non-functional requirements.
3. Two API endpoints.

**Part B - Feed generation strategy (4 marks)**

Choose the strategy for:
1. Normal users.
2. Celebrity users.

Use terms like fan-out-on-write, fan-out-on-read, or hybrid. Explain why.

**Part C - Storage, cache, and pagination (5 marks)**

Explain:
1. What data you store for posts.
2. What data you store for each user's feed.
3. How you shard or partition the data.
4. What you cache.
5. How cursor pagination works for the feed.

**Part D - Bottleneck and monitoring (3 marks)**

Name:
1. The first bottleneck you expect at scale.
2. One mitigation for that bottleneck.
3. Two metrics you would monitor.

---

## Scoring Guide

| Score | Interpretation |
|---|---|
| 50-60 | Strong applied system design. Ready to move forward with light carry-over only. |
| 42-49 | Good, but still needs targeted carry-over on missed trade-offs. |
| 30-41 | Partial transfer. Review weak concepts before the next full design problem. |
| Below 30 | Needs focused remediation before advancing. |

---

*End of paper.*
