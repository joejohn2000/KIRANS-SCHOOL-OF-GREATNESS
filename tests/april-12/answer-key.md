# APRIL 12 ASSESSMENT | ANSWER KEY
**Date:** April 12, 2026
**Paper:** System Design MCQ Marathon
**Total Questions:** 120
**Total Marks:** 120

---

## Section A Answer Key (Q1-Q20)

| Q | Answer | Why |
|---|---|---|
| 1 | B | Scalability is about handling more load without unacceptable degradation. |
| 2 | B | Latency is the time taken for one request/response cycle. |
| 3 | B | Horizontal scaling means adding more machines. |
| 4 | C | A load balancer spreads traffic across multiple servers. |
| 5 | B | Consistent hashing minimizes remapping when nodes change. |
| 6 | A | Cache-aside is a standard pattern for read-heavy systems. |
| 7 | C | On a miss, the app reads DB, populates cache, and returns data. |
| 8 | D | Exact financial balances are sensitive to stale cached data. |
| 9 | B | AP prioritizes availability during partitions, even with stale reads. |
| 10 | C | CP may reject requests rather than risk inconsistent data. |
| 11 | B | Strong multi-row transaction correctness strongly favors SQL. |
| 12 | A | Flexible nested JSON is a common document DB fit. |
| 13 | C | Sharding splits data across nodes for scale. |
| 14 | A | Read replicas increase read capacity. |
| 15 | C | Replication lag can make reads stale. |
| 16 | B | CDNs serve static content closer to users. |
| 17 | A | Idempotent operations reach the same final state when repeated. |
| 18 | D | Idempotency keys help prevent duplicate payment effects on retries. |
| 19 | B | Queue messages are typically consumed once; pub/sub fans out. |
| 20 | C | Kafka is designed for ordered, replayable event streams. |

## Section B Answer Key (Q21-Q40)

| Q | Answer | Why |
|---|---|---|
| 21 | C | Least connections helps when request durations vary. |
| 22 | A | Sticky sessions are usually needed because state lives on app servers. |
| 23 | D | Shared session storage or stateless auth removes affinity dependence. |
| 24 | B | Read replicas directly offload read pressure from the primary. |
| 25 | C | A unique ID plus Base62 encoding is a common shortener pattern. |
| 26 | A | A hot key overloads part of the cache/request path. |
| 27 | B | Queue backlog is a better signal for worker demand than CPU alone. |
| 28 | D | Virtual nodes improve key distribution balance. |
| 29 | B | API gateways commonly handle auth, routing, and rate limiting. |
| 30 | A | Canary rollout exposes the new version to limited traffic first. |
| 31 | C | Blue-green allows fast traffic switchback for rollback. |
| 32 | D | Token bucket permits bursts up to bucket capacity. |
| 33 | B | Fixed windows allow boundary bursts across adjacent windows. |
| 34 | C | A shared store is required for cross-server limit coordination. |
| 35 | A | Redis supports fast counters and atomic operations in memory. |
| 36 | B | Geo-routing sends traffic to the nearest healthy region. |
| 37 | C | Round robin ignores uneven numbers of long-lived active connections. |
| 38 | C | Low-cardinality shard keys create skew and imbalance. |
| 39 | B | Unevenly hot shards are a hotspotting problem. |
| 40 | D | First identify the real bottleneck with observability data. |

## Section C Answer Key (Q41-Q60)

| Q | Answer | Why |
|---|---|---|
| 41 | C | Relational databases are strongest for ACID, joins, and constraints. |
| 42 | A | Flexible nested documents match document stores well. |
| 43 | B | Sessions and cache lookups map naturally to key-value stores. |
| 44 | C | Wide-column stores are common for high-volume time-series/wide-row patterns. |
| 45 | D | Indexes speed reads but add storage and write overhead. |
| 46 | A | Denormalization reduces join cost on read-heavy paths. |
| 47 | C | Duplicated data creates consistency/update complexity. |
| 48 | B | Write-through updates both cache and backing store in the write path. |
| 49 | A | Write-behind lowers foreground write latency by delaying DB persistence. |
| 50 | D | Data may be lost if the cache dies before flush completes. |
| 51 | C | Updated source data can leave stale cached copies behind. |
| 52 | B | TTL caching works when bounded staleness is acceptable. |
| 53 | A | The primary still usually handles writes. |
| 54 | B | Multi-leader is useful when multiple regions need local writes. |
| 55 | C | Concurrent updates from different leaders create conflicts. |
| 56 | D | `R + W > N` is the common quorum overlap condition. |
| 57 | A | User-scoped access patterns pair well with user-based partitioning. |
| 58 | C | Geographic shards can become very uneven in load/data volume. |
| 59 | B | Materialized views precompute expensive query results for faster reads. |
| 60 | D | Analytics warehouses are designed for large analytical scans. |

## Section D Answer Key (Q61-Q80)

