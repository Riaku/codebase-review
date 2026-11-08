---
categories: [database, scaling-capacity]
domains: [data, reliability]
---

# Counter Exhaustion Headroom

**MUST** alarm on remaining headroom for every finite-width counter or identifier whose exhaustion halts writes, with a warning tier that leaves time to act before the stop.

**Why:** The limit is known in advance, so exhaustion is a self-inflicted outage with a published deadline: every day of headroom burned without an alarm is planning time nobody used, and the stop itself usually needs a drain, freeze, or single-mode migration to clear.

**Detect:** Compute headroom against the known limit — `SELECT age(datfrozenxid) FROM pg_database` versus `autovacuum_freeze_max_age`, a sequence's `last_value` versus its column type maximum, a generation or epoch field versus its width — then read the alert rules: a threshold only at the stop, or no rule at all, is the finding.

**References:** PostgreSQL routine vacuuming, https://www.postgresql.org/docs/current/routine-vacuuming.html, PostgreSQL `pg_database` catalog, https://www.postgresql.org/docs/current/catalog-pg-database.html, Alerting on SLOs (Google SRE Workbook), https://sre.google/workbook/alerting-on-slos/
