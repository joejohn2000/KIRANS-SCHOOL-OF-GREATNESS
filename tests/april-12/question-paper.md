# APRIL 12 ASSESSMENT | SYSTEM DESIGN MCQ MARATHON
**Date:** April 12, 2026
**Focus:** System design only - fundamentals, trade-offs, scaling, caching, storage, messaging, reliability, APIs, observability, and applied scenarios
**Total Marks:** 120
**Time Allowed:** 120 minutes

---

> "Choose the best answer, not just a familiar keyword."

---

## Instructions

1. This paper contains **120 multiple-choice questions** worth **1 mark each**.
2. There is **one best answer** for every question.
3. No negative marking.
4. Read scenario questions carefully. Some options are partially correct, but only one is the best system-design choice.
5. This is a **medium-hard** paper: expect concept recall, trade-off reasoning, and applied decision-making.

---

## SECTION A: SYSTEM DESIGN FUNDAMENTALS & TRADE-OFFS (Q1-Q20)

**1.** In system design, **scalability** mainly means:

A. Reducing code length  
B. Handling more load without unacceptable performance loss  
C. Using more programming languages  
D. Avoiding databases

**2.** Which statement best describes **low latency**?

A. The system handles many requests per second  
B. Each request gets a response quickly  
C. The database stores more rows  
D. The cache hit ratio is always 100%

**3.** **Horizontal scaling** means:

A. Adding more CPU and RAM to one machine  
B. Adding more machines to share the load  
C. Removing all bottlenecks  
D. Converting SQL to NoSQL

**4.** The primary job of a **load balancer** is to:

A. Compress images  
B. Encrypt every database record  
C. Distribute incoming traffic across multiple servers  
D. Replace the application server

**5.** **Consistent hashing** is especially useful when:

A. You need strong consistency across all regions  
B. Servers are added or removed and you want minimal key remapping  
C. You want to replace SQL joins  
D. You need faster TLS handshakes

**6.** A read-heavy product catalogue is a classic use case for:

A. Cache-aside  
B. Dead-letter queue  
C. Blue-green deployment  
D. Two-phase commit

**7.** In the **cache-aside** pattern, what happens on a cache miss?

A. The request is rejected immediately  
B. The app writes an empty value into the cache and stops  
C. The app fetches from the database, stores the result in cache, then returns it  
D. The database fetches from the cache

**8.** Which kind of data is **least suitable** for aggressive caching if correctness must be exact?

A. Product thumbnails  
B. Blog home page HTML  
C. Public FAQs  
D. Current bank account balance

**9.** In an **AP** system during a network partition, the system usually prioritizes:

A. Returning only the newest data  
B. Staying available even if some responses may be stale  
C. Rejecting all requests  
D. Global transactions

**10.** In a **CP** system during a network partition, the system may:

A. Always respond successfully with cached data  
B. Ignore the partition completely  
C. Refuse some requests to preserve consistency  
D. Convert itself into a CDN

**11.** Which situation most strongly favors a **SQL** database over a NoSQL store?

A. Flexible user profile fields that vary a lot  
B. Multi-row financial transactions with strong consistency  
C. Session cache with simple key-value lookups  
D. Event log replay

**12.** Which situation is a strong fit for a **document database**?

A. User profiles with nested, flexible JSON fields  
B. Strict double-entry bookkeeping  
C. Heavy relational joins across many normalized tables  
D. DNS resolution

**13.** **Database sharding** is mainly used to:

A. Improve image compression  
B. Eliminate the need for indexes  
C. Split data across multiple database nodes for scale  
D. Replace backups

**14.** A **read replica** primarily helps by:

A. Serving more read traffic from copies of the primary data  
B. Making writes strongly consistent across all regions automatically  
C. Eliminating all replication lag  
D. Replacing application logs

**15.** A common drawback of using read replicas is:

A. No support for SQL  
B. Infinite storage growth  
C. Replication lag can return stale reads  
D. They cannot serve any traffic

**16.** A **CDN** is best suited for:

A. Coordinating distributed transactions  
B. Serving static content closer to end users  
C. Replacing the primary database  
D. Running cron jobs

**17.** An **idempotent** operation is one that:

A. Produces the same final result even if repeated multiple times  
B. Always completes in O(1) time  
C. Never writes to a database  
D. Requires a queue

