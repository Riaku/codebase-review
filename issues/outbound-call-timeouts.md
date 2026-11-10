---
categories: [resilience]
domains: [reliability]
---

# Outbound Call Timeouts

**MUST** set an explicit finite connect and read timeout on every outbound client — HTTP, database, cache, queue, DNS — instead of inheriting a library default that never expires.

**Why:** A client without a timeout parks the caller's thread, connection and buffers on a socket that may never answer, so one stalled dependency exhausts the caller's workers and turns a slow response into an outage; no request recovers while every slot waits on a socket with no deadline.
**Detect:** Grep client construction for a missing timeout argument: `requests.get(` without `timeout=`, `http.Client{}` with no `Timeout`, JDBC URLs without `connectTimeout`/`socketTimeout`, `go-redis` without `ReadTimeout`, `Redis(socket_timeout=None)`, `axios.create()` without `timeout`, `SqlConnection` without `CommandTimeout`; flag explicit zero or infinite values too.
**References:** AWS Builders' Library timeouts, retries and backoff with jitter, https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/, Google SRE Book addressing cascading failures, https://sre.google/sre-book/addressing-cascading-failures/, CWE-400, https://cwe.mitre.org/data/definitions/400.html
