---
categories: [authorization-access-control]
domains: [backend, governance]
---

# Duty Conflict Matrix

**MUST** keep each pair of conflicting duties in separate roles or identities, so no principal can both initiate and release the same transaction.

**Why:** A principal that can request, grant, and reconcile the same action is an authorized self-dealer, and per-request checks never catch it because each step is legitimate for the role that holds it.

**Detect:** dump each role's permission set — `kubectl get clusterrole -o yaml`, an IAM policy JSON, `role_table_grants` in PostgreSQL — and flag any role holding both halves of a pair: `payment:create` with `payment:approve`, `access:request` with `access:grant`, `code:write` with `release:approve`, `ledger:post` with `ledger:reconcile`. Then confirm the approval check compares `requester_id != approver_id`, not merely that the caller holds an approve role.

**References:** NIST SP 800-53 AC-5 separation of duties, https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final, OWASP Authorization Cheat Sheet, https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
