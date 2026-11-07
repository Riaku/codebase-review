---
categories: [authorization-access-control, compliance-privacy]
domains: [backend, governance]
---

# Staff Data Access Oversight

**SHOULD** route staff reads of customer records through a time-boxed grant that carries a reason and writes an audit event naming the actor, the records touched, and the ticket served.

**Why:** Support and admin tooling can read any customer's data with nothing recording why, so a compromised staff account or an insider exfiltrates silently, and the audit trail cannot separate a real ticket from curiosity.

**Detect:** grep support, admin, and impersonation handlers for `is_staff` and `is_superuser` branches that query customer models with no approval, expiry, or audit call nearby; check whether admin list and detail views emit a record-access event carrying a reason; confirm support tooling demands a ticket or justification before it returns rows.

**References:** NIST SP 800-53 AC-6(9) log use of privileged functions, https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final, Microsoft Customer Lockbox, https://learn.microsoft.com/en-us/purview/customer-lockbox-requests
