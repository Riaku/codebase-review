---
categories: [cloud-network, scaling-capacity]
domains: [infrastructure, reliability]
---

# Reclaim Idle Capacity

**SHOULD** scale traffic-free workloads to zero, schedule non-production ones off out of hours, and delete capacity nothing binds to, rather than paying for replicas that serve nothing.

**Why:** Idle replicas, orphaned volumes, and staging clusters running around the clock are invisible in a dashboard tracking cost per request, so they accumulate silently until they outweigh the workloads anyone chose to pay for.

**Detect:** list replicas with no requests over a trailing week (per-service RPS, ingress counters, `kubectl get hpa` showing a floor never breached), namespaces idle overnight, unattached volumes and load balancers, and dev or staging clusters with no shutdown schedule; check a `ScaledObject`, CronJob, or delete job exists for each, and that node-pool consolidation is enabled where the platform offers it.

**References:** KEDA scale to zero, https://keda.sh/docs/latest/concepts/scaling-deployments/, Karpenter consolidation, https://karpenter.sh/docs/concepts/disruption/, AWS cost optimization pillar, https://docs.aws.amazon.com/wellarchitected/latest/cost-optimization-pillar/welcome.html
