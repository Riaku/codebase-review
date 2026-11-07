---
categories: [cloud-network]
domains: [infrastructure]
---

# Cost Attribution Labels

**MUST** tag every billable resource with an owner, service, environment, and cost center, so spend can be grouped by whatever created it.

**Why:** An untagged account produces one number nobody can split, so the service driving a doubling stays invisible and the team best placed to fix it never sees its own bill.

**Detect:** grep IaC for `tags` or `labels` blocks missing owner, service, environment, and cost-center keys; check the cost-allocation report or per-namespace breakdown for a large untagged share rather than a rounding error; confirm the keys are activated as cost-allocation dimensions, because a tag the billing export ignores groups nothing.

**References:** AWS tagging best practices, https://docs.aws.amazon.com/whitepapers/latest/tagging-best-practices/tagging-best-practices.html, GCP resource labels, https://cloud.google.com/compute/docs/labeling-resources, FinOps framework capabilities, https://www.finops.org/framework/capabilities/