**18.** Which feature most helps prevent duplicate charges when a client retries `POST /payments`?

A. Offset pagination  
B. WebSockets  
C. Read replicas  
D. Idempotency keys

**19.** What is the key difference between a **message queue** and **pub/sub**?

A. Queues use JSON and pub/sub does not  
B. Queue messages are typically consumed once, while pub/sub can fan out to multiple consumers  
C. Pub/sub cannot be distributed  
D. Queues cannot retry failed work

**20.** Which technology is the better fit for a replayable, ordered event stream?

A. Redis cache  
B. PostgreSQL read replica  
C. Kafka  
D. CDN

---

## SECTION B: SCALABILITY, LOAD BALANCING & TRAFFIC HANDLING (Q21-Q40)

**21.** Which load-balancing algorithm is most useful when requests have very different durations?

A. Random  
B. Round robin only  
C. Least connections  
D. DNS failover only

**22.** A team asks for **sticky sessions** at the load balancer. The most likely reason is:

A. Session state is stored in app server memory  
B. They want stronger database consistency  
C. They want smaller images  
D. They need better SQL joins

**23.** Which change is often better than relying on sticky sessions?

A. Removing the load balancer  
B. Keeping all user data only in browser memory  
C. Turning off HTTPS  
D. Moving session state to a shared store or using stateless tokens

**24.** A product service is mostly read-heavy and the primary database is overloaded. What is the most direct first improvement?

A. Replace all APIs with GraphQL  
B. Add read replicas  
C. Use a slower serializer  
D. Delete indexes

**25.** For a URL shortener, a common way to generate short codes at scale is to:

A. Hash the password of the user  
B. Use image metadata  
C. Generate a unique numeric ID and encode it in Base62  
D. Store the full URL as the short code

**26.** A **hot key** problem in caching means:

A. One key receives disproportionately high traffic and overloads part of the system  
B. Every key has identical traffic  
C. The cache is always empty  
D. Encryption is disabled

**27.** Which metric is often better than CPU alone for auto-scaling queue workers?

A. CSS bundle size  
B. Queue depth or backlog  
C. Number of comments in code  
D. Screen resolution

**28.** Virtual nodes are used with consistent hashing mainly to:

A. Remove the need for a hash function  
B. Guarantee strict serializability  
C. Eliminate all hotspots  
D. Distribute keys more evenly across nodes

**29.** Which responsibility commonly belongs to an **API gateway**?

A. Running database migrations  
B. Authentication, routing, and rate limiting at the edge  
C. Replacing all internal services  
D. Compiling frontend code

**30.** The main goal of a **canary deployment** is to:

A. Test the new version on a small percentage of traffic before full rollout  
B. Disable logging in production  
C. Avoid versioning APIs forever  
D. Replace monitoring with manual testing

**31.** A major benefit of **blue-green deployment** is:

A. Lower memory use in the database  
B. No need for testing  
C. Fast rollback by switching traffic back to the old environment  
D. Guaranteed zero bugs

**32.** Which rate-limiting algorithm naturally allows short bursts up to a configured capacity?

A. Round robin  
B. Fixed window counter  
C. Least connections  
D. Token bucket

**33.** What is the classic weakness of a **fixed-window** rate limiter?

A. It cannot count requests  
B. Clients can burst at the end of one window and the start of the next  
C. It requires a database schema  
D. It works only for GET requests

**34.** A distributed rate limiter shared across 100 API servers most commonly needs:

A. Local in-memory arrays on each server only  
B. Browser local storage  
C. A shared fast datastore such as Redis  
D. A CDN

**35.** Redis is popular for distributed rate limiting because it offers:

A. Fast in-memory operations and atomic counter updates  
B. Unlimited persistent storage for free  
C. Built-in full-text ranking better than any search engine  
D. Automatic conflict-free global transactions

**36.** Sending users to the nearest healthy region is most closely associated with:

A. Batch processing  
B. Geo-routing  
C. Vertical partitioning  
D. Cache warming

**37.** Why can plain round robin perform poorly for long-lived WebSocket connections?

A. It encrypts traffic twice  
B. It increases SQL lock contention  
C. It ignores that some servers may already hold many long-lived connections  
D. It forces strong consistency

**38.** Which is a poor shard key because it often has **low cardinality**?

