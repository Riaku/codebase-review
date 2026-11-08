---
categories: [database, observability]
domains: [data, reliability]
---

# Maintenance Backlog Alarm

**SHOULD** alarm on background reclamation backlog — dead rows, unmerged segments, unreleased retention — against the write rate, so a maintainer that runs but falls behind is visible.

**Why:** A maintenance job that reports success while its backlog grows is indistinguishable from one that was switched off, until the disk or the counter raises the alarm instead of the job.

**Detect:** Track the backlog per table or store — `pg_stat_user_tables.n_dead_tup` and `last_autovacuum`, `pg_stat_progress_vacuum` for a pass that never completes, compaction pending bytes, retention backlog age — and compare its trend against rows written per interval; a dashboard showing job exit status rather than backlog size is the finding.

**References:** PostgreSQL routine vacuuming, https://www.postgresql.org/docs/current/routine-vacuuming.html, PostgreSQL progress reporting, https://www.postgresql.org/docs/current/progress-reporting.html, PostgreSQL monitoring statistics, https://www.postgresql.org/docs/current/monitoring-stats.html
