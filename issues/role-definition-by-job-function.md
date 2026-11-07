---
categories: [authorization-access-control]
domains: [backend, governance]
---

# Roles Defined by Job Function

**SHOULD** derive every role from a job function and the smallest permission set that function needs, so roles stay few, named for the work, and free of unrelated duties.

**Why:** Roles that grow by accretion, or one role per person, make least privilege unmeasurable: every review sees a broad grant with no way to tell which permissions belong to the job and which accumulated.

**Detect:** export role definitions (`kubectl get clusterroles -o yaml`, IAM policy JSON, your `roles` and `role_permissions` tables) and count permissions per role; flag roles that span unrelated resources, roles named after a person, and a role count that tracks headcount rather than job functions. Check the role-to-job-function mapping is written down rather than inferred from who happens to hold what.

**References:** NIST role-based access control project, https://csrc.nist.gov/projects/role-based-access-control, OWASP Authorization Cheat Sheet, https://cheatsheetseries.owasp.org/cheatsheets/Authorization_Cheat_Sheet.html