A. User ID  
B. Order ID  
C. Country code or status field  
D. UUID

**39.** When one shard gets much more traffic than others, the problem is called:

A. Compression  
B. Hotspotting  
C. Serialization  
D. Pagination

**40.** A service suddenly shows high CPU and high latency after launch. What is the best first move?

A. Immediately rewrite the whole service  
B. Drop the database and start over  
C. Turn off all logs and metrics  
D. Use metrics and traces to find the hottest endpoint or dependency first

---

## SECTION C: STORAGE, CACHING & DATA MANAGEMENT (Q41-Q60)

**41.** Which database type is strongest when you need joins, constraints, and ACID transactions?

A. Document database  
B. Key-value store  
C. Relational database  
D. CDN

**42.** Which store is a natural fit for nested JSON documents whose fields may vary by user?

A. Document database  
B. Block storage  
C. Message queue  
D. CDN cache

**43.** Which store is most naturally suited for session tokens and simple cache lookups?

A. Graph database  
B. Key-value store  
C. Columnar analytics warehouse  
D. Object storage

**44.** Which kind of store is often used for very high-volume time-series or wide-row access patterns?

A. Spreadsheet  
B. Browser cache  
C. Wide-column store  
D. CDN only

**45.** Adding a secondary index usually trades:

A. Faster writes for slower reads  
B. Better compression for weaker consistency  
C. Fewer queries for more network hops  
D. Faster reads for extra write cost and storage

**46.** **Denormalization** is usually chosen to:

A. Reduce expensive joins on read-heavy paths  
B. Eliminate backups  
C. Guarantee serializable transactions  
D. Replace load balancers

**47.** A major downside of denormalization is:

A. SQL stops working  
B. Requests cannot be cached  
C. Duplicate data becomes harder to keep consistent  
D. APIs cannot paginate

**48.** In a **write-through cache**, the application:

A. Writes only to cache and never to the database  
B. Updates cache and database together during the write path  
C. Deletes the database before writing  
D. Uses only a CDN

**49.** One advantage of **write-behind** caching is:

A. Lower write latency because the database update can happen asynchronously  
B. Perfect durability even if the cache crashes  
C. No need for a database  
D. Automatic strong consistency across regions

**50.** The main risk of **write-behind** caching is:

A. Reads become impossible  
B. SSL certificates expire faster  
C. The cache cannot evict entries  
D. Data can be lost if the cache fails before flushing to the database

**51.** Why is **cache invalidation** considered hard?

A. Caches cannot store strings  
B. It always requires machine learning  
C. Stale data can survive after underlying data changes  
D. It works only on Linux

**52.** A simple **TTL-based cache** works best when:

A. Data changes constantly every millisecond  
B. Some staleness is acceptable and updates are relatively infrequent  
C. Every read must reflect the newest write instantly  
D. The dataset is too small to cache

**53.** Read replicas do not solve a write bottleneck because:

A. Writes still usually go through the primary  
B. Replicas can never store data  
C. Replicas delete indexes  
D. Replicas only serve static files

**54.** **Multi-leader replication** is most attractive when:

A. Only one region will ever write  
B. Multiple regions need local write capability  
C. The app has no users  
D. You want to remove conflict resolution entirely

**55.** A major challenge in multi-leader replication is:

A. Too few writes  
B. No network latency  
C. Conflict resolution between concurrent updates  
D. Lack of any storage engines

**56.** In a replicated database, which condition is commonly used to improve the chance of reading the latest write?

A. `R + W < N`  
B. `R = 0`  
C. `W = 0`  
D. `R + W > N`

**57.** Partitioning data by `userId` works especially well when:

A. Most requests are scoped to a single user  
B. Every request scans all users  
C. User IDs keep changing every second  
D. You need image compression

**58.** Sharding by country can be risky because:

A. Countries cannot be stored as strings  
B. SQL forbids geographic data  
C. Traffic and data may be uneven across regions, creating skew  
D. It always prevents indexing

**59.** A **materialized view** is useful when:

A. You want to avoid storing any derived data  
B. You need fast reads for precomputed query results such as dashboard aggregates  
C. You want to replace all application logic  
D. You need a message broker

**60.** For large-scale analytical queries over append-heavy event data, the best fit is often:

