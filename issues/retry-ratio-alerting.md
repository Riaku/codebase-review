---
categories: [observability, resilience]
domains: [reliability]
---

# Retry Ratio Alerting

**MUST** measure retried requests as a share of total traffic and alert when that ratio climbs, not only on the failures that triggered the retries.

**Why:** Retries mask the first minutes of a dependency failure, because error rates and latency stay inside their thresholds while the retry ratio doubles; the dashboard reports health exactly when the caller is multiplying load on a dependency that is already struggling to recover.
**Detect:** Grep client instrumentation, service mesh config and dashboards for an attempt counter or retried-over-total ratio (`retry_total`, `attempts`, `grpc_client_retried_requests`, `envoy_cluster_upstream_rq_retry`, resilience4j `Retry` metrics); flag retrying clients that emit no counter, and alert rules keyed only on 5xx or latency.
**References:** AWS Builders' Library timeouts, retries and backoff with jitter, https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/, Google SRE Workbook alerting on SLOs, https://sre.google/workbook/alerting-on-slos/, resilience4j Retry, https://resilience4j.readme.io/docs/retry
