---
categories: [authentication, authorization-access-control]
domains: [backend, governance]
---

# Privileged Identity Separation

**SHOULD** require administrative work to run under an identity distinct from the one used for ordinary work, so no single credential carries both everyday and privileged access.

**Why:** An administrator who reads mail, browses, and opens tickets with the same account turns every phishing lure into a privileged credential; a separate identity means the everyday session holds no administrative rights at all.

**Detect:** check the IdP for principals holding both an administrative role and ordinary business roles; whether admin consoles accept an existing SSO session without a fresh role assumption or re-authentication; and whether admin accounts have their own device or mailbox profile rather than the daily driver.

**References:** NIST SP 800-53 AC-6(5) privileged accounts, https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final, Microsoft Entra RBAC best practices, https://learn.microsoft.com/en-us/entra/identity/role-based-access-control/best-practices