A. An image CDN  
B. Browser local storage  
C. A transactional OLTP primary only  
D. A columnar analytics warehouse

---

## SECTION D: MESSAGING, RELIABILITY & DISTRIBUTED SYSTEMS (Q61-Q80)

**61.** Putting an async queue between an API and an email worker mainly helps by:

A. Removing the need for retries  
B. Making the database relational  
C. Smoothing traffic spikes and decoupling request handling from background work  
D. Replacing authentication

**62.** **At-least-once delivery** means:

A. A message is guaranteed to be delivered exactly once  
B. A message may be delivered more than once, so consumers must handle duplicates  
C. A message is delivered at most once  
D. Delivery order is always perfect globally

**63.** Why are **idempotent consumers** important with at-least-once delivery?

A. They prevent duplicates from causing incorrect repeated side effects  
B. They make queues unnecessary  
C. They turn AP systems into CP systems  
D. They remove the need for persistence

**64.** A **dead-letter queue** stores:

A. Only successful responses  
B. Cache invalidation rules  
C. TLS certificates  
D. Messages that repeatedly fail processing

**65.** Event-driven architecture is especially useful when:

A. One service must be hard-coded into every other service  
B. There are no background workflows  
C. Multiple independent services need to react to the same event  
D. All logic must stay synchronous

**66.** Kafka ordering is easiest to guarantee:

A. Across all topics in all regions  
B. Within a single partition  
C. Across every consumer group globally  
D. Only if there is one user

**67.** Which tool is often the better fit for a classic work queue with acknowledgements and per-message routing?

A. CDN  
B. PostgreSQL replica  
C. Elasticsearch  
D. RabbitMQ

**68.** Why is **exponential backoff** used for retries?

A. It reduces retry storms against an already failing dependency  
B. It makes latency always zero  
C. It guarantees strong consistency  
D. It replaces logging

**69.** A **circuit breaker** pattern helps by:

A. Increasing image resolution  
B. Turning retries into database joins  
C. Stopping repeated calls to a failing dependency for a while  
D. Removing the network

**70.** A **bulkhead** pattern is designed to:

A. Duplicate every log line  
B. Isolate failures by separating resources so one failure does not sink everything  
C. Force all services onto one machine  
D. Replace health checks

**71.** A load balancer health check should ideally indicate:

A. Whether the process exists, even if it cannot serve traffic  
B. Whether the code has comments  
C. Whether the machine has a desktop wallpaper  
D. Whether the service is actually ready to handle real requests

**72.** In distributed worker systems, **heartbeats** are mainly used to:

A. Detect failed or stalled workers  
B. Compress payloads  
C. Replace job queues  
D. Improve CSS loading

**73.** Why is true **exactly-once** processing across distributed systems difficult?

A. Databases cannot count  
B. Networks are always fast  
C. Retries, crashes, and acknowledgements can create duplicates or ambiguity  
D. JSON has no schema

**74.** The **Saga** pattern is used to:

A. Replace indexes  
B. Coordinate multi-step workflows across services without a single global transaction  
C. Build a CDN  
D. Cache static assets

**75.** In a saga, a **compensating transaction** means:

A. Compressing a request body  
B. Encrypting user data  
C. Electing a new leader  
D. Undoing or offsetting a previously completed local step

**76.** **Leader election** is needed when:

A. Only one node should perform a coordination role at a time  
B. Every node must always write everything  
C. There is no shared state  
D. You want more CSS bundles

**77.** **Split-brain** means:

A. A cache miss happened twice  
B. A request used two databases  
C. Two nodes both believe they are the active leader  
D. A queue lost ordering in one partition

**78.** A quorum-based approach helps reduce split-brain because:

A. It ignores network partitions  
B. It requires majority agreement for leadership or progress  
C. It forces all data into one table  
D. It removes the need for clocks

**79.** Why do distributed locks often include a **TTL or lease timeout**?

A. To increase font size  
B. To guarantee zero conflicts forever  
C. To avoid all retries  
D. To prevent a crashed lock holder from blocking progress forever

**80.** Heavy dependence on local machine clocks is risky in distributed systems because of:

A. Clock skew and unsynchronized time across machines  
B. Strong consistency  
C. SQL joins  
D. Pagination limits

---

## SECTION E: APIS, SECURITY, OBSERVABILITY & PERFORMANCE (Q81-Q100)

