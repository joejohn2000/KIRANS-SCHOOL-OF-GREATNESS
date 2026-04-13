# APRIL 12 ASSESSMENT | EVALUATION
**Date:** April 13, 2026
**Test folder:** `tests/april-12`
**Focus:** System design MCQ marathon - fundamentals, scaling, caching, storage, messaging, reliability, APIs, observability, and applied scenarios
**Total Score:** 94 / 120 (78.3%)
**Result:** Advance with targeted carry-over

---

## Score Breakdown

| Section | Focus | Marks |
|---|---|---:|
| Section A | Fundamentals & trade-offs | 16 / 20 |
| Section B | Scalability, load balancing & traffic handling | 17 / 20 |
| Section C | Storage, caching & data management | 15 / 20 |
| Section D | Messaging, reliability & distributed systems | 15 / 20 |
| Section E | APIs, security, observability & performance | 16 / 20 |
| Section F | Applied system design scenarios | 15 / 20 |
| **Total** |  | **94 / 120** |

---

## Question-Level Misses

| Q | Candidate | Correct | Comment |
|---|---|---|---|
| 6 | C | A | Chose blue-green deployment instead of cache-aside for a read-heavy catalogue. Deployment vocabulary got mixed with caching vocabulary. |
| 14 | C | A | Read replicas help read traffic; they do not eliminate replication lag. |
| 15 | A | C | The main read-replica drawback is stale reads from replication lag, not lack of SQL support. |
| 20 | A | C | Redis is a cache/key-value store; Kafka is the better fit for replayable ordered event streams. |
| 29 | D | B | API gateways commonly handle auth, routing, and rate limiting, not frontend compilation. |
| 32 | B | D | Token bucket, not fixed window, naturally allows bursts up to configured capacity. |
| 37 | D | C | WebSocket load balancing is about long-lived active connections, not strong consistency. |
| 43 | D | B | Session tokens and simple cache lookups fit key-value stores, not object storage. |
| 49 | B | A | Write-behind improves foreground write latency; it does not provide perfect durability if the cache crashes before flush. |
| 52 | C | B | TTL caching is best when bounded staleness is acceptable, not when every read must be newest. |
| 57 | C | A | Partitioning by `userId` helps when requests are scoped to a user. User IDs changing every second would be a bad fit. |
| 59 | A | B | Materialized views intentionally store derived/precomputed query results for faster reads. |
| 66 | A | B | Kafka ordering is guaranteed within a partition, not globally across all topics and regions. |
| 67 | C | D | RabbitMQ, not Elasticsearch, is the better fit for a classic ack-based work queue. |
| 68 | C | A | Exponential backoff reduces retry storms; it does not guarantee strong consistency. |
| 72 | C | A | Heartbeats detect failed or stalled workers; they do not replace job queues. |
| 75 | C | D | A compensating transaction undoes or offsets a prior local saga step; it is not leader election. |
| 83 | D | C | Cursor pagination is usually safer than offset pagination for large, frequently changing feeds. |
| 84 | A | B | API versioning exists to evolve behavior without breaking existing clients immediately. |
| 93 | A | C | For a failed order across services, trace ID or correlation ID is the useful lookup key. |
| 98 | B | C | Batching improves throughput by reducing round-trip overhead; it does not guarantee zero failures. |
| 103 | D | C | A payment ledger should prefer consistency during partitions, so CP is the closer trade-off. |
| 110 | A | B | A distributed rate limiter across 100 API servers needs a shared store such as Redis, not isolated local arrays. |
| 111 | D | C | Ordered event replay for audit/reprocessing is a Kafka-style workload, not local filesystem logs on one server. |
| 117 | D | A | Celebrity fan-out usually needs fan-out-on-read or a hybrid approach. The submitted answer appears copied from Q116. |
| 119 | D text, no letter | C | The answer text matched option D, "OLTP systems cannot have indexes." Correct answer is C: analytics scans can hurt transactional workloads. |

---

## Strengths Demonstrated

- Strong baseline system design vocabulary: scalability, latency, horizontal scaling, load balancers, consistent hashing, AP/CP trade-offs, SQL vs NoSQL, sharding, CDN, idempotency, and pub/sub basics were mostly correct.
- Load balancing and traffic-handling were the strongest section at 17/20.
- The candidate handled many applied scenarios correctly: URL shortener cache, social feed AP trade-off, product catalogue cache-aside, image storage plus CDN, regional read replicas, saga for order flow, distributed scheduler lease, search backend, time-series storage, inventory consistency, hot shards, monolith extraction, CDN invalidation, and requirement clarification.
- Compared with earlier evidence, system design remains a relative strength. This result is substantially stronger than the April 3 mixed test's system design subsection and far stronger than the implementation-heavy pattern results.

## Areas For Growth

- Concrete technology matching still needs repetition: Kafka vs RabbitMQ vs Redis vs Elasticsearch got mixed up in several places.
- Cache and replication nuance needs tightening: the candidate selected several impossible absolutes such as "eliminating all replication lag," "perfect durability if cache crashes," and "every read must be newest" for TTL caching.
- Distributed reliability concepts are partially understood but not stable: partition-level Kafka ordering, exponential backoff, heartbeats, and saga compensation were missed.
- Operational/API questions need a short review: API gateway responsibilities, API versioning, cursor pagination, correlation IDs, and batching.
- A small attention-to-detail pattern appeared near the end: Q117 appears copied from Q116, and Q119 omitted the option letter and selected the wrong option text.

---

## Recommendation

**Advance with targeted carry-over.**

Do not repeat the full 120-question paper. The result is good enough to move forward, but not clean enough to treat system design as fully consolidated. Use a focused 30-40 minute review on:

1. Kafka vs RabbitMQ vs Redis vs Elasticsearch.
2. Cache-aside, TTL, write-behind, read replicas, and replication lag.
3. Retry/backoff, heartbeats, saga compensation, and distributed rate limiting.
4. Cursor pagination, trace/correlation IDs, API gateway duties, and API versioning.

After the review, use a short 20-question mixed retest rather than another full paper.
