---
categories: [observability]
domains: [reliability]
---

# Pool Saturation Alerting

**MUST** export connection-pool saturation — active, idle, and waiting-for-a-slot counts plus acquire time — and alert before the pool is exhausted.

**Why:** A pool at its ceiling queues callers instead of failing them, so latency climbs and requests time out while CPU and query metrics still look idle; the waiting-client count and acquire time are the only early signals that the pool, not the database, is the constraint.
**Detect:** Grep pool, proxy and driver configuration for exported saturation series (`hikaricp_connections_pending`, `hikaricp_connections_acquire_seconds`, `pgbouncer_pools_waiting_clients`, `pg_stat_activity` against `max_connections`, `sql.DBStats.WaitCount`, Jedis/Lettuce pool statistics); flag a pool with no waiting-count series and alert rules that fire only on connection errors.
**References:** HikariCP JMX monitoring, https://github.com/brettwooldridge/HikariCP/wiki/MBean-(JMX)-Monitoring-and-Management, PgBouncer usage and monitoring, https://www.pgbouncer.org/usage.html, Brendan Gregg USE method, http://www.brendangregg.com/usemethod.html, CWE-770, https://cwe.mitre.org/data/definitions/770.html