**81.** Which REST principle says each request should contain all the information needed to process it?

A. Event sourcing  
B. Statelessness  
C. Leader election  
D. Sharding

**82.** Which HTTP method is expected to be both **safe** and **idempotent**?

A. POST  
B. PATCH  
C. DELETE  
D. GET

**83.** For a very large, frequently changing feed, which pagination style is usually better?

A. Page number in HTML comments  
B. Random pagination  
C. Cursor-based pagination  
D. Offset pagination with no index

**84.** Why is API versioning commonly introduced?

A. To slow development down  
B. To change behavior without breaking existing clients immediately  
C. To remove monitoring  
D. To avoid all documentation

**85.** A **signed URL** is especially useful when:

A. You want clients to upload or download directly from object storage for a limited time  
B. You need stronger SQL normalization  
C. You want to disable TLS  
D. You want to run cron jobs

**86.** **TLS** mainly protects:

A. Data stored in RAM forever  
B. Shard keys  
C. Data in transit between systems  
D. Cache hit rate

**87.** **Authentication** answers "who are you?", while **authorization** answers:

A. "How many CPUs do you have?"  
B. "Which database index exists?"  
C. "What is your cache TTL?"  
D. "What are you allowed to do?"

**88.** Rate limiting on a public API is mainly used to:

A. Increase image quality  
B. Protect the service from abuse and preserve fairness/capacity  
C. Replace login  
D. Eliminate the need for monitoring

**89.** A **p99 latency** of 800 ms means:

A. 99% of requests complete in 800 ms or less  
B. Every request takes exactly 800 ms  
C. Average latency is 800 ms  
D. The system is down 99% of the time

**90.** If average latency looks fine but p99 is very high, the system likely has:

A. No traffic  
B. Perfect consistency  
C. Tail latency problems affecting a smaller subset of requests  
D. Zero retries

**91.** Which observability tool is best for following one request across many services?

A. CDN invalidation  
B. CSS source maps  
C. Full-text search index  
D. Distributed tracing

**92.** Which metric most directly shows backlog building in an async processing system?

A. Screen brightness  
B. Queue depth  
C. Number of README files  
D. CSS selector count

**93.** If a customer says "order 817 failed somewhere," the most useful first thing to search for is:

A. Random cache keys  
B. JavaScript bundle hash  
C. The order's trace ID or correlation ID  
D. The favicon

**94.** An **error budget** is:

A. The amount of unreliability allowed by the SLO before you should slow feature changes  
B. A budget for buying more servers  
C. The number of engineers on call  
D. A cache eviction algorithm

**95.** Which alert is most aligned with user impact?

A. One debug log line changed  
B. CPU hit 5% on one internal batch worker at midnight  
C. A comment was deleted in a file  
D. User-facing error rate or latency breached the SLO

**96.** **Synthetic monitoring** means:

A. Automated probes that simulate user behavior from outside the system  
B. A real user complaint on social media  
C. Logging only SQL queries  
D. Turning off health checks

**97.** Which technique most reduces network transfer size for large JSON responses?

A. Leader election  
B. Compression such as gzip or brotli  
C. Sticky sessions  
D. Read replicas only

**98.** Why can **batching** writes improve throughput?

A. It increases page reload speed  
B. It guarantees zero failures  
C. It reduces per-write round-trip overhead  
D. It removes the need for persistence

**99.** The **N+1 query** problem means:

A. One query is always enough  
B. A CDN invalidated too many files  
C. There are too many indexes  
D. One initial query is followed by many extra queries, often one per item

**100.** A **database connection pool** helps by:

A. Reusing established connections instead of creating a new one for every request  
B. Replacing the database with a cache  
C. Encrypting payloads automatically at rest  
D. Running background jobs

---

## SECTION F: APPLIED SYSTEM DESIGN SCENARIOS (Q101-Q120)

**101.** A URL shortener is heavily read-biased. Which component most directly reduces redirect latency for popular short codes?

A. Leader election  
B. A fast cache such as Redis for hot mappings  
C. Blue-green deployment  
D. A dead-letter queue

**102.** A social feed can tolerate slightly stale counts during a partition, but staying available is critical. Which trade-off fits best?

A. CP  
B. AP  
C. CA  
D. Single-threaded only