| Q | Answer | Why |
|---|---|---|
| 61 | C | Queues decouple user requests from slower background work. |
| 62 | B | At-least-once means duplicates are possible. |
| 63 | A | Idempotency prevents duplicate deliveries from duplicating effects. |
| 64 | D | Dead-letter queues hold messages that repeatedly fail processing. |
| 65 | C | Events let multiple services react independently to the same change. |
| 66 | B | Kafka guarantees ordering per partition, not globally across all partitions. |
| 67 | D | RabbitMQ is a classic fit for ack-based task queues. |
| 68 | A | Backoff reduces pressure on a failing downstream dependency. |
| 69 | C | Circuit breakers temporarily stop calls to failing dependencies. |
| 70 | B | Bulkheads isolate failure domains/resources. |
| 71 | D | Health checks should reflect real readiness to serve traffic. |
| 72 | A | Heartbeats help detect dead or stuck workers. |
| 73 | C | Retries, crashes, and ack ambiguity make true exactly-once hard. |
| 74 | B | Saga coordinates distributed steps without one global transaction. |
| 75 | D | A compensating action reverses or offsets earlier work. |
| 76 | A | Some coordination roles must have only one active owner. |
| 77 | C | Split-brain means multiple nodes think they are leader. |
| 78 | B | Majority agreement reduces conflicting leadership decisions. |
| 79 | D | TTL/leases prevent permanent lock ownership after crashes. |
| 80 | A | Unsynchronized clocks make ordering and expiry tricky. |

## Section E Answer Key (Q81-Q100)

| Q | Answer | Why |
|---|---|---|
| 81 | B | REST statelessness means each request is self-contained. |
| 82 | D | GET is expected to be safe and idempotent. |
| 83 | C | Cursor pagination scales better for large, changing feeds. |
| 84 | B | Versioning lets APIs evolve without instantly breaking clients. |
| 85 | A | Signed URLs let clients access object storage directly for a limited time. |
| 86 | C | TLS secures data while it travels over the network. |
| 87 | D | Authorization determines what an authenticated user may do. |
| 88 | B | Rate limiting protects service capacity and fairness. |
| 89 | A | p99 means 99% of requests are at or below that latency. |
| 90 | C | Good averages can hide poor tail latency. |
| 91 | D | Distributed traces follow one request across services. |
| 92 | B | Queue depth is the clearest backlog signal. |
| 93 | C | Correlation/trace IDs tie events from one request together. |
| 94 | A | Error budget is the allowed failure room under the SLO. |
| 95 | D | User-facing SLO breach alerts map most directly to impact. |
| 96 | A | Synthetic monitoring uses automated probes to simulate user checks. |
| 97 | B | Compression reduces response transfer size. |
| 98 | C | Batching reduces repeated per-operation overhead. |
| 99 | D | N+1 is one initial fetch plus many follow-up item fetches. |
| 100 | A | Connection pools reuse existing DB connections efficiently. |

## Section F Answer Key (Q101-Q120)

| Q | Answer | Why |
|---|---|---|
| 101 | B | Hot URL mappings in Redis reduce redirect lookup latency. |
| 102 | B | A social feed usually favors availability over perfect consistency. |
| 103 | C | Payment ledgers usually prioritize consistency during partitions. |
| 104 | A | Read-heavy, rarely changing data is ideal for cache-aside with TTL. |
| 105 | D | Rapidly changing scores need very fresh delivery or push updates. |
| 106 | C | Object storage plus CDN is the standard global image-serving path. |
| 107 | B | A nearby read replica reduces cross-region read latency. |
| 108 | A | Saga fits multi-service workflows without one global transaction. |
| 109 | D | Scheduler coordination needs a lease/lock with expiry and health signals. |
| 110 | B | Redis is the practical shared store for distributed rate limiting. |
| 111 | C | Kafka supports ordered replayable logs for audit/reprocessing. |
| 112 | D | Autocomplete and relevance ranking are search-engine workloads. |
| 113 | A | Time-range metrics fit time-series optimized storage. |
| 114 | C | Inventory must be reserved in a strongly consistent source before confirmation. |
| 115 | B | Celebrity traffic concentrating on one shard is hotspotting. |
| 116 | D | Extracting one bounded service reduces migration risk. |
| 117 | A | Celebrity fan-out often needs fan-out-on-read or a hybrid design. |
| 118 | B | CDN invalidation/purge removes stale cached objects. |
| 119 | C | Heavy analytical scans can degrade transactional workload performance. |
| 120 | D | Requirements and constraints should drive technology choices. |

---

## Quick Score Guide

- **100-120:** Strong system design understanding for this learning stage
- **80-99:** Good grasp with a few trade-off gaps
- **60-79:** Partial understanding; needs revision on weak sections
- **Below 60:** Needs another focused review before moving ahead

---

*Teacher note: This paper is intentionally broad and medium-hard. It checks vocabulary, trade-offs, and scenario reasoning rather than deep distributed-systems theory.*
