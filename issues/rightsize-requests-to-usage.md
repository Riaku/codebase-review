---
categories: [containers-k8s, scaling-capacity]
domains: [infrastructure, reliability]
---

# Size Requests to Observed Use

**SHOULD** set CPU and memory requests within a measured band of what the workload actually consumes, and shrink them when usage drops.

**Why:** Requests are what the scheduler reserves and what autoscalers and bin-packers add node capacity for, so a workload asking for four CPUs to burn sixty millicores makes the cluster buy hardware nothing uses.

**Detect:** compare `kubectl top pods -A` or metrics-server output against each container's `resources.requests`; flag p95 usage below a quarter of the request, Vertical Pod Autoscaler recommendations ignored across several cycles, requests copied from a template and never revised, and nodes that stay under-utilised while pods sit Pending.

**References:** Kubernetes resource usage monitoring, https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-usage-monitoring/, Vertical Pod Autoscaler, https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler, Goldilocks, https://github.com/FairwindsOps/goldilocks
