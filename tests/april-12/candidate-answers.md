**ANSWERS**

1. B. Handling more load without unacceptable performance loss  
2. B. Each request gets a response quickly  
3. B. Adding more machines to share the load  
4. C. Distribute incoming traffic across multiple servers  
5. B. Servers are added or removed and you want minimal key remapping  
6. C. Blue-green deployment  
7. **C. The app fetches from the database, stores the result in cache, then returns it**  
8. D. Current bank account balance  
9. B. Staying available even if some responses may be stale  
10. C. Refuse some requests to preserve consistency  
11. B. Multi-row financial transactions with strong consistency  
12. A. User profiles with nested, flexible JSON fields  
13. C. Split data across multiple database nodes for scale  
14. **C. Eliminating all replication lag**  
15. **A. No support for SQL**  
16. B. Serving static content closer to end users  
17. A. Produces the same final result even if repeated multiple times  
18. D. Idempotency keys  
19. **B. Queue messages are typically consumed once, while pub/sub can fan out to multiple consumers**  
20. **A. Redis cache**

21. C. Least connections  
22. A. Session state is stored in app server memory  
23. D. Moving session state to a shared store or using stateless tokens  
24. B. Add read replicas  
25. C. Generate a unique numeric ID and encode it in Base62  
26. A. One key receives disproportionately high traffic and overloads part of the system  
27.  B. Queue depth or backlog  
28. D. Distribute keys more evenly across nodes  
29. D. Compiling frontend code  
30. **A. Test the new version on a small percentage of traffic before full rollout**  
31. C. Fast rollback by switching traffic back to the old environment    
32. B. Fixed window counter  
33. B. Clients can burst at the end of one window and the start of the next  
34. C. A shared fast datastore such as Redis  
35. A. Fast in-memory operations and atomic counter updates  
36. B. Geo-routing  
37. **D. It forces strong consistency**  
38. **C. Country code or status field**  
39. B. Hotspotting  
40. D. Use metrics and traces to find the hottest endpoint or dependency first

41. C. Relational database  
42. A. Document database  
43. D. Object storage  
44. C. Wide-column store  
45. D. Faster reads for extra write cost and storage  
46. A. Reduce expensive joins on read-heavy paths  
47. C. Duplicate data becomes harder to keep consistent  
48.   B. Updates cache and database together during the write path  
49. **B. Perfect durability even if the cache crashes**  
50.  **D. Data can be lost if the cache fails before flushing to the database**  
51. C. Stale data can survive after underlying data changes  
52.  C. Every read must reflect the newest write instantly  
53. A. Writes still usually go through the primary  
54. B. Multiple regions need local write capability   
55. C. Conflict resolution between concurrent updates  
56. **D. R \+ W \> N**  
57. C. User IDs keep changing every second  
58. C. Traffic and data may be uneven across regions, creating skew  
59. **A. You want to avoid storing any derived data**  
60. D. A columnar analytics warehouse

61. C. Smoothing traffic spikes and decoupling request handling from background work  
62. B. A message may be delivered more than once, so consumers must handle duplicates  
63. A. They prevent duplicates from causing incorrect repeated side effects  
64. D. Messages that repeatedly fail processing  
65. C. Multiple independent services need to react to the same event  
66. **A. Across all topics in all regions**  
67. **C. Elasticsearch**  
68. C. It guarantees strong consistency  
69. C. Stopping repeated calls to a failing dependency for a while  
70. B. Isolate failures by separating resources so one failure does not sink everything  
71. D. Whether the service is actually ready to handle real requests  
72. C. Replace job queues  
73.  C. Retries, crashes, and acknowledgements can create duplicates or ambiguity  
74. B. Coordinate multi-step workflows across services without a single global transaction  
75. C. Electing a new leader  
76. A. Only one node should perform a coordination role at a time  
77. C. Two nodes both believe they are the active leader  
78. **B. It requires majority agreement for leadership or progress**  
79. D. To prevent a crashed lock holder from blocking progress forever  
80. **A. Clock skew and unsynchronized time across machines**  
81. B. Statelessness  
82. D. GET  
83. D. Offset pagination with no index  
84. **A. To slow development down**  
85. A. You want clients to upload or download directly from object storage for a limited time  
86. C. Data in transit between systems  
87. D. "What are you allowed to do?"  
88.  B. Protect the service from abuse and preserve fairness/capacity  
89. A. 99% of requests complete in 800 ms or less  
90. C. Tail latency problems affecting a smaller subset of requests  
91.  D. Distributed tracing  
92. **B. Queue depth**  
93.  A. Random cache keys  
94. A. The amount of unreliability allowed by the SLO before you should slow feature changes  
95. D. User-facing error rate or latency breached the SLO  
96. A. Automated probes that simulate user behavior from outside the system  
97. B. Compression such as gzip or brotli  
98. B. It guarantees zero failures  
99. D. One initial query is followed by many extra queries, often one per item  
100. A. Reusing established connections instead of creating a new one for every request  
101. B. A fast cache such as Redis for hot mappings  
102. B. AP  
103. D. Eventual consistency first  
104. **A. Cache-aside with TTL**  
105. D. Use short TTLs or push-based updates because stale data becomes wrong quickly  
106. C. Put images in object storage and serve through a CDN  
107. B. Add a regional read replica closer to Indian users  
108. A. Saga pattern  
109. D. A distributed lock or lease with expiry and heartbeats  
110. A. In-memory arrays on each API server  
111.  D. Local filesystem logs on one server  
112. D. A search engine such as Elasticsearch  
113. A. Time-series database or a wide-column/time-series optimized store  
114. C. Reserve or decrement inventory in a strongly consistent source before confirming the order  
115. B. Hotspotting  
116. D. Extract one bounded, high-value service behind a clear API  
117. D. Extract one bounded, high-value service behind a clear API  
118. B. Purge or invalidate the cached object  
119. OLTP systems cannot have indexes.  
120. D. Clarify functional and non-functional requirements, constraints, and traffic shape  
     