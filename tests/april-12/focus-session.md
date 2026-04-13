# APRIL 12 SYSTEM DESIGN FOCUS SESSION
**Date:** April 13, 2026
**Based on:** `tests/april-12/evaluation-score.md`
**Purpose:** Convert the 94/120 result into stable system-design recall by drilling only the weak clusters.
**Time:** 35 minutes

---

## Focus Rule

Do not reread the whole paper. The candidate already has the broad vocabulary. Review only the concepts that caused wrong answers.

---

## Block 1 - Tool Matching (10 minutes)

Fill this table from memory before checking notes:

| Need | Best tool | One-sentence reason |
|---|---|---|
| Replayable ordered event stream | Kafka | Ordered replay by partition for event logs and reprocessing |
| Classic ack-based work queue | RabbitMQ | Message routing, acknowledgements, and worker queue semantics |
| Fast shared counters for rate limiting | Redis | Atomic increments and expiry across API servers |
| Text autocomplete and relevance ranking | Elasticsearch | Search indexing, prefix matching, and ranking |
| Session token lookup | Key-value store | Simple fast lookup by key |
| Large object/image storage | Object storage | Durable blob storage, usually served through CDN |

Mini-check:
1. Why is Kafka better than Redis for event replay?
2. Why is RabbitMQ better than Elasticsearch for a work queue?
3. Why is local memory wrong for a distributed rate limiter?

---

## Block 2 - Cache and Replica Nuance (10 minutes)

Write one correction sentence for each:

1. Read replicas help reads, but they do not eliminate replication lag.
2. TTL caching is useful when bounded staleness is acceptable.
3. Write-behind lowers write latency but can lose data if the cache fails before flushing.
4. Materialized views store derived/precomputed results to speed up reads.
5. Payment ledgers usually prefer CP behavior because stale balances are dangerous.

Mini-check:
1. When is cache-aside a good first choice?
2. Why is "every read must be newest" a bad match for TTL caching?
3. Why are analytics scans safer on a warehouse than on the OLTP primary?

---

## Block 3 - Reliability Concepts (8 minutes)

Memorize these exact pairs:

| Concept | Correct meaning |
|---|---|
| Kafka ordering | Guaranteed within a partition, not globally across all partitions |
| Exponential backoff | Reduces retry pressure on a failing dependency |
| Heartbeat | Detects failed or stalled workers |
| Compensating transaction | Undoes or offsets a previous saga step |
| Circuit breaker | Stops repeated calls to a failing dependency for a while |

Mini-check:
1. Why does backoff help during an outage?
2. What is the difference between leader election and compensating transaction?
3. Why should a worker send heartbeats?

---

## Block 4 - API and Observability Recall (7 minutes)

Write these four lines from memory:

1. API gateway: authentication, routing, rate limiting.
2. API versioning: evolve behavior without immediately breaking clients.
3. Cursor pagination: better for large, frequently changing feeds than offset pagination.
4. Trace/correlation ID: the key used to follow one request across services.

Mini-check:
1. If an order fails across multiple services, what ID do you search first?
2. Why does batching improve throughput?
3. Why is "frontend compilation" not an API gateway responsibility?

---

## Short Retest Recommendation

After this session, give a 20-question mixed retest with:

- 5 tool-matching questions.
- 5 caching/replica nuance questions.
- 5 reliability questions.
- 5 API/observability questions.

Target score: 16/20 or higher.