**103.** A payment ledger must not return stale balances during a partition. Which trade-off is closer to the desired behavior?

A. AP  
B. Best effort only  
C. CP  
D. Eventual consistency first

**104.** A product catalogue is read 10,000 times per second and updated once per hour. Which caching approach is the most natural first choice?

A. Cache-aside with TTL  
B. No caching at all  
C. Recompute everything on every request  
D. Store responses only in browser history

**105.** A live sports score changes every second. Which approach is the best choice?

A. Cache it globally for 24 hours  
B. Use write-behind caching only  
C. Avoid any invalidation strategy  
D. Use short TTLs or push-based updates because stale data becomes wrong quickly

**106.** Users around the world upload and view images. Which combination best reduces latency and origin bandwidth?

A. Store images only on app servers  
B. Use read replicas only  
C. Put images in object storage and serve through a CDN  
D. Replace image URLs with SQL joins

**107.** Users in India are reading from a database hosted only in the US and complain about latency. What is the best first improvement?

A. Remove indexes  
B. Add a regional read replica closer to Indian users  
C. Convert all APIs to XML  
D. Disable caching

**108.** An order flow spans payment, inventory, and shipping services. You want reliability without a single global distributed transaction. What is the best fit?

A. Saga pattern  
B. Round robin  
C. Sticky sessions  
D. Browser local storage

**109.** A distributed job scheduler must ensure the same job is not run by multiple schedulers at the same time. What is most important?

A. Bigger frontend bundle  
B. A CDN for worker logs  
C. More comments in code  
D. A distributed lock or lease with expiry and heartbeats

**110.** You need a rate limiter that works consistently across 100 API servers. Which backing store is the most practical?

A. In-memory arrays on each API server  
B. Redis with atomic increments and expiry  
C. Browser cookies only  
D. CDN edge cache only

**111.** A system needs ordered event replay for audit and reprocessing. Which technology is the best fit?

A. RabbitMQ as a basic task queue only  
B. CDN  
C. Kafka  
D. Local filesystem logs on one server

**112.** Search autocomplete needs prefix matching and relevance ranking over text. Which backend is the best fit?

A. Redis list only  
B. Plain object storage  
C. Message queue  
D. A search engine such as Elasticsearch

**113.** A metrics platform ingests timestamped measurements continuously and queries them by time range. Which store is the best fit?

A. Time-series database or a wide-column/time-series optimized store  
B. Image CDN  
C. Signed URLs  
D. Browser session storage

**114.** During a flash sale, stale inventory cache data is causing overselling. What is the best fix?

A. Increase CDN TTL  
B. Add more colors to the UI  
C. Reserve or decrement inventory in a strongly consistent source before confirming the order  
D. Retry failed emails faster

**115.** One celebrity causes extreme traffic to a single shard in a social system. What is the core problem?

A. Quorum  
B. Hotspotting  
C. Encryption  
D. Batch size

**116.** A company wants to move from a monolith to microservices with less risk. What is the best first step?

A. Split everything into 50 services at once  
B. Remove all tests first  
C. Rewrite the frontend and backend together  
D. Extract one bounded, high-value service behind a clear API

**117.** In a social network, fan-out-on-write becomes very expensive for celebrity accounts with millions of followers. What is the better approach for those users?

A. Fan-out-on-read or a hybrid approach  
B. Store all followers in browser memory  
C. Turn off caching everywhere  
D. Force all reads to the primary region only

**118.** A user changes their profile photo, but the old image is still served globally from the CDN. What should you do?

A. Disable all CDNs forever  
B. Purge or invalidate the cached object  
C. Add more SQL joins  
D. Use fixed-window rate limiting

**119.** Why should heavy analytics queries usually run on a separate warehouse instead of the OLTP primary?

A. Warehouses cannot store data  
B. Primaries do not support SQL  
C. Large analytical scans can hurt transactional workloads and user-facing latency  
D. OLTP systems cannot have indexes

**120.** In a system design interview, what should you usually do **before** choosing specific technologies?

A. Start drawing database tables immediately  
B. Pick Kafka and Redis because they are popular  
C. Write code first  
D. Clarify functional and non-functional requirements, constraints, and traffic shape

---

## Marking

- **Total Questions:** 120  
- **Marks per Question:** 1  
- **Total Marks:** 120

---

*End of paper.*
