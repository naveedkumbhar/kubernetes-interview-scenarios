# ☸️ Kubernetes Production Interview Scenarios & Troubleshooting Runbooks

> Battle-tested Kubernetes production interview questions, incident root-cause triage, zero-downtime cluster upgrades, HPA tuning, networking, and Helm charts.

<!-- Total Scenarios: 186 | Author: Naveed Ahmed -->

[![Live Interactive Simulator](https://img.shields.io/badge/Live_Simulator-interview.naveedkumbhar.com-00d2ff?style=for-the-badge&logo=googlechrome&logoColor=white)](https://interview.naveedkumbhar.com/?cat=kubernetes)
[![Total Scenarios](https://img.shields.io/badge/Scenarios-186_Live-4ade80?style=for-the-badge)](https://interview.naveedkumbhar.com/?cat=kubernetes)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](LICENSE)
[![Author](https://img.shields.io/badge/Author-Naveed_Ahmed-purple?style=for-the-badge&logo=github)](https://github.com/naveedkumbhar)

---

### 🚀 Interactive Practice Mode Available

All **186 scenarios** in this repository are interactive on the live practice engine with search, category filtering, bookmarking, and timer modes:
👉 **[Launch Interactive Simulator on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)**

---

## 📑 Scenarios Directory

1. [Zero-Downtime Amazon EKS Minor & Multi-Version Upgrade (v1.34 → v1.36+)](#scenario-1-zero-downtime-amazon-eks-minor-multi-version-upgrade-v1-34-v1-36)
2. [Pod Stuck in Pending — Scheduler & Resource Triage](#scenario-2-pod-stuck-in-pending-scheduler-resource-triage)
3. [Pod in CrashLoopBackOff — Diagnostic & Root Cause Workflow](#scenario-3-pod-in-crashloopbackoff-diagnostic-root-cause-workflow)
4. [Pod Running but Service Inaccessible — End-to-End Network Approach](#scenario-4-pod-running-but-service-inaccessible-end-to-end-network-approach)
5. [New Deployment Breaks Production — Fast & Safe Rollback](#scenario-5-new-deployment-breaks-production-fast-safe-rollback)
6. [CI/CD Pipeline Succeeds but New Version Isn't Deployed — Debugging](#scenario-6-ci-cd-pipeline-succeeds-but-new-version-isn-t-deployed-debugging)
7. [Design a High-Availability Cloud Infrastructure for Millions of Requests/Day](#scenario-7-design-a-high-availability-cloud-infrastructure-for-millions-of-requests-day)
8. [Kubernetes Cluster Intermittent Pod Failures & High Latency — Systematic Troubleshooting](#scenario-8-kubernetes-cluster-intermittent-pod-failures-high-latency-systematic-troubleshooting)
9. [Deployment vs StatefulSet vs DaemonSet — Architectural Decision Matrix](#scenario-9-deployment-vs-statefulset-vs-daemonset-architectural-decision-matrix)
10. [Ingress Controller — End-to-End OSI Layer 7 Traffic Flow](#scenario-10-ingress-controller-end-to-end-osi-layer-7-traffic-flow)
11. [Troubleshooting ImagePullBackOff & ErrImagePull — 4 Root Causes](#scenario-11-troubleshooting-imagepullbackoff-errimagepull-4-root-causes)
12. [Kubernetes Pod Logs & Events — Senior Diagnostic Command Toolkit](#scenario-12-kubernetes-pod-logs-events-senior-diagnostic-command-toolkit)
13. [Configuring CPU & Memory Requests and Limits — QoS Classes & Throttling](#scenario-13-configuring-cpu-memory-requests-and-limits-qos-classes-throttling)
14. [Horizontal Pod Autoscaler (HPA) — Internals, Algorithm & Stabilization](#scenario-14-horizontal-pod-autoscaler-hpa-internals-algorithm-stabilization)
15. [Troubleshooting High CPU or Memory Usage in Kubernetes](#scenario-15-troubleshooting-high-cpu-or-memory-usage-in-kubernetes)
16. [Kubernetes Resource Right-Sizing & Bin-Packing for Cost Reduction](#scenario-16-kubernetes-resource-right-sizing-bin-packing-for-cost-reduction)
17. [Core Azure Cloud Services in Enterprise DevOps & DevSecOps](#scenario-17-core-azure-cloud-services-in-enterprise-devops-devsecops)
18. [Azure Kubernetes Service (AKS) — Architecture, Deployment & Troubleshooting](#scenario-18-azure-kubernetes-service-aks-architecture-deployment-troubleshooting)
19. [Managing Secrets Securely in Kubernetes — External Secrets Operator (ESO)](#scenario-19-managing-secrets-securely-in-kubernetes-external-secrets-operator-eso)
20. [What Really Happens Under the Hood When You Run 'kubectl apply -f deployment.yaml'?](#scenario-20-what-really-happens-under-the-hood-when-you-run-kubectl-apply-f-deployment-yaml)
21. [Kubernetes Q1: Your pod is stuck in Pending state What do you do [L1]](#scenario-21-kubernetes-q1-your-pod-is-stuck-in-pending-state-what-do-you-do-l1)
22. [Kubernetes Q2: A pod is in CrashLoopBackOff How do you debug it [L1]](#scenario-22-kubernetes-q2-a-pod-is-in-crashloopbackoff-how-do-you-debug-it-l1)
23. [Kubernetes Q3: A pod shows OOMKilled in its status What happened and how do you fix it [L2]](#scenario-23-kubernetes-q3-a-pod-shows-oomkilled-in-its-status-what-happened-and-how-do-you-fix-it-l2)
24. [Kubernetes Q4: Your deployment rollout is stuck Pods from the new version arent coming up but old ones are still running Whats happening [L2]](#scenario-24-kubernetes-q4-your-deployment-rollout-is-stuck-pods-from-the-new-version-arent-coming-up-but-old-ones-are-still-running-whats-happening-l2)
25. [Kubernetes Q5: A pod is Running but your app is not reachable via the Service What do you check [L2]](#scenario-25-kubernetes-q5-a-pod-is-running-but-your-app-is-not-reachable-via-the-service-what-do-you-check-l2)
26. [Kubernetes Q6: A node in your cluster shows NotReady Your team is panicking because several services are on it Whats your action plan [L3]](#scenario-26-kubernetes-q6-a-node-in-your-cluster-shows-notready-your-team-is-panicking-because-several-services-are-on-it-whats-your-action-plan-l3)
27. [Kubernetes Q7: Your HPA (Horizontal Pod Autoscaler) is not scaling up even though CPU usage is high Why [L2]](#scenario-27-kubernetes-q7-your-hpa-horizontal-pod-autoscaler-is-not-scaling-up-even-though-cpu-usage-is-high-why-l2)
28. [Kubernetes Q8: A pod has been running fine for weeks and suddenly starts failing with ImagePullBackOff Nothing in the pod spec changed What could cause this [L3]](#scenario-28-kubernetes-q8-a-pod-has-been-running-fine-for-weeks-and-suddenly-starts-failing-with-imagepullbackoff-nothing-in-the-pod-spec-changed-what-could-cause-this-l3)
29. [Kubernetes Q9: You run kubectl exec -it <pod> -- bash and get container not found Whats wrong [L2]](#scenario-29-kubernetes-q9-you-run-kubectl-exec-it-pod-bash-and-get-container-not-found-whats-wrong-l2)
30. [Kubernetes Q10: Your init container is stuck and the main container never starts How do you debug [L2]](#scenario-30-kubernetes-q10-your-init-container-is-stuck-and-the-main-container-never-starts-how-do-you-debug-l2)
31. [Kubernetes Q11: Whats the difference between a Deployment and a StatefulSet When would you use each [L1]](#scenario-31-kubernetes-q11-whats-the-difference-between-a-deployment-and-a-statefulset-when-would-you-use-each-l1)
32. [Kubernetes Q12: You need to run a database in Kubernetes Someone says just use a Deployment with a PVC Is that okay [L2]](#scenario-32-kubernetes-q12-you-need-to-run-a-database-in-kubernetes-someone-says-just-use-a-deployment-with-a-pvc-is-that-okay-l2)
33. [Kubernetes Q13: You updated a ConfigMap thats mounted as an environment variable in a pod The pod still shows the old value Why [L2]](#scenario-33-kubernetes-q13-you-updated-a-configmap-thats-mounted-as-an-environment-variable-in-a-pod-the-pod-still-shows-the-old-value-why-l2)
34. [Kubernetes Q14: How would you ensure a critical pod always runs on the same node [L2]](#scenario-34-kubernetes-q14-how-would-you-ensure-a-critical-pod-always-runs-on-the-same-node-l2)
35. [Kubernetes Q15: You want to make sure two pods of the same app NEVER run on the same node How [L2]](#scenario-35-kubernetes-q15-you-want-to-make-sure-two-pods-of-the-same-app-never-run-on-the-same-node-how-l2)
36. [Kubernetes Q16: Your deployment has 10 replicas You need to do a zero-downtime deploy of a new version How do you configure and verify it [L3]](#scenario-36-kubernetes-q16-your-deployment-has-10-replicas-you-need-to-do-a-zero-downtime-deploy-of-a-new-version-how-do-you-configure-and-verify-it-l3)
37. [Kubernetes Q17: What is a DaemonSet and when do you use it [L1]](#scenario-37-kubernetes-q17-what-is-a-daemonset-and-when-do-you-use-it-l1)
38. [Kubernetes Q18: You have a DaemonSet but some nodes arent getting a pod Why [L2]](#scenario-38-kubernetes-q18-you-have-a-daemonset-but-some-nodes-arent-getting-a-pod-why-l2)
39. [Kubernetes Q19: When would you use a Job vs a CronJob [L2]](#scenario-39-kubernetes-q19-when-would-you-use-a-job-vs-a-cronjob-l2)
40. [Kubernetes Q20: Your CronJob is creating overlapping runs — the previous job hasnt finished when the next one starts How do you fix it [L2]](#scenario-40-kubernetes-q20-your-cronjob-is-creating-overlapping-runs-the-previous-job-hasnt-finished-when-the-next-one-starts-how-do-you-fix-it-l2)
41. [Kubernetes Q21: What is the difference between ClusterIP NodePort and LoadBalancer service types [L1]](#scenario-41-kubernetes-q21-what-is-the-difference-between-clusterip-nodeport-and-loadbalancer-service-types-l1)
42. [Kubernetes Q22: What is an Ingress and why do you need it when you already have LoadBalancer services [L2]](#scenario-42-kubernetes-q22-what-is-an-ingress-and-why-do-you-need-it-when-you-already-have-loadbalancer-services-l2)
43. [Kubernetes Q23: Your Ingress is returning 404 for a path that youve configured What do you check [L2]](#scenario-43-kubernetes-q23-your-ingress-is-returning-404-for-a-path-that-youve-configured-what-do-you-check-l2)
44. [Kubernetes Q24: You have a microservices app where Service A should never talk directly to Service C only through Service B How do you enforce this in Kubernetes [L3]](#scenario-44-kubernetes-q24-you-have-a-microservices-app-where-service-a-should-never-talk-directly-to-service-c-only-through-service-b-how-do-you-enforce-this-in-kubernetes-l3)
45. [Kubernetes Q25: What is a headless service and why would you use it [L2]](#scenario-45-kubernetes-q25-what-is-a-headless-service-and-why-would-you-use-it-l2)
46. [Kubernetes Q26: A request is going from Pod A to Pod B via a Service and its very slow How do you troubleshoot network latency in Kubernetes [L3]](#scenario-46-kubernetes-q26-a-request-is-going-from-pod-a-to-pod-b-via-a-service-and-its-very-slow-how-do-you-troubleshoot-network-latency-in-kubernetes-l3)
47. [Kubernetes Q27: DNS resolution is failing inside your cluster Pods cant resolve service names What do you check [L2]](#scenario-47-kubernetes-q27-dns-resolution-is-failing-inside-your-cluster-pods-cant-resolve-service-names-what-do-you-check-l2)
48. [Kubernetes Q28: What is the difference between a PersistentVolume (PV) and a PersistentVolumeClaim (PVC) [L1]](#scenario-48-kubernetes-q28-what-is-the-difference-between-a-persistentvolume-pv-and-a-persistentvolumeclaim-pvc-l1)
49. [Kubernetes Q29: A PVC is stuck in Pending state What do you check [L2]](#scenario-49-kubernetes-q29-a-pvc-is-stuck-in-pending-state-what-do-you-check-l2)
50. [Kubernetes Q30: You deleted a PVC but the data is gone How could you have protected it [L2]](#scenario-50-kubernetes-q30-you-deleted-a-pvc-but-the-data-is-gone-how-could-you-have-protected-it-l2)
51. [Kubernetes Q31: A StatefulSet pod cant start because its trying to attach a volume thats still attached to a terminated pod on a dead node How do you fix it [L3]](#scenario-51-kubernetes-q31-a-statefulset-pod-cant-start-because-its-trying-to-attach-a-volume-thats-still-attached-to-a-terminated-pod-on-a-dead-node-how-do-you-fix-it-l3)
52. [Kubernetes Q32: A developer says they cant list pods in the production namespace but they can in staging How do you debug this [L2]](#scenario-52-kubernetes-q32-a-developer-says-they-cant-list-pods-in-the-production-namespace-but-they-can-in-staging-how-do-you-debug-this-l2)
53. [Kubernetes Q33: You run a pod that needs to call the Kubernetes API (eg to list other pods) How do you set this up securely [L2]](#scenario-53-kubernetes-q33-you-run-a-pod-that-needs-to-call-the-kubernetes-api-eg-to-list-other-pods-how-do-you-set-this-up-securely-l2)
54. [Kubernetes Q34: Someone accidentally ran kubectl delete clusterrolebinding cluster-admin and deleted the cluster admin binding Now no one can manage the cluster What do you do [L3]](#scenario-54-kubernetes-q34-someone-accidentally-ran-kubectl-delete-clusterrolebinding-cluster-admin-and-deleted-the-cluster-admin-binding-now-no-one-can-manage-the-cluster-what-do-you-do-l3)
55. [Kubernetes Q35: Your app gets a traffic spike every day at 9 AM when offices open HPA isnt fast enough What do you do [L2]](#scenario-55-kubernetes-q35-your-app-gets-a-traffic-spike-every-day-at-9-am-when-offices-open-hpa-isnt-fast-enough-what-do-you-do-l2)
56. [Kubernetes Q36: HPA is scaling pods up and down too aggressively causing instability How do you fix it [L2]](#scenario-56-kubernetes-q36-hpa-is-scaling-pods-up-and-down-too-aggressively-causing-instability-how-do-you-fix-it-l2)
57. [Kubernetes Q37: Your cluster has 50 nodes and pod scheduling is taking 10+ seconds What could cause this and how do you fix it [L3]](#scenario-57-kubernetes-q37-your-cluster-has-50-nodes-and-pod-scheduling-is-taking-10-seconds-what-could-cause-this-and-how-do-you-fix-it-l3)
58. [Kubernetes Q38: You need to run a privileged pod that can modify kernel parameters on the host How do you do this and what are the security implications [L3]](#scenario-58-kubernetes-q38-you-need-to-run-a-privileged-pod-that-can-modify-kernel-parameters-on-the-host-how-do-you-do-this-and-what-are-the-security-implications-l3)
59. [Kubernetes Q39: You need to do a zero-downtime migration of a StatefulSet (eg upgrading Postgres version) Walk me through your approach [L3]](#scenario-59-kubernetes-q39-you-need-to-do-a-zero-downtime-migration-of-a-statefulset-eg-upgrading-postgres-version-walk-me-through-your-approach-l3)
60. [Kubernetes Q40: Your team wants to implement GitOps for Kubernetes What tools would you recommend and what does the workflow look like [L3]](#scenario-60-kubernetes-q40-your-team-wants-to-implement-gitops-for-kubernetes-what-tools-would-you-recommend-and-what-does-the-workflow-look-like-l3)
61. [Kubernetes Q41: How do you handle secrets in Kubernetes What are the problems with default Kubernetes Secrets [L2]](#scenario-61-kubernetes-q41-how-do-you-handle-secrets-in-kubernetes-what-are-the-problems-with-default-kubernetes-secrets-l2)
62. [Kubernetes Q42: A developer wants to test a microservice that depends on 8 other services Setting up the full cluster locally is impractical What would you suggest [L3]](#scenario-62-kubernetes-q42-a-developer-wants-to-test-a-microservice-that-depends-on-8-other-services-setting-up-the-full-cluster-locally-is-impractical-what-would-you-suggest-l3)
63. [Kubernetes Q43: Your cluster upgrade from 126 to 127 failed halfway through Control plane is on 127 but worker nodes are still on 126 Is this okay [L2]](#scenario-63-kubernetes-q43-your-cluster-upgrade-from-126-to-127-failed-halfway-through-control-plane-is-on-127-but-worker-nodes-are-still-on-126-is-this-okay-l2)
64. [Kubernetes Q44: How do you handle configuration that differs between environments (dev staging prod) in Kubernetes [L2]](#scenario-64-kubernetes-q44-how-do-you-handle-configuration-that-differs-between-environments-dev-staging-prod-in-kubernetes-l2)
65. [Kubernetes Q45: You want to implement pod disruption budgets across your cluster What is a PDB and how does it protect your services [L3]](#scenario-65-kubernetes-q45-you-want-to-implement-pod-disruption-budgets-across-your-cluster-what-is-a-pdb-and-how-does-it-protect-your-services-l3)
66. [Kubernetes Q46: What happens to pods when you run kubectl drain on a node [L2]](#scenario-66-kubernetes-q46-what-happens-to-pods-when-you-run-kubectl-drain-on-a-node-l2)
67. [Kubernetes Q47: Explain how the Kubernetes scheduler makes a placement decision for a new pod [L3]](#scenario-67-kubernetes-q47-explain-how-the-kubernetes-scheduler-makes-a-placement-decision-for-a-new-pod-l3)
68. [Kubernetes Q48: What is a LimitRange and why would you use it [L2]](#scenario-68-kubernetes-q48-what-is-a-limitrange-and-why-would-you-use-it-l2)
69. [Kubernetes Q49: You have a multi-tenant cluster where different teams share the cluster How do you isolate them [L3]](#scenario-69-kubernetes-q49-you-have-a-multi-tenant-cluster-where-different-teams-share-the-cluster-how-do-you-isolate-them-l3)
70. [Kubernetes Q50: Explain the difference between kubectl apply and kubectl create When would you use each [L3]](#scenario-70-kubernetes-q50-explain-the-difference-between-kubectl-apply-and-kubectl-create-when-would-you-use-each-l3)
71. [Kubernetes Q51: Your readiness probe keeps failing even though the app is working fine What could be wrong [L2]](#scenario-71-kubernetes-q51-your-readiness-probe-keeps-failing-even-though-the-app-is-working-fine-what-could-be-wrong-l2)
72. [Kubernetes Q52: What is the difference between liveness and readiness probes Give a scenario where each is important [L2]](#scenario-72-kubernetes-q52-what-is-the-difference-between-liveness-and-readiness-probes-give-a-scenario-where-each-is-important-l2)
73. [Kubernetes Q53: Describe the pod lifecycle from kubectl apply to the app serving traffic [L3]](#scenario-73-kubernetes-q53-describe-the-pod-lifecycle-from-kubectl-apply-to-the-app-serving-traffic-l3)
74. [Kubernetes Q54: Someone applied a bad NetworkPolicy thats blocking all traffic in the cluster How do you recover [L2]](#scenario-74-kubernetes-q54-someone-applied-a-bad-networkpolicy-thats-blocking-all-traffic-in-the-cluster-how-do-you-recover-l2)
75. [Kubernetes Q55: What is the role of etcd in Kubernetes and what happens if etcd goes down [L3]](#scenario-75-kubernetes-q55-what-is-the-role-of-etcd-in-kubernetes-and-what-happens-if-etcd-goes-down-l3)
76. [Kubernetes Q56: How do you pass sensitive configuration (like DB passwords) to a pod without hardcoding them [L2]](#scenario-76-kubernetes-q56-how-do-you-pass-sensitive-configuration-like-db-passwords-to-a-pod-without-hardcoding-them-l2)
77. [Kubernetes Q57: You need to run a pod that requires access to the host network (like a network monitoring tool) How do you configure this [L3]](#scenario-77-kubernetes-q57-you-need-to-run-a-pod-that-requires-access-to-the-host-network-like-a-network-monitoring-tool-how-do-you-configure-this-l3)
78. [Kubernetes Q58: Explain the concept of resource requests vs limits What happens if you only set limits and not requests [L2]](#scenario-78-kubernetes-q58-explain-the-concept-of-resource-requests-vs-limits-what-happens-if-you-only-set-limits-and-not-requests-l2)
79. [Kubernetes Q59: What are the three QoS classes in Kubernetes and how does each affect eviction [L3]](#scenario-79-kubernetes-q59-what-are-the-three-qos-classes-in-kubernetes-and-how-does-each-affect-eviction-l3)
80. [Kubernetes Q60: You have a multi-container pod (sidecar pattern) How do the containers share data with each other [L2]](#scenario-80-kubernetes-q60-you-have-a-multi-container-pod-sidecar-pattern-how-do-the-containers-share-data-with-each-other-l2)
81. [Kubernetes Q61: What is the difference between emptyDir and hostPath volumes [L2]](#scenario-81-kubernetes-q61-what-is-the-difference-between-emptydir-and-hostpath-volumes-l2)
82. [Kubernetes Q62: A cluster-autoscaler is not scaling up even though pods are Pending What could be wrong [L3]](#scenario-82-kubernetes-q62-a-cluster-autoscaler-is-not-scaling-up-even-though-pods-are-pending-what-could-be-wrong-l3)
83. [Kubernetes Q63: How do you roll back a Helm release [L2]](#scenario-83-kubernetes-q63-how-do-you-roll-back-a-helm-release-l2)
84. [Kubernetes Q64: What is Helm and why is it used instead of raw YAML [L2]](#scenario-84-kubernetes-q64-what-is-helm-and-why-is-it-used-instead-of-raw-yaml-l2)
85. [Kubernetes Q65: Explain how Kubernetes handles pod eviction during node memory pressure [L3]](#scenario-85-kubernetes-q65-explain-how-kubernetes-handles-pod-eviction-during-node-memory-pressure-l3)
86. [Kubernetes Q66: What is the purpose of terminationGracePeriodSeconds [L2]](#scenario-86-kubernetes-q66-what-is-the-purpose-of-terminationgraceperiodseconds-l2)
87. [Kubernetes Q67: You need to run a pod that will only start after a specific ConfigMap exists in the cluster How do you implement this [L3]](#scenario-87-kubernetes-q67-you-need-to-run-a-pod-that-will-only-start-after-a-specific-configmap-exists-in-the-cluster-how-do-you-implement-this-l3)
88. [Kubernetes Q68: What is the purpose of podAntiAffinity with topologyKey topologykubernetesio/zone [L2]](#scenario-88-kubernetes-q68-what-is-the-purpose-of-podantiaffinity-with-topologykey-topologykubernetesio-zone-l2)
89. [Kubernetes Q69: Describe the Container Storage Interface (CSI) and why it replaced in-tree volume plugins [L3]](#scenario-89-kubernetes-q69-describe-the-container-storage-interface-csi-and-why-it-replaced-in-tree-volume-plugins-l3)
90. [Kubernetes Q70: What is a mutating admission webhook and give a practical use case [L3]](#scenario-90-kubernetes-q70-what-is-a-mutating-admission-webhook-and-give-a-practical-use-case-l3)
91. [Kubernetes Q71: Pod shows ErrImagePull [L1]](#scenario-91-kubernetes-q71-pod-shows-errimagepull-l1)
92. [Kubernetes Q72: Deployment has 0 ready pods but desired is 3 [L2]](#scenario-92-kubernetes-q72-deployment-has-0-ready-pods-but-desired-is-3-l2)
93. [Kubernetes Q73: How do you scale a deployment to 5 replicas [L1]](#scenario-93-kubernetes-q73-how-do-you-scale-a-deployment-to-5-replicas-l1)
94. [Kubernetes Q74: NodePort service not reachable from outside [L2]](#scenario-94-kubernetes-q74-nodeport-service-not-reachable-from-outside-l2)
95. [Kubernetes Q75: Two pods cant communicate even though NetworkPolicy allows it [L2]](#scenario-95-kubernetes-q75-two-pods-cant-communicate-even-though-networkpolicy-allows-it-l2)
96. [Kubernetes Q76: How do you upgrade Kubernetes version with zero downtime [L3]](#scenario-96-kubernetes-q76-how-do-you-upgrade-kubernetes-version-with-zero-downtime-l3)
97. [Kubernetes Q77: Ingress shows Address <pending> [L2]](#scenario-97-kubernetes-q77-ingress-shows-address-pending-l2)
98. [Kubernetes Q78: How do you get logs from all pods of a deployment [L1]](#scenario-98-kubernetes-q78-how-do-you-get-logs-from-all-pods-of-a-deployment-l1)
99. [Kubernetes Q79: Horizontal Pod Autoscaler shows unknown/50% for current metric [L2]](#scenario-99-kubernetes-q79-horizontal-pod-autoscaler-shows-unknown-50-for-current-metric-l2)
100. [Kubernetes Q80: etcd backup failed Recovery steps [L3]](#scenario-100-kubernetes-q80-etcd-backup-failed-recovery-steps-l3)
101. [Kubernetes Q81: A developer accidentally deleted a namespace How do you recover [L2]](#scenario-101-kubernetes-q81-a-developer-accidentally-deleted-a-namespace-how-do-you-recover-l2)
102. [Kubernetes Q82: Pod shows Terminating for hours and wont delete [L2]](#scenario-102-kubernetes-q82-pod-shows-terminating-for-hours-and-wont-delete-l2)
103. [Kubernetes Q83: Service mesh vs NetworkPolicy — when do you use each [L3]](#scenario-103-kubernetes-q83-service-mesh-vs-networkpolicy-when-do-you-use-each-l3)
104. [Kubernetes Q84: How do you make a pod restart on config change without a code change [L2]](#scenario-104-kubernetes-q84-how-do-you-make-a-pod-restart-on-config-change-without-a-code-change-l2)
105. [Kubernetes Q85: A CronJob job ran but the pod isnt showing in kubectl get jobs [L2]](#scenario-105-kubernetes-q85-a-cronjob-job-ran-but-the-pod-isnt-showing-in-kubectl-get-jobs-l2)
106. [Kubernetes Q86: Your admission webhook is blocking all pod creation cluster-wide How do you recover [L3]](#scenario-106-kubernetes-q86-your-admission-webhook-is-blocking-all-pod-creation-cluster-wide-how-do-you-recover-l3)
107. [Kubernetes Q87: How do you check if a service account has permission to create pods [L2]](#scenario-107-kubernetes-q87-how-do-you-check-if-a-service-account-has-permission-to-create-pods-l2)
108. [Kubernetes Q88: What is the difference between kubectl get and kubectl describe [L1]](#scenario-108-kubernetes-q88-what-is-the-difference-between-kubectl-get-and-kubectl-describe-l1)
109. [Kubernetes Q89: You want to run a one-off debug pod on a specific node How [L2]](#scenario-109-kubernetes-q89-you-want-to-run-a-one-off-debug-pod-on-a-specific-node-how-l2)
110. [Kubernetes Q90: Explain how kube-proxy implements Services using iptables [L3]](#scenario-110-kubernetes-q90-explain-how-kube-proxy-implements-services-using-iptables-l3)
111. [Kubernetes Q91: What is topology spread constraints and when would you use it over pod anti-affinity [L2]](#scenario-111-kubernetes-q91-what-is-topology-spread-constraints-and-when-would-you-use-it-over-pod-anti-affinity-l2)
112. [Kubernetes Q92: A pod needs GPU resources How do you configure it [L2]](#scenario-112-kubernetes-q92-a-pod-needs-gpu-resources-how-do-you-configure-it-l2)
113. [Kubernetes Q93: Describe leader election in Kubernetes control plane components [L3]](#scenario-113-kubernetes-q93-describe-leader-election-in-kubernetes-control-plane-components-l3)
114. [Kubernetes Q94: What is a finalizer and when would you use one [L2]](#scenario-114-kubernetes-q94-what-is-a-finalizer-and-when-would-you-use-one-l2)
115. [Kubernetes Q95: How does the Kubernetes garbage collector work [L3]](#scenario-115-kubernetes-q95-how-does-the-kubernetes-garbage-collector-work-l3)
116. [Kubernetes Q96: How do you run a privileged debug container on a running pod without modifying the pod spec [L2]](#scenario-116-kubernetes-q96-how-do-you-run-a-privileged-debug-container-on-a-running-pod-without-modifying-the-pod-spec-l2)
117. [Kubernetes Q97: What is the Kubernetes watch mechanism and how do informers use it [L3]](#scenario-117-kubernetes-q97-what-is-the-kubernetes-watch-mechanism-and-how-do-informers-use-it-l3)
118. [Kubernetes Q98: Explain the difference between kubectl apply with a file vs kubectl apply -k (kustomize) [L2]](#scenario-118-kubernetes-q98-explain-the-difference-between-kubectl-apply-with-a-file-vs-kubectl-apply-k-kustomize-l2)
119. [Kubernetes Q99: How would you migrate a stateful workload from one Kubernetes cluster to another with minimal downtime [L3]](#scenario-119-kubernetes-q99-how-would-you-migrate-a-stateful-workload-from-one-kubernetes-cluster-to-another-with-minimal-downtime-l3)
120. [Kubernetes Q100: What is KEDA and how does it extend HPA [L3]](#scenario-120-kubernetes-q100-what-is-keda-and-how-does-it-extend-hpa-l3)
121. [Kubernetes Q101: How do you expose a gRPC service in Kubernetes [L2]](#scenario-121-kubernetes-q101-how-do-you-expose-a-grpc-service-in-kubernetes-l2)
122. [Kubernetes Q102: Explain how Kubernetes handles rolling back a DaemonSet update [L3]](#scenario-122-kubernetes-q102-explain-how-kubernetes-handles-rolling-back-a-daemonset-update-l3)
123. [Kubernetes Q103: A Kubernetes Job is stuck at 0/1 Running and never starts What do you check [L2]](#scenario-123-kubernetes-q103-a-kubernetes-job-is-stuck-at-0-1-running-and-never-starts-what-do-you-check-l2)
124. [Kubernetes Q104: How do you configure a pod to get secrets from HashiCorp Vault without modifying app code [L2]](#scenario-124-kubernetes-q104-how-do-you-configure-a-pod-to-get-secrets-from-hashicorp-vault-without-modifying-app-code-l2)
125. [Kubernetes Q105: What is the Kubernetes control loop and how does it apply to custom operators [L3]](#scenario-125-kubernetes-q105-what-is-the-kubernetes-control-loop-and-how-does-it-apply-to-custom-operators-l3)
126. [Kubernetes Q106: How do you restrict a pod from accessing the cloud metadata endpoint (eg 169254169254) [L2]](#scenario-126-kubernetes-q106-how-do-you-restrict-a-pod-from-accessing-the-cloud-metadata-endpoint-eg-169254169254-l2)
127. [Kubernetes Q107: What is a ServiceAccount token and when does it expire [L2]](#scenario-127-kubernetes-q107-what-is-a-serviceaccount-token-and-when-does-it-expire-l2)
128. [Kubernetes Q108: Explain Kubernetes Operator pattern vs Helm chart When would you build an Operator [L3]](#scenario-128-kubernetes-q108-explain-kubernetes-operator-pattern-vs-helm-chart-when-would-you-build-an-operator-l3)
129. [Kubernetes Q109: How do you do a canary deployment on Kubernetes without a service mesh [L2]](#scenario-129-kubernetes-q109-how-do-you-do-a-canary-deployment-on-kubernetes-without-a-service-mesh-l2)
130. [Kubernetes Q110: What is the purpose of the kube-proxy and what happens if it goes down [L3]](#scenario-130-kubernetes-q110-what-is-the-purpose-of-the-kube-proxy-and-what-happens-if-it-goes-down-l3)
131. [Kubernetes Q111: How do you share a single Nginx config across multiple pods [L2]](#scenario-131-kubernetes-q111-how-do-you-share-a-single-nginx-config-across-multiple-pods-l2)
132. [Kubernetes Q112: What is Pod Topology Spread Constraints and how is it different from podAntiAffinity [L3]](#scenario-132-kubernetes-q112-what-is-pod-topology-spread-constraints-and-how-is-it-different-from-podantiaffinity-l3)
133. [Kubernetes Q113: How do you implement health checks for a gRPC service in Kubernetes [L2]](#scenario-133-kubernetes-q113-how-do-you-implement-health-checks-for-a-grpc-service-in-kubernetes-l2)
134. [Kubernetes Q114: Describe how Kubernetes implements Services using IPVS mode instead of iptables [L3]](#scenario-134-kubernetes-q114-describe-how-kubernetes-implements-services-using-ipvs-mode-instead-of-iptables-l3)
135. [Kubernetes Q115: You have a Kubernetes cluster in two regions for disaster recovery How do you sync workloads [L2]](#scenario-135-kubernetes-q115-you-have-a-kubernetes-cluster-in-two-regions-for-disaster-recovery-how-do-you-sync-workloads-l2)
136. [Kubernetes Q116: What is the Container Runtime Interface (CRI) and what runtimes are commonly used [L3]](#scenario-136-kubernetes-q116-what-is-the-container-runtime-interface-cri-and-what-runtimes-are-commonly-used-l3)
137. [Kubernetes Q117: How do you implement autoscaling based on custom metrics (eg queue depth) [L2]](#scenario-137-kubernetes-q117-how-do-you-implement-autoscaling-based-on-custom-metrics-eg-queue-depth-l2)
138. [Kubernetes Q118: A pod is being scheduled and then immediately evicted Whats happening [L2]](#scenario-138-kubernetes-q118-a-pod-is-being-scheduled-and-then-immediately-evicted-whats-happening-l2)
139. [Kubernetes Q119: How do you implement multi-cluster service discovery so Service A in cluster 1 can call Service B in cluster 2 [L3]](#scenario-139-kubernetes-q119-how-do-you-implement-multi-cluster-service-discovery-so-service-a-in-cluster-1-can-call-service-b-in-cluster-2-l3)
140. [Kubernetes Q120: What is a pause container and why is it in every pod [L2]](#scenario-140-kubernetes-q120-what-is-a-pause-container-and-why-is-it-in-every-pod-l2)
141. [Kubernetes Q121: What is imagePullPolicy Always vs IfNotPresent [L2]](#scenario-141-kubernetes-q121-what-is-imagepullpolicy-always-vs-ifnotpresent-l2)
142. [Kubernetes Q122: How do you configure resource requests and limits for init containers [L2]](#scenario-142-kubernetes-q122-how-do-you-configure-resource-requests-and-limits-for-init-containers-l2)
143. [Kubernetes Q123: What is a projected volume in Kubernetes [L3]](#scenario-143-kubernetes-q123-what-is-a-projected-volume-in-kubernetes-l3)
144. [Kubernetes Q124: How do you check what labels are on a node [L2]](#scenario-144-kubernetes-q124-how-do-you-check-what-labels-are-on-a-node-l2)
145. [Kubernetes Q125: What is the downward API in Kubernetes [L2]](#scenario-145-kubernetes-q125-what-is-the-downward-api-in-kubernetes-l2)
146. [Kubernetes Q126: How do you handle pod disruptions during Kubernetes version upgrades [L3]](#scenario-146-kubernetes-q126-how-do-you-handle-pod-disruptions-during-kubernetes-version-upgrades-l3)
147. [Kubernetes Q127: What is kubectl diff [L2]](#scenario-147-kubernetes-q127-what-is-kubectl-diff-l2)
148. [Kubernetes Q128: How do you enforce that all pods in a namespace must have resource limits [L2]](#scenario-148-kubernetes-q128-how-do-you-enforce-that-all-pods-in-a-namespace-must-have-resource-limits-l2)
149. [Kubernetes Q129: What is Vertical Pod Autoscaler (VPA) and when should you use it vs HPA [L3]](#scenario-149-kubernetes-q129-what-is-vertical-pod-autoscaler-vpa-and-when-should-you-use-it-vs-hpa-l3)
150. [Kubernetes Q130: How do you temporarily expose a service from a remote cluster to your local machine for debugging [L2]](#scenario-150-kubernetes-q130-how-do-you-temporarily-expose-a-service-from-a-remote-cluster-to-your-local-machine-for-debugging-l2)
151. [Kubernetes Q131: What is kubectl top and what does it need to work [L2]](#scenario-151-kubernetes-q131-what-is-kubectl-top-and-what-does-it-need-to-work-l2)
152. [Kubernetes Q132: How does Kubernetes handle pod security with the Pod Security Standards [L3]](#scenario-152-kubernetes-q132-how-does-kubernetes-handle-pod-security-with-the-pod-security-standards-l3)
153. [Kubernetes Q133: What is a Kubernetes lease [L2]](#scenario-153-kubernetes-q133-what-is-a-kubernetes-lease-l2)
154. [Kubernetes Q134: How do you get events for a specific namespace sorted by time [L2]](#scenario-154-kubernetes-q134-how-do-you-get-events-for-a-specific-namespace-sorted-by-time-l2)
155. [Kubernetes Q135: What is a Service Mesh and when is the complexity worth it [L3]](#scenario-155-kubernetes-q135-what-is-a-service-mesh-and-when-is-the-complexity-worth-it-l3)
156. [Kubernetes Q136: How do you forward all logs from a Kubernetes pod to Elasticsearch [L2]](#scenario-156-kubernetes-q136-how-do-you-forward-all-logs-from-a-kubernetes-pod-to-elasticsearch-l2)
157. [Kubernetes Q137: What is eBPF and how is it used in Kubernetes networking [L3]](#scenario-157-kubernetes-q137-what-is-ebpf-and-how-is-it-used-in-kubernetes-networking-l3)
158. [Kubernetes Q138: What happens when you delete a namespace that has resources in it [L2]](#scenario-158-kubernetes-q138-what-happens-when-you-delete-a-namespace-that-has-resources-in-it-l2)
159. [Kubernetes Q139: How do you run a pod on the control plane node [L2]](#scenario-159-kubernetes-q139-how-do-you-run-a-pod-on-the-control-plane-node-l2)
160. [Kubernetes Q140: Explain Kubernetes Network Policies default behavior and why it can be a security risk [L3]](#scenario-160-kubernetes-q140-explain-kubernetes-network-policies-default-behavior-and-why-it-can-be-a-security-risk-l3)
161. [Kubernetes Q141: What is a sidecar container pattern [L2]](#scenario-161-kubernetes-q141-what-is-a-sidecar-container-pattern-l2)
162. [Kubernetes Q142: How do you pass the pods own name to the app running inside it [L2]](#scenario-162-kubernetes-q142-how-do-you-pass-the-pods-own-name-to-the-app-running-inside-it-l2)
163. [Kubernetes Q143: What is Kubernetes Federation and is it still recommended [L3]](#scenario-163-kubernetes-q143-what-is-kubernetes-federation-and-is-it-still-recommended-l3)
164. [Kubernetes Q144: How do you create a self-signed TLS certificate for an Ingress [L2]](#scenario-164-kubernetes-q144-how-do-you-create-a-self-signed-tls-certificate-for-an-ingress-l2)
165. [Kubernetes Q145: What is an Admission Controller and how does Kubernetes use them [L3]](#scenario-165-kubernetes-q145-what-is-an-admission-controller-and-how-does-kubernetes-use-them-l3)
166. [Kubernetes Q146: How do you retrieve only the logs from a specific container in a pod that has multiple containers [L2]](#scenario-166-kubernetes-q146-how-do-you-retrieve-only-the-logs-from-a-specific-container-in-a-pod-that-has-multiple-containers-l2)
167. [Kubernetes Q147: What is kubectl apply --prune [L2]](#scenario-167-kubernetes-q147-what-is-kubectl-apply-prune-l2)
168. [Kubernetes Q148: How do you implement an egress gateway in a Kubernetes cluster [L3]](#scenario-168-kubernetes-q148-how-do-you-implement-an-egress-gateway-in-a-kubernetes-cluster-l3)
169. [Kubernetes Q149: What is the significance of the --dry-run=server flag vs --dry-run=client [L2]](#scenario-169-kubernetes-q149-what-is-the-significance-of-the-dry-run-server-flag-vs-dry-run-client-l2)
170. [Kubernetes Q150: How do you implement a global rate limiter for all requests to your services in Kubernetes [L3]](#scenario-170-kubernetes-q150-how-do-you-implement-a-global-rate-limiter-for-all-requests-to-your-services-in-kubernetes-l3)
171. [Fine-Grained Service Discovery Across 1,000+ Microservices Using Envoy & Istio](#scenario-171-fine-grained-service-discovery-across-1-000-microservices-using-envoy-istio)
172. [Runtime Network Security Enforcement with eBPF & Cilium vs. Traditional iptables CNIs](#scenario-172-runtime-network-security-enforcement-with-ebpf-cilium-vs-traditional-iptables-cnis)
173. [Advanced Kubernetes Health Probe Engineering: Detecting Deep Business Logic Deadlocks Beyond HTTP 200](#scenario-173-advanced-kubernetes-health-probe-engineering-detecting-deep-business-logic-deadlocks-beyond-http-200)
174. [Kubernetes HPA Refuses to Scale Despite Prometheus CPU > 80%: Cloud & Metrics Server Triage](#scenario-174-kubernetes-hpa-refuses-to-scale-despite-prometheus-cpu-80-cloud-metrics-server-triage)
175. [Production Kubernetes Version Lifecycle & Deprecation Audit Strategy](#scenario-175-production-kubernetes-version-lifecycle-deprecation-audit-strategy)
176. [Production Incident Walkthrough: Bad ConfigMap Feature Flag & Rapid Rollback](#scenario-176-production-incident-walkthrough-bad-configmap-feature-flag-rapid-rollback)
177. [Intermittent 502 Bad Gateway via Ingress Under High Traffic — Systematic Triage](#scenario-177-intermittent-502-bad-gateway-via-ingress-under-high-traffic-systematic-triage)
178. [Preventing Bad Configurations from Reaching Production in CI/CD Pipelines](#scenario-178-preventing-bad-configurations-from-reaching-production-in-ci-cd-pipelines)
179. [Helm Deployment Fails Due to Insufficient Cluster Resources — SRE Triage](#scenario-179-helm-deployment-fails-due-to-insufficient-cluster-resources-sre-triage)
180. [Enterprise Internal Helm Chart Distribution Using OCI Registries (ECR/Harbor)](#scenario-180-enterprise-internal-helm-chart-distribution-using-oci-registries-ecr-harbor)
181. [Automated Helm Chart Testing: Linting, Unit Testing & Ephemeral Kind Verification](#scenario-181-automated-helm-chart-testing-linting-unit-testing-ephemeral-kind-verification)
182. [Multi-Cloud Docker Workload Architecture: Build Once, Deploy Portably](#scenario-182-multi-cloud-docker-workload-architecture-build-once-deploy-portably)
183. [Integrating Jenkins with Docker, Kubernetes, and AWS (ECR/EKS) for Cloud-Native CI/CD](#scenario-183-integrating-jenkins-with-docker-kubernetes-and-aws-ecr-eks-for-cloud-native-ci-cd)
184. [Designing High Availability (HA) & Resilient Autoscaling in Production Kubernetes](#scenario-184-designing-high-availability-ha-resilient-autoscaling-in-production-kubernetes)
185. [Kubernetes Pod Restart Mechanics: Container Restarts vs Pod Evictions & Lifecycle Hooks](#scenario-185-kubernetes-pod-restart-mechanics-container-restarts-vs-pod-evictions-lifecycle-hooks)
186. [Why Deployments Succeed at the Orchestrator Level Yet Users Still See 5xx Errors](#scenario-186-why-deployments-succeed-at-the-orchestrator-level-yet-users-still-see-5xx-errors)

---

## 🛠️ Production Scenarios & First-Person Runbooks

<a id="scenario-1-zero-downtime-amazon-eks-minor-multi-version-upgrade-v1-34-v1-36"></a>
### 1. Zero-Downtime Amazon EKS Minor & Multi-Version Upgrade (v1.34 → v1.36+)

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Amazon EKS & Upgrades` | **Type:** `Classic Scenario`

**Tags:** `Kubernetes` `Amazon EKS` `Zero Downtime` `Cluster Upgrade` `PDB`

> **Interview Question:**  
> *"Walk me through how you upgraded an Amazon EKS cluster from Kubernetes v1.34 to v1.36 and even after v1.37 without downtime."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
In one of my projects, we had a customer-facing application running as microservices on Amazon EKS, and we had a requirement to upgrade Kubernetes from v1.34 to v1.36. Since it was Production, we couldn't afford application downtime, so we followed a proper upgrade runbook.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Pre-checks & Compatibility Verification

Before touching the cluster, perform a complete pre-flight check of deprecated APIs and dependencies:

- **EKS Upgrade Insights:** Checked automated AWS insights for deprecated APIs and cluster readiness.
- **Deprecated Kubernetes APIs:** Audited manifests and Helm charts using API deprecation tools (e.g., Pluto / kubent).
- **Helm chart and application compatibility:** Verified all third-party charts, CRDs, and controllers support the target version.
- **Core Add-ons:** Checked compatibility matrices for VPC CNI, CoreDNS, and kube-proxy for target versions.
- **AWS Load Balancer Controller:** Verified controller version, IAM policies (IRSA), and TargetGroupBinding CRDs.
- **PDBs and replica counts:** Verified PodDisruptionBudgets and replica counts (≥ 2) across all critical services.
- **Monitoring components:** Ensured Prometheus, Grafana, and CloudWatch were operational to capture real-time telemetry.

> 💡 **Pro-Tip / Highlight:** Once the pre-checks were clean, we tested the complete upgrade in a lower environment first (Dev → Staging/UAT). We never started directly with Production.

##### 2️⃣ Upgrade One Version at a Time

Kubernetes minor version upgrades must be performed sequentially. You cannot skip minor versions:

- For each version, I first upgraded the **EKS control plane** (AWS handles the multi-AZ control plane upgrade without API downtime).
- Once the control plane was healthy, I validated the cluster and then upgraded the required **EKS add-ons** (VPC CNI, CoreDNS, kube-proxy, EBS CSI driver).

**Execution Flow:** `v1.34` ➔ `v1.35` ➔ `Validate` ➔ `v1.36` ➔ `Validate` ➔ `v1.37`

##### 3️⃣ Replace Worker Nodes (Blue/Green Node Groups)

For worker nodes, we didn't immediately terminate the existing node group:

- We created a **new managed node group** with an EKS-optimized AMI compatible with the new Kubernetes version.
- Once the new nodes joined the cluster and showed `Ready`, we started moving the workloads.
- **Cordon old node:** Marked the node unschedulable so new pods were only scheduled on the new node group.
- **Drain one node at a time:** `kubectl drain &lt;node&gt; --ignore-daemonsets --delete-emptydir-data`.
- We didn't drain everything together — we moved workloads gradually to maintain application availability.

**Execution Flow:** `Cordon old node` ➔ `Drain one node at a time` ➔ `Pods move to new nodes`

##### 4️⃣ How Did We Avoid Downtime?

Zero downtime was guaranteed because our critical microservices were engineered for High Availability:

- ✅ **Multiple Replicas:** Every critical service had at least 2–3 replicas running across nodes.
- ✅ **PodDisruptionBudgets (PDBs):** Enforced minAvailable / maxUnavailable so the API server blocked evictions that would breach availability.
- ✅ **Readiness Probes & Graceful Shutdown:** Traffic was only routed once newly scheduled pods passed readiness checks; preStop hooks allowed in-flight requests to complete.
- ✅ **Multi-AZ Workload Distribution:** Topology spread constraints ensured pods were distributed evenly across multiple Availability Zones.

> 💡 **Pro-Tip / Highlight:** So even when one node was being drained, healthy Pods on other nodes continued serving customer traffic without interruption.

##### 5️⃣ Continuous Telemetry & Monitoring

Using CloudWatch and Prometheus/Grafana, continuously monitored throughout the upgrade:

- **Node Health:** Memory/CPU pressure and kubelet status.
- **Pod Restarts:** Monitored CrashLoopBackOff and restart counts.
- **Pending Pods:** Detected scheduling bottlenecks or resource exhaustion.
- **CPU and Memory:** Monitored cluster-wide headroom and OOM warnings.
- **ALB Target Health:** Confirmed targets remained healthy in AWS Target Groups.
- **Application Latency:** Verified p95/p99 response times did not degrade.
- **5xx HTTP Errors:** Monitored error rates to confirm zero dropped requests.

##### 6️⃣ Validate Before Removing Anything

Once all workloads were running on the new node group, we didn't immediately remove the old one:

- We performed smoke testing and validated critical application flows under real traffic.
- Once everything was verified stable, we cleanly deleted the old node group.
- Then we repeated the same process for subsequent minor version bumps (e.g. v1.34 → v1.35 → v1.36 → v1.37).

**Execution Flow:** `Customer Login` ➔ `Account Information` ➔ `API Connectivity` ➔ `Transaction Processing`

#### 🎯 Key Architectural Takeaway
> Zero downtime wasn't achieved just because we carefully upgraded EKS. It was possible because the application was already designed for high availability with multiple replicas, PDBs, readiness probes, Multi-AZ deployment, and controlled node draining.

#### ⏱️ 60-Second Elevator Pitch Summary

- Conducted rigorous pre-checks: EKS Upgrade Insights, API deprecations (Pluto), add-on compatibility, and lower-environment testing.
- Upgraded strictly one minor version at a time (v1.34 → v1.35 → v1.36 → v1.37): control plane first, followed by managed add-ons.
- Implemented blue/green worker node replacement with new EKS-optimized AMI node groups; cordoned and drained nodes one-by-one.
- Guaranteed zero downtime via HA safeguards: replica counts ≥ 2, PodDisruptionBudgets, readiness probes, preStop hooks, and multi-AZ spread.
- Monitored CloudWatch/Grafana telemetry (5xx errors, latency, pending pods, ALB target health) throughout.
- Executed critical business flow smoke tests before safely decommissioning old node groups.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-2-pod-stuck-in-pending-scheduler-resource-triage"></a>
### 2. Pod Stuck in Pending — Scheduler & Resource Triage

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Workloads & Scheduling` | **Type:** `Core K8s Scenario`

**Tags:** `Kubernetes` `Scheduler` `kubectl describe` `Resource Limits` `PVC`

> **Interview Question:**  
> *"Pod is stuck in Pending — what would you check?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
A Pod stuck in Pending means the kube-scheduler cannot find a node that meets all the pod's constraints, or volume mounting / admission controllers are blocked. My primary tool is immediately 'kubectl describe pod '.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Inspect Scheduler Events First

Run `kubectl describe pod &lt;pod-name&gt;` and look directly at the **Events** section at the bottom:

- **FailedScheduling message:** The scheduler explains in plain English why each node was rejected (e.g. `0/6 nodes available: 3 Insufficient cpu, 3 node(s) had untolerated taint`).
- **FailedMount / FailedAttachVolume:** Storage subsystem is blocked attempting to attach or format an EBS/NFS volume.

##### 2️⃣ Root Cause 1: Insufficient Node Capacity (CPU/Memory)

Scheduler calculates fit based on **requests**, not actual usage:

- Run `kubectl describe nodes | grep -A 8 'Allocated resources'` to see node allocation percentages.
- If pods have huge CPU/memory requests (e.g. `cpu: 4` on 4-core nodes), no single node can fit them.
- **Fix:** Adjust application requests, or ensure Cluster Autoscaler / Karpenter is provisioning new nodes.

##### 3️⃣ Root Cause 2: Node Selectors, Affinity & Taints

Filter constraints that eliminate eligible nodes:

- `spec.nodeSelector`: Label typo (e.g. `disk: ssd` when nodes are labeled `disktype: ssd`).
- `nodeAffinity` / `podAntiAffinity`: Hard anti-affinity (`requiredDuringSchedulingIgnoredDuringExecution`) preventing pods from running on the same node/AZ.
- **Taints without Tolerations:** Nodes tainted with `dedicated=gpu:NoSchedule` or uncordoned maintenance taints.

##### 4️⃣ Root Cause 3: Unbound PVCs & Missing Config

Check persistent storage and required configuration:

- Check PVC state: `kubectl get pvc`. If `Pending`, check StorageClass and CSI provisioner.
- **Volume Multi-AZ Trap:** In AWS, an EBS volume lives in `us-east-1a`. If nodes in `us-east-1a` are full, scheduler cannot place the pod in `us-east-1b`.
- Check referenced ConfigMaps/Secrets: If a volume references a non-existent ConfigMap, pod cannot start.

#### 🎯 Key Architectural Takeaway
> Always run 'kubectl describe pod' and read the Scheduler Events. Differentiate resource request starvation (fit calculation) from affinity/taint rules and AZ-locked EBS volume binding.

#### ⏱️ 60-Second Elevator Pitch Summary

- Run 'kubectl describe pod ' and read the Events section: FailedScheduling tells you why.
- Check Resources: verify node allocated requests ('kubectl describe nodes') vs pod spec.resources.requests.
- Check Constraints: nodeSelector, nodeAffinity, and taints/tolerations that block placement.
- Check Storage: verify PVC status ('kubectl get pvc') - check if volume is locked to a different AWS AZ.
- Verify Cluster Autoscaler / Karpenter logs to ensure nodes are actively spinning up.
- Fix: Tune requests, correct label selectors, add tolerations, or trigger node autoscaling.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-3-pod-in-crashloopbackoff-diagnostic-root-cause-workflow"></a>
### 3. Pod in CrashLoopBackOff — Diagnostic & Root Cause Workflow

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Core K8s Scenario`

**Tags:** `Kubernetes` `CrashLoopBackOff` `OOMKilled` `kubectl logs` `Probes`

> **Interview Question:**  
> *"Pod is in CrashLoopBackOff — how would you troubleshoot?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
CrashLoopBackOff means the container started, crashed, and Kubernetes is backing off before restarting it. My troubleshooting sequence always follows: Exit Code analysis -> Previous container logs -> Liveness probe evaluation.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Inspect Exit Code via kubectl describe

Run `kubectl describe pod &lt;pod-name&gt;` and examine the `Last State: Terminated` block:

- **Exit Code 137 (OOMKilled):** `Reason: OOMKilled`. The Linux kernel OOM Killer terminated the container for exceeding its `limits.memory`. Fix: bump memory limit or fix memory leak.
- **Exit Code 1 or 255 (App Error):** Application code crashed (uncaught exception, syntax error, missing environment variable, failed DB connection).
- **Exit Code 127 (Command Not Found):** Container CMD/ENTRYPOINT executable does not exist inside the image.
- **Exit Code 143 (SIGTERM):** Graceful shutdown signal was received, often from a failing liveness probe or preStop hook.
- **Exit Code 0 (Completed):** Container finished its task and exited normally, but pod restartPolicy is `Always` instead of `OnFailure/Never`.

##### 2️⃣ Fetch Previous Container Logs (--previous)

Because the crashing container has already terminated, standard logs may be empty or only show startup lines:

- `kubectl logs &lt;pod-name&gt; --previous`: **The golden command** — reads the stdout/stderr from the crashed instance before it restarted.
- If multi-container pod: `kubectl logs &lt;pod-name&gt; -c &lt;container-name&gt; --previous`.
- Look at the last 20 lines for stack traces, database connection timeouts, or missing config keys.

##### 3️⃣ Check Liveness & Startup Probes

A misconfigured liveness probe will actively kill a healthy container during slow startup:

- Check events for: `Liveness probe failed: HTTP probe failed with statuscode: 500`.
- If an app takes 45 seconds to initialize but `initialDelaySeconds` is 10, Kubernetes kills it repeatedly!
- **Fix:** Implement a `startupProbe` with generous failureThreshold, giving the app time to start before liveness checks engage.

##### 4️⃣ Interactive Debugging with Ephemeral Containers

If logs are silent and container crashes instantly:

- Override entrypoint in a local manifest: change command to `['sh', '-c', 'sleep 3600']` to keep container alive, then `kubectl exec -it` to inspect files and environment.
- Use `kubectl debug -it &lt;pod-name&gt; --image=busybox --target=&lt;container&gt;` to attach an ephemeral debugging container sharing the process namespace.

#### 🎯 Key Architectural Takeaway
> Look at the Exit Code first (137 = OOM, 1 = App crash). Use 'kubectl logs --previous' to capture the crash stack trace. Verify startupProbe isn't killing slow-starting applications.

#### ⏱️ 60-Second Elevator Pitch Summary

- Run 'kubectl describe pod ' -> inspect Last State: Exit Code (137 = OOMKill, 1 = code exception, 127 = binary missing).
- Run 'kubectl logs  --previous' to retrieve the stack trace from the crashed instance.
- If Exit Code 137: Increase spec.resources.limits.memory or profile memory leak.
- Check Probes: Verify livenessProbe isn't timing out during slow boots; add startupProbe.
- If container crashes instantly: Override command with 'sleep 3600' or attach ephemeral container via 'kubectl debug'.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-4-pod-running-but-service-inaccessible-end-to-end-network-approach"></a>
### 4. Pod Running but Service Inaccessible — End-to-End Network Approach

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Services & Networking` | **Type:** `Core K8s Scenario`

**Tags:** `Kubernetes` `Service` `Endpoints` `CoreDNS` `NetworkPolicy`

> **Interview Question:**  
> *"Pod is running but Service isn't accessible — what's your approach?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
When a Pod is Running but its Service isn't accessible, I isolate the failure across 5 discrete layers: Service Selector/Endpoints -> Port mapping -> Readiness probes -> Cluster DNS -> NetworkPolicies.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Step 1: Check Endpoints & EndpointSlices (The #1 Culprit)

Services do not route to Pods directly; they route to Endpoints populated by label matching:

- Run: `kubectl get endpoints &lt;service-name&gt;` and `kubectl get endpointslices -l kubernetes.io/service-name=&lt;service-name&gt;`.
- **If Endpoints is &lt;none&gt;:** The Service's `spec.selector` does NOT match the Pod's labels! Compare `kubectl get svc &lt;svc&gt; -o yaml` against `kubectl get pods --show-labels`.
- Common typos: `app: web` in service vs `app: frontend` or `tier: web` on pod.

##### 2️⃣ Step 2: Check Pod Readiness Probes

A pod can be 'Running' but failing its readiness probe:

- Check `kubectl get pods`: Is the pod showing `0/1 READY`?
- If a readiness probe fails, Kubernetes **removes the pod's IP from the Service Endpoints** to prevent traffic from hitting unready pods.
- Check `kubectl describe pod` for readiness probe failures.

##### 3️⃣ Step 3: Verify Port & TargetPort Mapping

Confirm the port translation pipeline:

- `port: 80`: The port clients connect to on the Service ClusterIP.
- `targetPort: 8080`: The port the container is actually listening on.
- Verify the app is listening inside the container: `kubectl exec -it &lt;pod&gt; -- ss -tulpn` or `curl localhost:8080`.
- If `targetPort` is a named port (e.g. `http`), verify `containerPort: 8080` in pod spec matches the name.

##### 4️⃣ Step 4: Test In-Cluster DNS & NetworkPolicies

Spin up a temporary debug pod inside the cluster:

- `kubectl run curl-test --rm -it --image=curlimages/curl -- sh`
- Test by IP first: `curl -Iv http://&lt;ClusterIP&gt;:&lt;port&gt;`. If IP works, problem is CoreDNS resolution.
- Test by FQDN: `curl -Iv http://&lt;service&gt;.&lt;namespace&gt;.svc.cluster.local:&lt;port&gt;`.
- **Check NetworkPolicies:** Run `kubectl get netpol`. If an ingress default-deny NetworkPolicy exists on the namespace without an allow rule for the client, all traffic is dropped silently at the CNI layer.

#### 🎯 Key Architectural Takeaway
> Always check 'kubectl get endpoints ' first. If endpoints are empty, it's either a label selector mismatch or a failing readiness probe. Then test port mappings and NetworkPolicies.

#### ⏱️ 60-Second Elevator Pitch Summary

- Check Endpoints: 'kubectl get endpoints '. If empty, Service selector doesn't match Pod labels.
- Check Readiness: If pod is 0/1 READY, failing readiness probe stripped pod IP from endpoints.
- Check Port Translation: Verify service port -> targetPort matches the port the container is listening on (ss -tulpn).
- Test via curl container: Test ClusterIP directly, then FQDN (service.ns.svc.cluster.local) to rule out CoreDNS.
- Check NetworkPolicies: 'kubectl get netpol -n ' - verify ingress allow rules exist between namespaces.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-5-new-deployment-breaks-production-fast-safe-rollback"></a>
### 5. New Deployment Breaks Production — Fast & Safe Rollback

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Deployment Strategies & Rollbacks` | **Type:** `Incident Recovery`

**Tags:** `Kubernetes` `Deployment` `Rollback` `GitOps` `ArgoCD`

> **Interview Question:**  
> *"New deployment breaks production — how would you rollback?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
When a new deployment causes production degradation, the priority is mean time to recovery (MTTR). The rollback path depends on whether you run imperative deployments or declarative GitOps.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Immediate Imperative Rollback (kubectl rollout undo)

If using native Kubernetes deployments:

- `kubectl rollout undo deployment/&lt;deployment-name&gt; -n &lt;ns&gt;`: Instantly rolls back to the previous revision.
- `kubectl rollout status deployment/&lt;deployment-name&gt;`: Monitor the rollback progress in real-time.
- To target a specific revision: `kubectl rollout history deployment/&lt;name&gt;` followed by `kubectl rollout undo deployment/&lt;name&gt; --to-revision=3`.
- **How it works under the hood:** Kubernetes points the Deployment back to the previous healthy `ReplicaSet`, scaling it up while scaling down the broken ReplicaSet.

##### 2️⃣ GitOps Rollback (ArgoCD / Flux Reality)

In GitOps, manual kubectl rollouts will be reverted by self-healing:

- **The GitOps Trap:** If you run `kubectl rollout undo` while ArgoCD has `auto-sync` + `self-heal` enabled, ArgoCD will detect drift and immediately re-deploy the broken version!
- **Proper GitOps Rollback:** Run `git revert HEAD &amp;&amp; git push origin main` in the manifest repository. ArgoCD syncs and restores the previous commit cleanly.
- **Emergency Fast-Path:** In ArgoCD UI/CLI, click **Disable Auto-Sync**, roll back revision, then fix Git repository.

##### 3️⃣ The Database Migration Trap

Can code be safely rolled back if database schema migrated?

- If the release included destructive database schema migrations (e.g. dropped a column or renamed a table), rolling back application code will crash the previous version because old code expects the old schema.
- **The Rule:** Production deployments must follow **Expand and Contract** database migrations (additive changes first, deploy code, cleanup in next release).
- If a migration broke backward compatibility: Coordinate with DBAs to apply a compensating forward migration or restore DB snapshot before reverting code.

##### 4️⃣ Post-Incident & Blameless Post-Mortem

Preventing the same failure in future releases:

- Conduct blameless post-mortem: Why didn't automated CI tests or staging catch this?
- Implement **Canary Deployments with Argo Rollouts or Flagger**: Route 5% traffic to canary; automatically abort if 5xx errors spike without human intervention.
- Add automated smoke tests and readiness probe validation.

#### 🎯 Key Architectural Takeaway
> Know your deployment mechanism: In pure K8s, use 'kubectl rollout undo'; in GitOps (ArgoCD), disable auto-sync or 'git revert' to prevent self-heal fighting. Never do destructive DB migrations in single-step releases.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate action: Run 'kubectl rollout undo deployment/' to revert to previous ReplicaSet.
- If GitOps (ArgoCD/Flux): Disable auto-sync immediately or 'git revert HEAD && git push' so self-heal doesn't re-break it.
- Database check: Verify if DB migrations ran. If additive, rollback is safe. If destructive, apply compensating migration.
- Verify recovery: Monitor 'kubectl rollout status', ALB 5xx metrics, and application logs.
- Post-mortem: Implement progressive delivery (Argo Rollouts/Canary) with automatic metric-based rollback.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-6-ci-cd-pipeline-succeeds-but-new-version-isn-t-deployed-debugging"></a>
### 6. CI/CD Pipeline Succeeds but New Version Isn't Deployed — Debugging

**Level:** `Senior DevOps / SRE` | **Category:** `CI/CD` • `Pipelines & Delivery` | **Type:** `Pipeline Triage`

**Tags:** `CI/CD` `Docker` `Image Tagging` `GitOps` `Kubernetes`

> **Interview Question:**  
> *"Pipeline succeeds but the new version isn't deployed — how would you debug?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
When a CI/CD pipeline shows green but production is unchanged, the issue lies in artifact immutability, deployment trigger conditions, or GitOps reconciliation gaps.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Verify What is Actually Running in Production

Start by inspecting the live cluster/server before checking pipeline scripts:

- Run: `kubectl get deployment &lt;app&gt; -o jsonpath='{.spec.template.spec.containers[0].image}'`.
- Check the image tag and digest. Does it match the newly built Git commit SHA?
- Hit the application's version endpoint: `curl https://app.example.com/version`.

##### 2️⃣ The ':latest' Tag & imagePullPolicy Trap

The single most common root cause in container CI/CD:

- If the pipeline pushes `myapp:latest` and the Kubernetes Deployment manifest says `image: myapp:latest` with `imagePullPolicy: IfNotPresent`:
- Kubernetes checks if a tag named `latest` exists locally on the node. If yes, it **never pulls the new image from the registry!**
- Furthermore, Kubernetes detects no change in the Deployment manifest (the image string is still `myapp:latest`), so it triggers **zero rollout!**
- **Fix:** Always use immutable image tags based on Git SHA or semantic release (e.g. `myapp:sha-7f3a9b2`).

##### 3️⃣ Pipeline Step Conditions & Environment Mismatch

Audit pipeline execution steps:

- **Skipped Deploy Step:** Did the build/test job succeed, but the deploy job was skipped because of a condition like `if: github.ref == 'refs/heads/main'` when building a feature branch?
- **Target Environment Mismatch:** Did the pipeline deploy to Staging instead of Production due to environment variable configuration?
- **Manual Approval Gate:** Is the pipeline waiting on manual approval in GitHub Actions Environments / GitLab Protected Environments?

##### 4️⃣ GitOps Manifest Repo & Controller Audit

If using a separate manifest repository (ArgoCD / Flux):

- Did the CI pipeline successfully commit and push the updated image tag to the config repo? (Check git credentials and branch protection rules).
- Check ArgoCD sync status: Is the application in `OutOfSync` or `Sync Failed` state? Is auto-sync paused?
- Check for Kubernetes manifest validation failure (e.g. invalid YAML or unaccepted CPU limit).

#### 🎯 Key Architectural Takeaway
> Check the live running image tag first. Avoid mutable ':latest' tags that bypass k8s rollouts. Verify pipeline conditions, approval gates, and GitOps manifest commit chains.

#### ⏱️ 60-Second Elevator Pitch Summary

- Verify running container image: 'kubectl get deploy  -o jsonpath={..image}'.
- Check image tagging: Avoid ':latest' with 'imagePullPolicy: IfNotPresent' which ignores new image pushes.
- Audit CI logs: Ensure the deploy job actually executed and was not skipped by branch/tag conditions.
- Check GitOps repo: Verify CI successfully pushed new image tag commit to the manifest repository.
- Check ArgoCD/Flux: Inspect sync status, controller errors, or paused auto-sync.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-7-design-a-high-availability-cloud-infrastructure-for-millions-of-requests-day"></a>
### 7. Design a High-Availability Cloud Infrastructure for Millions of Requests/Day

**Level:** `Staff / Principal SRE` | **Category:** `System Design` • `Cloud Architecture & Scalability` | **Type:** `Premium Architecture`

**Tags:** `System Design` `AWS` `EKS` `Architecture` `Aurora`

> **Interview Question:**  
> *"Design a highly available, production-grade cloud infrastructure for a microservices application handling millions of requests per day. Explain your choices around networking, load balancing, autoscaling, databases, observability, security, and disaster recovery."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
To support millions of daily requests with 99.99% availability, the architecture is designed around multi-AZ redundancy, zero single points of failure, decoupling of state, automated progressive scaling, and zero-trust security.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Networking & Edge Load Balancing

Multi-layered ingress and defense-in-depth perimeter:

- **Edge Acceleration & Perimeter:** Amazon CloudFront for global content delivery, SSL termination, and static caching, paired with **AWS WAF** (OWASP Top 10 rules, rate-limiting, bot control) and **AWS Shield** for DDoS protection.
- **VPC Topology:** Multi-AZ VPC spanning 3 Availability Zones (AZs) with three subnet tiers: Public Subnets (ALB, NAT Gateways), Private Subnets (EKS compute nodes), and Isolated Database Subnets (no internet route).
- **Load Balancing Layer:** Public Application Load Balancer (ALB) distributing traffic across EKS worker nodes, handing off to an in-cluster Ingress Controller (NGINX or AWS Load Balancer Controller) using IP target mode (bypasses kube-proxy hop directly to pod IPs via AWS VPC CNI).

##### 2️⃣ Compute Layer & Elastic Autoscaling

High-density, cost-effective container orchestration:

- **Managed Control Plane:** Amazon EKS spanning 3 AZs for resilient API availability.
- **Fast Node Provisioning (Karpenter):** Replace slow Cluster Autoscaler with **Karpenter** for just-in-time EC2 provisioning (graviton/spot/on-demand mix) in <45 seconds based on pending pod requests.
- **Multi-Tier Workload Autoscaling:** Horizontal Pod Autoscaler (HPA) coupled with **KEDA** (Kubernetes Event-driven Autoscaling) to scale on custom business metrics (e.g. SQS queue backlog, Redis queue length, or HTTP RPS) before CPU saturates.
- **HA Scheduling Safeguards:** `topologySpreadConstraints` across AZs and `PodDisruptionBudgets (PDBs)` to guarantee minimum healthy replicas during rolling updates or node drains.

##### 3️⃣ Databases, Caching & Data Layer

Decoupling hot reads, writes, and cache tiers:

- **Relational Database:** **Amazon Aurora PostgreSQL (Multi-AZ)** with a primary writer instance and auto-scaling Read Replicas across AZs. Aurora provides storage auto-replication across 6 storage nodes and sub-30s failover.
- **Caching Tier:** **Amazon ElastiCache for Redis (Cluster Mode)** with multi-AZ replication. Implements cache-aside pattern for hot user queries and session state, absorbing 80%+ read traffic from the database.
- **NoSQL / Event Streaming:** Amazon DynamoDB with on-demand capacity for ultra-low latency key-value lookups; Amazon MSK (Managed Kafka) or SQS for asynchronous event-driven inter-service messaging.

##### 4️⃣ Zero-Trust Security & Secrets

Hardening at rest, in transit, and across identities:

- **Workload Identity:** IAM Roles for Service Accounts (IRSA) — pods assume scoped AWS IAM roles without long-lived credentials.
- **Secrets Management:** AWS Secrets Manager integrated via **External Secrets Operator (ESO)** with automatic password rotation; etcd encryption-at-rest via AWS KMS.
- **Network Segmentation:** Calico/Cilium NetworkPolicies enforcing default-deny ingress/egress between microservice namespaces.
- **Runtime Auditing:** Falco runtime threat detection + AWS GuardDuty EKS Protection.

##### 5️⃣ Full-Stack Observability & Disaster Recovery

Unified telemetry and business continuity:

- **Distributed Telemetry:** OpenTelemetry collector agents forwarding metrics to Prometheus/Grafana, logs to Loki/OpenSearch, and traces to Tempo/Jaeger with W3C tracecontext headers.
- **SLO/SLI Alerting:** Multi-window burn rate alerts sent to PagerDuty based on error budget depletion.
- **Disaster Recovery (RPO < 1m, RTO < 15m):** Route 53 DNS failover with health checks. Aurora Global Databases replicating across a secondary AWS region with automated cross-region S3 backup replication.

#### 🎯 Key Architectural Takeaway
> Achieving scale and 99.99% availability isn't about bigger machines: it's CloudFront/WAF edge caching, 3-AZ VPC with Karpenter + KEDA autoscaling, Aurora Multi-AZ with Redis caching, and zero-trust IAM with OpenTelemetry correlation.

#### ⏱️ 60-Second Elevator Pitch Summary

- Edge & Ingress: CloudFront + WAF + Shield -> ALB with IP Target Mode into multi-AZ EKS cluster.
- Compute & Autoscaling: EKS with Karpenter for sub-minute node scaling; HPA + KEDA for event-driven pod scaling.
- Data Tier: Multi-AZ Aurora PostgreSQL with auto-scaling read replicas + ElastiCache Redis cluster for 80%+ cache hit ratio.
- Security: IRSA for pod IAM, External Secrets Operator, Cilium NetworkPolicies (default-deny), KMS encryption.
- Observability: OpenTelemetry pipeline -> Prometheus, Loki, Tempo with trace_id correlation across all logs.
- DR: Pilot light / warm standby in secondary region with Aurora Global Database and Route 53 health-check failover.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-8-kubernetes-cluster-intermittent-pod-failures-high-latency-systematic-troubleshooting"></a>
### 8. Kubernetes Cluster Intermittent Pod Failures & High Latency — Systematic Troubleshooting

**Level:** `Staff / Principal SRE` | **Category:** `Kubernetes` • `Cluster Reliability & Diagnostics` | **Type:** `Core Diagnostics`

**Tags:** `Kubernetes` `CoreDNS` `Latency` `Troubleshooting` `Conntrack`

> **Interview Question:**  
> *"Your Kubernetes cluster is experiencing intermittent pod failures and high latency. How would you troubleshoot it systematically? Explain how you would investigate pods, nodes, networking, resource limits, probes, scheduling, DNS, and application metrics."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
Intermittent failures and latency spikes in Kubernetes are notoriously elusive because they rarely show up as hard crashes. I isolate them using a layered, full-stack diagnostic model: Nodes -> Pods & Limits -> CoreDNS -> Networking/CNI -> Application Probes.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Layer 1: Node Health, Kernel & CPU Throttling

Inspect underlying host instances and container runtime:

- Run `kubectl get nodes`: Check for node conditions like `MemoryPressure`, `DiskPressure`, or `PIDPressure`.
- SSH into suspected nodes: check `dmesg -T` for kernel OOM-killer invocations, hardware errors, or TCP drops.
- **CPU Throttling Trap:** Check Prometheus metric `container_cpu_cfs_throttled_seconds_total`. Even when average node CPU is only 40%, strict pod `resources.limits.cpu` cause Linux CFS throttling, introducing random 200–500ms latency spikes!

##### 2️⃣ Layer 2: Pod Restarts, OOMKills & Exit Codes

Inspect container states across namespaces:

- `kubectl get pods -A --sort-by='.status.containerStatuses[0].restartCount'`: Identify flapping pods.
- `kubectl describe pod &lt;pod&gt;`: Check for `OOMKilled` (Exit Code 137).
- Retrieve stack trace from crashed container: `kubectl logs &lt;pod&gt; -c &lt;container&gt; --previous`.
- Check liveness probe thresholds: Are slow database calls causing the liveness probe to timeout and restart otherwise healthy pods?

##### 3️⃣ Layer 3: CoreDNS & The 'ndots:5' DNS Latency Trap

Intermittent 1-second latency spikes are almost always DNS issues:

- Check CoreDNS latency: `coredns_dns_request_duration_seconds` in Prometheus.
- **The ndots:5 Amplification Trap:** Default Kubernetes `/etc/resolv.conf` has `ndots:5`. For external domains (e.g. `api.stripe.com`), the pod queries 4 internal search domains (`.default.svc...`) before querying the public domain, multiplying DNS queries by 5x and overloading CoreDNS!
- **Fix:** Deploy **NodeLocal DNSCache** daemonset on all nodes, or append a trailing dot (`api.stripe.com.`) in application configs.

##### 4️⃣ Layer 4: CNI, IP Exhaustion & Conntrack Table

Subtle networking drops at the host and CNI level:

- **VPC CNI IP Exhaustion:** In AWS, check if worker node subnets ran out of free private IP addresses, preventing newly scheduled pods from obtaining an ENI secondary IP.
- **Linux Conntrack Saturation:** High-traffic microservices exhaust the Linux connection tracking table (`nf_conntrack_max`). Once full, the kernel silently drops new TCP SYN packets! Check with `dmesg -T | grep 'table full, dropping packet'`.
- **kube-proxy Sync Latency:** Check if iptables rule processing is stalling packet forwarding.

#### 🎯 Key Architectural Takeaway
> Intermittent K8s latency is usually not pod crashes: it's Linux CFS CPU throttling, CoreDNS ndots:5 search domain multiplication, or Linux nf_conntrack table exhaustion. Deploy NodeLocal DNSCache and tune CPU limits.

#### ⏱️ 60-Second Elevator Pitch Summary

- Layer 1 (Node): Check node pressure flags (Memory/DiskPressure) and CFS CPU throttling (container_cpu_cfs_throttled_seconds_total).
- Layer 2 (Pods): Sort pods by restart count; inspect 'kubectl logs --previous' for OOMKilled (Exit Code 137).
- Layer 3 (DNS): Inspect CoreDNS metrics; mitigate ndots:5 search domain amplification using NodeLocal DNSCache.
- Layer 4 (Network): Verify VPC CNI subnet IP availability; check 'dmesg' for nf_conntrack table exhaustion drops.
- Layer 5 (Probes): Ensure liveness probes have sufficient timeout/initialDelay to avoid killing slow-starting pods.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-9-deployment-vs-statefulset-vs-daemonset-architectural-decision-matrix"></a>
### 9. Deployment vs StatefulSet vs DaemonSet — Architectural Decision Matrix

**Level:** `Senior DevOps / DevSecOps` | **Category:** `Kubernetes` • `Core Workload Primitives` | **Type:** `Core Architecture`

**Tags:** `Kubernetes` `Workloads` `Deployment` `StatefulSet` `DaemonSet`

> **Interview Question:**  
> *"In Kubernetes, what is the difference between Deployment, StatefulSet, and DaemonSet?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
In production, selecting the wrong workload controller leads to data corruption, deployment deadlocks, or wasted compute. I categorize them by statefulness, pod identity, and placement topology.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Deployment: Stateless, Interchangeable Workloads

Designed for stateless microservices, web apps, and API gateways where pods are ephemeral and interchangeable:

- **Pod Identity:** Pods receive random hash suffixes (e.g. `api-7d58f97b6b-4kx9l`). Any pod can serve any request.
- **Storage:** Typically stateless. If mounting PersistentVolumes (PV), all replicas share the same ReadWriteMany (NFS/EFS) volume or ephemeral emptyDir.
- **Rollouts:** Controlled by ReplicaSets with declarative RollingUpdate or Recreate strategies.

##### 2️⃣ StatefulSet: Ordered, Stateful & Identity-Preserving Workloads

Designed for databases, distributed storage, and clustered systems (Kafka, Elasticsearch, PostgreSQL, Redis Cluster, ZooKeeper):

- **Predictable Identity:** Pods get deterministic, zero-indexed ordinal names (e.g. `kafka-0`, `kafka-1`, `kafka-2`).
- **Headless Service & DNS:** Uses `clusterIP: None` so each pod receives a distinct DNS entry (e.g. `kafka-0.kafka-headless.prod.svc.cluster.local`) essential for leader election and cluster peering.
- **volumeClaimTemplates:** Each replica dynamically provisions its own dedicated, persistent disk that survives pod recreation or rescheduling.
- **Ordered Deployment & Termination:** Deploys sequentially (0 ➔ 1 ➔ 2) and shuts down in reverse order to preserve quorum.

##### 3️⃣ DaemonSet: Exactly One Pod Per Node Workloads

Ensures that a copy of the pod runs on every matching node in the cluster:

- **Node-Bound Placement:** Pods are automatically scheduled when a new node joins the cluster and garbage collected when the node is decommissioned.
- **Primary Use Cases:** Cluster observability agents (Datadog, Fluentbit, Prometheus Node Exporter), networking CNI plugins (Calico, AWS VPC CNI, Cilium), and security runtimes (Falco, Sysdig).
- **Tolerations:** DaemonSets typically tolerate `node.kubernetes.io/unschedulable` and master/control-plane taints to monitor every physical host.

#### 🎯 Key Architectural Takeaway
> Use Deployments for interchangeable stateless APIs; StatefulSets for quorum-based, disk-backed databases needing deterministic DNS and storage; and DaemonSets for infrastructure agents (CNI, logging, metrics, security) that must live on every physical node.

#### ⏱️ 60-Second Elevator Pitch Summary

- Deployment: Stateless apps (APIs, web apps); random pod hashes; shared or no persistent disk; rolling updates.
- StatefulSet: Clustered databases (Kafka, Postgres, Redis); deterministic ordinal names (app-0, app-1); dedicated volumeClaimTemplates; headless service DNS.
- DaemonSet: Infrastructure agents (Fluentbit, Node Exporter, Cilium, Falco); runs exactly one pod per node automatically as nodes scale.
- Pro-Tip: Never run databases on Deployments with ReadWriteOnce EBS volumes—pods will fail to remount across nodes due to multi-attach errors.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-10-ingress-controller-end-to-end-osi-layer-7-traffic-flow"></a>
### 10. Ingress Controller — End-to-End OSI Layer 7 Traffic Flow

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Networking & Ingress` | **Type:** `Core Networking`

**Tags:** `Kubernetes` `Ingress` `Ingress Controller` `NGINX` `ALB`

> **Interview Question:**  
> *"Explain Ingress Controller. What is the difference between Ingress resource, Ingress Controller, and Service?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
Candidates often confuse the declarative Ingress YAML with the actual reverse proxy software. Ingress requires two components: the declarative API rule and an active controller running in the cluster.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ The Three Discrete Layers (Resource vs Controller vs Service)

Understanding the separation of concerns:

- 📄 **Ingress Resource:** A Kubernetes API object (YAML) that defines routing rules: hostnames, URL path prefixes (/api, /auth), and TLS certificate secrets.
- ⚙️ **Ingress Controller:** The actual running proxy application (Ingress-NGINX, Traefik, AWS Load Balancer Controller, or Azure AGIC) that reads Ingress resources and dynamically reconfigures its routing table.
- 🔌 **Kubernetes Service:** An internal ClusterIP abstraction that provides a stable virtual IP and tracks healthy Pod IPs via Endpoints/EndpointSlices.

##### 2️⃣ End-to-End Traffic Flow (Internet to Application)

How an HTTP request traverses the layers:

- 1. User accesses `https://api.example.com/checkout`.
- 2. DNS resolves to the Cloud Load Balancer (AWS ALB, Azure App Gateway, or NLB).
- 3. Load balancer forwards traffic to the Ingress Controller Pods running in the cluster.
- 4. The Ingress Controller evaluates its in-memory routing table: matches host `api.example.com` and path `/checkout`.
- 5. **The Performance Secret:** Modern ingress controllers (like NGINX) bypass the `kube-proxy` ClusterIP NAT hop and route directly to the backend Pod IP discovered via the Kubernetes Endpoints API.

**Execution Flow:** `Client DNS Request` ➔ `Cloud Load Balancer (ALB/AGIC)` ➔ `Ingress Controller Pods` ➔ `Bypass kube-proxy (Endpoints)` ➔ `Target Pod IP`

##### 3️⃣ Production Add-Ons: TLS & Security

Essential components paired with Ingress Controllers in enterprise setups:

- **Cert-Manager:** Automates Let's Encrypt / enterprise PKI SSL certificate issuance and renewal into Kubernetes TLS secrets.
- **IngressClass:** Decouples cluster from specific controllers, allowing multiple ingress controllers (e.g. internal vs public) in one cluster.
- **WAF & Rate Limiting:** Ingress controllers inject annotations for rate-limiting (`limit-rps`), IP whitelisting, and WAF protection.

#### 🎯 Key Architectural Takeaway
> An Ingress Resource is just a passive config manifest. Without an active Ingress Controller pod listening to the Kubernetes API, your ingress rules do nothing. High-performance controllers route directly to Pod IPs via EndpointSlices rather than bouncing through kube-proxy.

#### ⏱️ 60-Second Elevator Pitch Summary

- Ingress Resource is the YAML routing specification (hosts, paths, TLS secrets).
- Ingress Controller is the active reverse proxy daemon (NGINX, Traefik, Envoy, AWS ALB Controller) executing the rules.
- Service is the backend abstraction; the Ingress Controller watches Service Endpoints to stream traffic directly to container IPs.
- Client -> Cloud LB -> Ingress Controller Pod -> Evaluates Host/Path Rules -> Direct connection to target Pod IP.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-11-troubleshooting-imagepullbackoff-errimagepull-4-root-causes"></a>
### 11. Troubleshooting ImagePullBackOff & ErrImagePull — 4 Root Causes

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Troubleshooting & Pod Lifecycle` | **Type:** `Core Troubleshooting`

**Tags:** `Kubernetes` `ImagePullBackOff` `Docker` `ECR` `ACR`

> **Interview Question:**  
> *"How do you troubleshoot ImagePullBackOff?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
ImagePullBackOff means kubelet tried to pull the container image from the registry, failed, and is backing off exponentially. My troubleshooting begins by running 'kubectl describe pod ' and reading the exact container runtime error in the Events.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Inspect Describe Events for the Exact Error String

Run `kubectl describe pod &lt;pod&gt; -n &lt;ns&gt;` and check the bottom Events section:

- `Error: ImagePullBackOff` is preceded by `Failed to pull image &lt;image-name&gt;: rpc error: code = NotFound / Unknown`.
- The exact error string immediately categorizes the failure into one of 4 root causes.

##### 2️⃣ Root Cause 1: Image Name or Tag Typo / Non-Existent Image

Error: `manifest unknown` or `repository does not exist`:

- Verify the repository URL, image name, and tag in `spec.containers[0].image`.
- Check if the CI/CD pipeline actually pushed the image to ECR/ACR/DockerHub, or if the build job failed before the push stage.
- Check for architecture mismatch (e.g. pushed ARM64 image while nodes are AMD64).

##### 3️⃣ Root Cause 2: Authentication & Missing imagePullSecrets

Error: `401 Unauthorized` or `403 Forbidden / Access Denied`:

- Private registries require Kubernetes credentials. Check if the Pod or its ServiceAccount references `imagePullSecrets`.
- Check secret existence: `kubectl get secret &lt;secret-name&gt; -o yaml`.
- In AWS EKS: Verify node IAM instance profile has `AmazonEC2ContainerRegistryReadOnly` or IRSA is configured.
- In Azure AKS: Verify AKS kubelet identity has `AcrPull` role assignment on the Azure Container Registry (ACR).

##### 4️⃣ Root Cause 3 & 4: Rate Limiting (429) & Network / Egress Blocks

Error: `toomanyrequests: You have reached your pull rate limit` or `i/o timeout`:

- **Docker Hub 429:** Free tier limits anonymous pulls to 100 per 6 hours. Solution: Mirror images to private ECR/ACR or add authenticated Docker Hub pull secret.
- **Network / DNS Timeout:** Worker nodes in private subnets cannot reach external registries if NAT Gateway is down, security group blocks outbound 443, or CoreDNS fails to resolve registry domain.
- **Quick Test from Node:** SSH into worker node or run a debug pod: `crictl pull &lt;image-name&gt;` to test pull directly.

#### 🎯 Key Architectural Takeaway
> Read the exact error in 'kubectl describe pod': 'manifest unknown' = image tag typo or unpushed image; '401/403' = missing imagePullSecret or IAM/AcrPull role; '429' = Docker Hub rate limit; 'i/o timeout' = NAT Gateway or egress firewall block.

#### ⏱️ 60-Second Elevator Pitch Summary

- Run 'kubectl describe pod ' and examine the Events message.
- Case 1: 'manifest unknown' -> Image tag typo or CI/CD failed to push image.
- Case 2: '401 Unauthorized' -> Missing imagePullSecret in pod spec or node lacks ECR/ACR IAM pull permissions.
- Case 3: '429 Too Many Requests' -> Docker Hub rate limit; switch to private registry mirror (ECR/ACR).
- Case 4: 'Connection timeout' -> Node in private subnet has no egress route to NAT Gateway or Security Group blocks 443 outbound.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-12-kubernetes-pod-logs-events-senior-diagnostic-command-toolkit"></a>
### 12. Kubernetes Pod Logs & Events — Senior Diagnostic Command Toolkit

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Observability & CLI Tooling` | **Type:** `Core Diagnostics`

**Tags:** `Kubernetes` `kubectl logs` `kubectl events` `Debugging` `Stern`

> **Interview Question:**  
> *"How do you check Kubernetes pod logs and events?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
Checking logs and events is fundamental, but in large-scale production with multi-container pods, crashing containers, and thousands of events, using standard 'kubectl logs' alone is insufficient.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Mastering Pod Logs (Crashing, Multi-Container, Live Stream)

Essential commands for container log inspection:

- `kubectl logs &lt;pod-name&gt; -f`: Real-time stream (follow) of container stdout/stderr.
- `kubectl logs &lt;pod-name&gt; --previous`: **The crashed container command** — inspects logs of the container instance that just crashed before restarting.
- `kubectl logs &lt;pod-name&gt; -c &lt;container-name&gt;`: Explicitly targets a container in multi-container pods (e.g. Istio sidecar vs app container).
- `kubectl logs deployment/&lt;app&gt; --all-containers=true --tail=50`: Triage all pods in a deployment simultaneously.
- `stern &lt;app-prefix&gt; -n prod --since 15m`: Cross-pod color-coded log aggregator that tails all pods matching a regex even as pods restart.

##### 2️⃣ Mastering Cluster Events (Sorting, Filtering & Warning Triage)

Events explain WHY pods are failing, evicted, or unschedulable:

- `kubectl get events -n &lt;ns&gt; --sort-by='.metadata.creationTimestamp'`: Chronological event timeline of recent cluster occurrences.
- `kubectl get events --field-selector type=Warning -n &lt;ns&gt;`: Filters noise to show only warnings (FailedScheduling, Unhealthy, FailedMount, BackOff).
- `kubectl events -n &lt;ns&gt;`: Modern K8s 1.23+ dedicated command with clean human-readable table formatting.
- `kubectl get events --field-selector involvedObject.name=&lt;pod-name&gt;`: Filters events tied strictly to a specific pod.

##### 3️⃣ Deep Debugging: Ephemeral Containers & Node Logs

When container logs are silent or container won't run:

- `kubectl debug -it &lt;pod-name&gt; --image=nicolaka/netshoot --target=&lt;app&gt;`: Attaches an ephemeral container with tcpdump, curl, and dig sharing the pod's network and process namespace.
- **Node kubelet logs:** If the node itself is unresponsive: `journalctl -u kubelet -e` on the host.

#### 🎯 Key Architectural Takeaway
> Always use '--previous' to catch the smoking gun of a crashed container. Filter events by 'type=Warning' to eliminate noise, and leverage 'stern' for multi-pod regex log streaming across autoscaling pods.

#### ⏱️ 60-Second Elevator Pitch Summary

- Current logs: 'kubectl logs  -f' (add -c for specific container).
- Crashed logs: 'kubectl logs  --previous' to see crash stack trace.
- Multi-pod streaming: Use 'stern ' for live tailing across all replicas.
- Events: 'kubectl get events -n  --sort-by=.metadata.creationTimestamp' and filter by 'type=Warning'.
- Zero-downtime debugging: 'kubectl debug' to attach ephemeral netshoot container with diagnostics tools.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-13-configuring-cpu-memory-requests-and-limits-qos-classes-throttling"></a>
### 13. Configuring CPU & Memory Requests and Limits — QoS Classes & Throttling

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Resource Management & Capacity` | **Type:** `Resource Architecture`

**Tags:** `Kubernetes` `Requests` `Limits` `QoS` `OOMKilled`

> **Interview Question:**  
> *"How do you configure CPU and memory requests/limits?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
Configuring requests and limits is not guess-work. Requests determine where the scheduler places pods; limits determine when the Linux kernel throttles or terminates them. Setting them incorrectly causes either cluster starvation or silent application slowness.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Requests vs Limits Mechanics

Understanding how the control plane and Linux kernel treat them differently:

- **spec.resources.requests:** The *guaranteed reservation*. The `kube-scheduler` calculates node placement strictly based on sum of requests vs node capacity. If a node has 4 cores and 3.8 cores are requested, no new pod requesting 500m can fit.
- **spec.resources.limits:** The *hard ceiling*. Enforced by Linux kernel cgroups. How the kernel responds depends on the resource type:

- ⏱️ **CPU (Compressible):** When a pod hits its CPU limit, it is NOT killed. The kernel CFS quota throttles CPU cycles, causing latency spikes and slow response times.
- 💥 **Memory (Incompressible):** Memory cannot be throttled. When a container exceeds its memory limit, the Linux kernel OOM Killer terminates it immediately (Exit Code 137, OOMKilled).

##### 2️⃣ The 3 Kubernetes Quality of Service (QoS) Classes

Kubernetes automatically assigns QoS based on requests and limits:

- **1. Guaranteed (Highest Priority):** `requests.cpu == limits.cpu` AND `requests.memory == limits.memory` for all containers. Last to be evicted when node is under resource pressure. Best for critical databases and core services.
- **2. Burstable (Medium Priority):** Requests are less than limits (e.g. request 500m, limit 2000m). Allowed to burst when extra node capacity exists. Standard for most web APIs.
- **3. BestEffort (Lowest Priority):** No requests and no limits set. First to be killed instantly when a node experiences memory pressure.

##### 3️⃣ Production Right-Sizing Best Practices

How senior SREs avoid common traps:

- **Right-Sizing:** Use Prometheus historical p95 usage or Vertical Pod Autoscaler (VPA in recommendation mode) to base requests on actual p95 peak load + 20% headroom.
- **The CPU Limit Debate:** Many high-scale teams (Google, Uber) remove CPU limits on latency-sensitive Burstable services to prevent CFS throttle penalties during micro-bursts, relying on HPA to scale out.
- **Memory:** Always set memory limits equal or close to requests to prevent noisy neighbors from consuming all node RAM.

#### 🎯 Key Architectural Takeaway
> Requests are for scheduling (reservations); limits are for kernel enforcement. CPU is compressible (hits limit -> throttles); memory is incompressible (hits limit -> OOMKilled Exit 137). Set requests = limits on databases for Guaranteed QoS, and right-size requests to p95 peak usage.

#### ⏱️ 60-Second Elevator Pitch Summary

- Requests: Guaranteed minimum reserved by kube-scheduler; placement depends on it.
- Limits: Maximum ceiling enforced by cgroups.
- CPU behavior: Compressible -> throttled via CFS quota (app slows down, no crash).
- Memory behavior: Incompressible -> killed immediately by OOM Killer (Exit Code 137).
- QoS Classes: Guaranteed (requests == limits, safest), Burstable (requests < limits), BestEffort (no values, evicted first).
- Best practice: Right-size with VPA recommendation mode; always set memory limits.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-14-horizontal-pod-autoscaler-hpa-internals-algorithm-stabilization"></a>
### 14. Horizontal Pod Autoscaler (HPA) — Internals, Algorithm & Stabilization

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Autoscaling & Reliability` | **Type:** `Core Autoscaling`

**Tags:** `Kubernetes` `HPA` `Autoscaling` `Metrics Server` `Prometheus`

> **Interview Question:**  
> *"How does HPA work in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
HPA automatically scales the number of pod replicas in a Deployment or StatefulSet based on observed metrics like CPU, memory, or custom business metrics. It operates as a continuous reconciliation control loop inside kube-controller-manager.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Step 1: The Control Loop & Metrics Pipeline

How HPA gathers metrics every 15 seconds (default `--horizontal-pod-autoscaler-sync-period`):

- kubelet's embedded **cAdvisor** collects container CPU and memory usage from cgroups.
- **Metrics Server** scrapes kubelet summary APIs and aggregates resource usage in memory.
- The HPA controller queries `metrics.k8s.io` (or `custom.metrics.k8s.io` via Prometheus Adapter) for target pods.
- HPA calculates the average utilization against the pod's `spec.resources.requests` (not limits!).

**Execution Flow:** `kubelet (cAdvisor)` ➔ `Metrics Server` ➔ `metrics.k8s.io API` ➔ `HPA Controller` ➔ `Scale ReplicaSet`

##### 2️⃣ Step 2: The Exact Mathematical Formula

HPA executes this exact formula on every evaluation loop:

- `desiredReplicas = ceil[ currentReplicas * ( currentMetricValue / desiredMetricValue ) ]`
- **Concrete Example:** Current replicas = 3. Target CPU = 50%. Current CPU utilization = 80%.
- `desiredReplicas = ceil[ 3 * (80 / 50) ] = ceil[ 4.8 ] = 5 replicas.`
- **Tolerance Window:** If `currentMetricValue / desiredMetricValue` is within 10% (0.9 to 1.1), HPA does not scale to prevent flapping.

##### 3️⃣ Step 3: Flapping Prevention (Behavior) & KEDA for Events

Advanced production safeguards:

- **Scale-Down Stabilization Window:** Default 300s (5 minutes). HPA records the highest desired replica count over the last 5 minutes and waits before scaling down to prevent thrashing during momentary traffic dips.
- **HPA Behavior Spec:** Define custom scaleUp/scaleDown policies (e.g. max 100% scale up every 15s, max 10% scale down every minute).
- **KEDA (Kubernetes Event-driven Autoscaling):** For async workloads (SQS, Kafka, RabbitMQ), scaling on CPU is too slow. KEDA scales pods from 0 to N based on queue lag before CPU even moves.

#### 🎯 Key Architectural Takeaway
> HPA evaluates every 15s using `desiredReplicas = ceil[currentReplicas * (currentMetric / targetMetric)]`. Crucially, target CPU percentage is calculated against the pod's resource REQUESTS, not limits. Use stabilization windows to prevent flapping, and KEDA for event-driven queue scaling.

#### ⏱️ 60-Second Elevator Pitch Summary

- Continuous control loop running in kube-controller-manager (polls every 15s).
- Formula: desiredReplicas = ceil[ currentReplicas * (currentMetric / targetMetric) ].
- Golden Rule: CPU percentage is relative to resource REQUESTS (not limits!). If requests aren't set, HPA cannot calculate CPU utilization.
- Flapping prevention: Uses a 5-minute stabilization window for scale-down to absorb traffic dips.
- For event queues (Kafka, SQS, RabbitMQ): Use KEDA to autoscale on queue length before CPU spikes.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-15-troubleshooting-high-cpu-or-memory-usage-in-kubernetes"></a>
### 15. Troubleshooting High CPU or Memory Usage in Kubernetes

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Performance & Troubleshooting` | **Type:** `Performance Triage`

**Tags:** `Kubernetes` `CPU` `Memory` `kubectl top` `Profiling`

> **Interview Question:**  
> *"How would you troubleshoot high CPU or memory usage in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
When a high CPU or memory alert triggers in Kubernetes, my workflow moves top-down: Cluster/Node level -> Pod level -> Container level -> Application runtime profiling (Go pprof / Java jstack).

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Step 1: Isolate Affected Nodes and Pods

Identify where the saturation is concentrated:

- `kubectl top nodes`: Pinpoints if a single node is saturated or if the entire cluster is running out of headroom.
- `kubectl top pods -A --sort-by=cpu`: Instantly lists the top CPU-consuming pods across all namespaces.
- `kubectl top pods -A --sort-by=memory`: Instantly lists the top memory-consuming pods.
- Check if the pod is near its configured limit: compare `kubectl top pod &lt;pod&gt;` with `limits.cpu` / `limits.memory` in `kubectl describe pod`.

##### 2️⃣ Step 2: Differentiate CPU Spikes vs Memory Leaks

Analyze Grafana/Prometheus metrics to identify the pattern:

- **CPU Saturation:** Correlate with request rate (RPS) in ingress metrics. If RPS spiked 5x, it's legitimate traffic -> trigger HPA or scale replicas. If RPS is flat but CPU hit 100%, it's an infinite loop, thread lock, or regex catastrophic backtracking.
- **Memory Saturation:** Look at the memory graph over 24-48 hours. If memory steadily climbs in a sawtooth pattern and never drops after garbage collection, it is a **Memory Leak**.

##### 3️⃣ Step 3: Capture Runtime Telemetry (Don't Restart Blindly)

Capture the root cause before restarting the container:

- **Java / JVM:** Exec into pod or use ephemeral container: `jcmd &lt;pid&gt; GC.heap_dump /tmp/dump.hprof` and `jstack &lt;pid&gt;` to see locked threads.
- **Golang / Node.js:** Query the pprof endpoint: `curl http://localhost:6060/debug/pprof/profile?seconds=30` or heap profile.
- **Immediate Mitigation:** Once profiling is captured, scale replicas horizontally (HPA) or do a rolling restart (`kubectl rollout restart deployment/&lt;app&gt;`) to restore customer SLA.

#### 🎯 Key Architectural Takeaway
> Diagnose top-down: 'kubectl top nodes' -> 'kubectl top pods --sort-by=cpu/memory' -> Correlate with traffic RPS in Grafana. For CPU without traffic spikes, capture thread dumps; for climbing memory, capture heap dumps before restarting.

#### ⏱️ 60-Second Elevator Pitch Summary

- Identify culprit: 'kubectl top nodes' followed by 'kubectl top pods -A --sort-by=cpu / --sort-by=memory'.
- Correlate: Compare with Grafana request rate (RPS). Traffic spike = scale replicas. Flat traffic + 100% CPU = code deadlock/infinite loop.
- Memory triage: Check memory graph slope. Gradual steady climb without GC recovery = Memory Leak.
- Capture telemetry before restart: Run jstack/jcmd for Java, or pprof heap profiles for Go.
- Mitigate: Trigger HPA scale-out, or perform 'kubectl rollout restart' to buy time while developers fix the leak.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-16-kubernetes-resource-right-sizing-bin-packing-for-cost-reduction"></a>
### 16. Kubernetes Resource Right-Sizing & Bin-Packing for Cost Reduction

**Level:** `Senior DevOps / SRE` | **Category:** `FinOps & Cost` • `Container Efficiency` | **Type:** `Resource Optimization`

**Tags:** `Kubernetes` `FinOps` `Right-Sizing` `VPA` `Karpenter`

> **Interview Question:**  
> *"How would you use Kubernetes resource requests/limits to control costs?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
In Kubernetes, you pay for what you REQUEST, not what you use. If a developer requests 4 CPUs but the container only consumes 200m, the cloud provider bills you for 4 CPUs because the scheduler reserves the space. That gap is 'phantom spend'.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ The Phantom Spend Trap (Request vs Actual)

How over-provisioned requests trigger unneeded cloud node scale-outs:

- Kube-scheduler treats `requests` as hard commitments. If node capacity is 8 vCPU, and two pods request 4 vCPU each, the node is 100% allocated.
- Cluster Autoscaler / Karpenter is forced to provision a second EC2 node, even if the actual CPU utilization on the first node is only 5%!
- Result: Cloud bills double while clusters run at 10% actual hardware utilization.

##### 2️⃣ Automated Right-Sizing Tools (Goldilocks & VPA)

Data-driven sizing replacing developer guesswork:

- **Vertical Pod Autoscaler (VPA) in 'Off' (Recommendation) Mode:** Analyzes historical container usage and outputs exact recommended requests for CPU and memory.
- **Fairwinds Goldilocks:** Dashboard that consumes VPA recommendations and highlights over-provisioned workloads across namespaces.
- Set requests to the **p95 peak utilization + 15-20% headroom**, allowing pods to burst safely without blocking node scheduling.

##### 3️⃣ Dynamic Node Consolidation with Karpenter

Maximizing node packing density:

- Enable Karpenter `consolidationPolicy: WhenUnderutilized`.
- Karpenter constantly evaluates cluster bin-packing: if 3 nodes are 30% full, Karpenter cordons and drains one node, moves its pods onto the remaining nodes, and terminates the empty instance in real-time.

#### 🎯 Key Architectural Takeaway
> Cloud bills scale with Kubernetes CPU/memory REQUESTS, not actual utilization. Over-provisioned requests force autoscalers to launch expensive unnecessary nodes. Right-size requests to p95 usage using VPA recommendation mode and enable Karpenter node consolidation.

#### ⏱️ 60-Second Elevator Pitch Summary

- Problem: Cloud billing follows requests, not usage. Over-requested pods force the cluster to spin up empty, expensive nodes.
- Solution 1: Deploy VPA in recommendation mode + Goldilocks to discover real p95 CPU/memory usage.
- Solution 2: Adjust requests down to actual p95 load + 20% buffer, freeing up node capacity.
- Solution 3: Implement Karpenter with consolidation enabled—it automatically merges sparse nodes and terminates unneeded EC2 instances.
- Result: 30–50% reduction in cluster compute spend with zero impact on application performance.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-17-core-azure-cloud-services-in-enterprise-devops-devsecops"></a>
### 17. Core Azure Cloud Services in Enterprise DevOps & DevSecOps

**Level:** `Senior DevOps / DevSecOps` | **Category:** `Azure & Cloud` • `Cloud Architecture` | **Type:** `Enterprise Azure`

**Tags:** `Azure` `AKS` `Key Vault` `ACR` `VNet`

> **Interview Question:**  
> *"Other than APIs, what Azure services have you worked with?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
In enterprise DevOps environments, I interact daily across 6 foundational Azure service pillars: Identity & Access, Container Infrastructure, Networking, Security & Secrets, Observability, and Storage.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ The Core Enterprise Azure Portfolio

Services implemented in production architectures:

- **Azure Kubernetes Service (AKS):** Managed container orchestration with Azure CNI, managed node pools (Ubuntu/Azure Linux), and cluster autoscaler.
- **Azure Key Vault (AKV):** Hardware-backed HSM secret, certificate, and cryptographic key store; integrated with AKS via Azure Key Vault Secrets Provider / External Secrets Operator.
- **Azure Container Registry (ACR):** Enterprise private Docker registry with Geo-replication, automated vulnerability scanning (Microsoft Defender for Cloud), and task webhooks.
- **Microsoft Entra ID (formerly Azure AD) & Workload Identity:** Zero-trust identity; replaces long-lived credentials by federating Kubernetes ServiceAccounts directly to Azure Managed Identities.

##### 2️⃣ Networking & Observability Pillars

Network boundary and telemetry backbone:

- **Virtual Networks (VNet) & Network Security Groups (NSGs):** Subnet segmentation, peering with on-prem ExpressRoute, Private Endpoints for PaaS services, and NSG stateful packet filtering.
- **Azure Application Gateway & AGIC:** Layer 7 load balancer with integrated WAF v2 routing directly to AKS pods via Application Gateway Ingress Controller.
- **Azure Monitor & Log Analytics Workspaces:** Centralized telemetry sink collecting Kusto Query Language (KQL) logs from AKS container stdout, audit logs, and metrics alerts.

#### 🎯 Key Architectural Takeaway
> A modern Azure DevOps stack integrates AKS with Azure Key Vault for secrets, ACR for geo-replicated secure images, Entra ID Workload Identity for passwordless IAM, VNets with Private Endpoints for network isolation, and Log Analytics with KQL for telemetry.

#### ⏱️ 60-Second Elevator Pitch Summary

- Compute: Azure Kubernetes Service (AKS) with system and user node pools.
- Security & Secrets: Azure Key Vault integrated via Workload Identity (no hardcoded passwords).
- Registries: Azure Container Registry (ACR) with Defender vulnerability scanning and geo-replication.
- Networking: VNet, subnets, NSGs, Private Endpoints (no public IPs on DBs), and Azure Application Gateway (AGIC).
- Observability: Azure Monitor, Container Insights, and Log Analytics workspaces using KQL queries.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-18-azure-kubernetes-service-aks-architecture-deployment-troubleshooting"></a>
### 18. Azure Kubernetes Service (AKS) — Architecture, Deployment & Troubleshooting

**Level:** `Senior DevOps / SRE` | **Category:** `Azure & Cloud` • `Managed Kubernetes` | **Type:** `AKS Mastery`

**Tags:** `Azure` `AKS` `Azure CNI` `Workload Identity` `Container Insights`

> **Interview Question:**  
> *"Have you worked with Azure Kubernetes Service (AKS)? How would you deploy, monitor, and troubleshoot applications on AKS?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
Yes, extensively. AKS provides a managed control plane while offloading worker node management into System and User node pools. Managing AKS effectively requires understanding Azure CNI networking, Workload Identity, and Azure Container Insights.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ AKS Architecture & Networking Fundamentals

Control plane and networking choices:

- **Architecture:** Free/Standard tier managed control plane (etcd, API server managed by Microsoft); customer pays only for Virtual Machine Scale Set (VMSS) worker nodes grouped into System (CoreDNS, Metrics Server) and User (microservices) node pools.
- **Azure CNI vs Kubenet:** **Kubenet** uses internal pod overlay subnets (saves VNet IPs). **Azure CNI** gives every pod a real, routable IP from the Azure VNet subnet (lower latency, Direct VNet integration, but requires careful VNet CIDR sizing to avoid IP exhaustion).

##### 2️⃣ Deploying Applications to AKS

Modern automated deployment workflow:

- CI pipeline builds image and pushes to Azure Container Registry (ACR).
- Authenticates to AKS using **Microsoft Entra Workload Identity** (OIDC federation—no long-lived service principal client secrets stored in CI).
- CD pipeline (or ArgoCD GitOps) renders Helm templates and applies manifests to AKS.

**Execution Flow:** `Git Push` ➔ `GitHub Actions / Azure Pipelines` ➔ `ACR Docker Build` ➔ `Workload Identity Auth` ➔ `ArgoCD / Helm Sync` ➔ `AKS Cluster`

##### 3️⃣ Monitoring & Troubleshooting in AKS

Diagnostic workflow when issues occur:

- **Monitoring:** Enable **Azure Monitor Container Insights** with Managed Prometheus and Grafana. Run KQL queries in Log Analytics: `ContainerInventory | where ContainerStatus == 'Failed'`.
- **Troubleshooting Pods:** Standard `kubectl describe pod` and `kubectl logs --previous`.
- **AKS Diagnose and Solve Problems:** Native Azure Portal blade that runs automated diagnostic checks on node readiness, subnet IP allocation, and API server throttles.
- **Node Issues:** Check VMSS instance health in Azure Portal or run `az aks check-acr` to verify network connectivity between AKS nodes and ACR.

#### 🎯 Key Architectural Takeaway
> AKS architecture relies on System vs User node pools, Azure CNI for routable VNet networking, and Entra Workload Identity for secretless IAM. Monitor via Azure Monitor Container Insights (Prometheus/Grafana) and troubleshoot using kubectl alongside the Azure 'Diagnose and Solve' blade.

#### ⏱️ 60-Second Elevator Pitch Summary

- Architecture: Microsoft-managed control plane + VMSS worker node pools (System pool for core add-ons, User pool for workloads).
- Networking: Azure CNI gives pods native VNet IPs; requires large subnets to prevent IP exhaustion.
- Security: Entra Workload Identity federates Kubernetes ServiceAccounts with Azure Managed Identities (zero stored keys).
- Deployment: Azure Pipelines / GitHub Actions -> build & scan image -> push to ACR -> deploy via Helm / ArgoCD.
- Troubleshooting: Use 'kubectl describe/logs' for pod issues; 'az aks check-acr' for registry connectivity; and the Azure Portal 'Diagnose and Solve Problems' blade for node and network health.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-19-managing-secrets-securely-in-kubernetes-external-secrets-operator-eso"></a>
### 19. Managing Secrets Securely in Kubernetes — External Secrets Operator (ESO)

**Level:** `Senior DevOps / DevSecOps` | **Category:** `DevSecOps & Security` • `Secret Governance` | **Type:** `Secret Governance`

**Tags:** `Kubernetes` `Secrets` `External Secrets Operator` `AWS Secrets Manager` `Azure Key Vault`

> **Interview Question:**  
> *"How do you manage secrets securely in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
Kubernetes native Secret objects are only base64-encoded plain text—they are NOT encrypted by default. In enterprise production, we NEVER store secrets in Git or YAML files. We sync them dynamically using External Secrets Operator (ESO).

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ The Native Secret Trap & Plaintext in Git

Why native Kubernetes secrets fail enterprise compliance:

- Base64 encoding is not encryption: `echo 'cGFzc3dvcmQ=' | base64 -d` takes 1 millisecond.
- If developer commits a Secret manifest to Git, the secret is permanently recorded in Git history.
- In etcd, secrets are stored unencrypted unless **EncryptionAtRest** (using AWS KMS or Azure Key Vault KMS plugin) is explicitly enabled on the API server.

##### 2️⃣ Production Standard: External Secrets Operator (ESO)

How External Secrets Operator bridges cloud vaults to Kubernetes:

- **Source of Truth:** Secrets are maintained and rotated inside **AWS Secrets Manager**, **Azure Key Vault**, or **HashiCorp Vault**.
- **SecretStore CRD:** Configures authentication to the cloud vault using AWS IRSA or Azure Workload Identity (passwordless).
- **ExternalSecret CRD:** A safe Git-committable manifest that specifies which remote secret key to fetch and how often to refresh (e.g. `refreshInterval: 1h`).
- **Auto-Reconciliation:** ESO continuously syncs the remote secret into an in-cluster native Kubernetes Secret automatically.

**Execution Flow:** `Cloud Secret Store (AKV/AWS SM/Vault)` ➔ `SecretStore CRD (IAM/Workload Identity)` ➔ `ExternalSecret Manifest (Git Safe)` ➔ `Kubernetes Secret (Auto-Generated)`

##### 3️⃣ Secure Pod Consumption: Volume Mounts vs Env Vars

How the pod should consume the secret securely:

- **Avoid Plaintext Env Vars:** Environment variables (`envFrom.secretRef`) can leak into application error crash dumps, child process forks, and `/proc/&lt;pid&gt;/environ`.
- **Preferred Practice (Volume Mounts):** Mount secrets as file volumes into `/etc/secrets`. In Kubernetes, secret volumes are backed by **tmpfs (RAM only)**, meaning they are never written to physical node disk storage.

#### 🎯 Key Architectural Takeaway
> Never store secrets in Git. Keep the source of truth in AWS Secrets Manager, Azure Key Vault, or HashiCorp Vault. Use External Secrets Operator (ESO) with Workload Identity to sync them into in-memory Kubernetes Secrets, and mount them as tmpfs file volumes rather than environment variables.

#### ⏱️ 60-Second Elevator Pitch Summary

- Kubernetes Secrets are just base64 plain text; storing them in Git is a critical security vulnerability.
- Single Source of Truth: Store secrets in AWS Secrets Manager, Azure Key Vault, or HashiCorp Vault with automated rotation.
- Syncing Engine: Deploy External Secrets Operator (ESO). The Git repo only contains ExternalSecret manifests pointing to secret paths.
- Authentication: ESO authenticates to cloud vaults via AWS IRSA or Azure Workload Identity (zero hardcoded cloud keys).
- In-Pod consumption: Mount secrets as tmpfs RAM-backed file volumes instead of environment variables to prevent leak in crash logs.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-20-what-really-happens-under-the-hood-when-you-run-kubectl-apply-f-deployment-yaml"></a>
### 20. What Really Happens Under the Hood When You Run 'kubectl apply -f deployment.yaml'?

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Control Plane & Orchestration Internals` | **Type:** `Core Architecture`

**Tags:** `Kubernetes` `Architecture` `Control Plane` `kubectl apply` `API Server`

> **Interview Question:**  
> *"What really happens under the hood when you run 'kubectl apply -f deployment.yaml'? Walk me through the entire journey from client CLI to running container."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
Most Kubernetes engineers run 'kubectl apply' daily, but behind that single command lies an entire distributed orchestration engine. Kubernetes operates as a Desired State System: you declare the desired state, and a chain of independent control loops continuously works to reconcile reality to match that state.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Client-Side Processing & Validation (kubectl)

Before any network request reaches the cluster, kubectl performs client-side inspection:

- **Client-Side Validation:** kubectl verifies YAML syntax and checks resource fields against the locally cached OpenAPI / Swagger schema from the cluster (`~/.kube/cache/discovery`).
- **Three-Way Strategic Merge Patch:** Reads the `kubectl.kubernetes.io/last-applied-configuration` annotation, compares it with the live cluster state and the new local YAML, and computes a JSON Strategic Merge Patch.
- **HTTP REST Request:** Formats the payload into JSON and dispatches an HTTP POST/PATCH request to the API server: `POST /apis/apps/v1/namespaces/default/deployments` with TLS client certificates or OIDC Bearer tokens.

##### 2️⃣ API Server: Authentication, Authorization & Admission Control

The kube-apiserver is the single front door to the cluster. The request traverses 4 sequential filters:

- **1. Authentication:** Validates TLS cert, ServiceAccount token, or Entra/AWS IAM OIDC identity to establish the caller's username and groups.
- **2. Authorization (RBAC):** Evaluates ClusterRoles/RoleBindings to verify if the subject has `create` / `patch` permissions on `deployments` in the target namespace.
- **3. Mutating Admission Webhooks:** Plugins and webhooks (e.g. Istio sidecar injector, Vault agent injector) modify the object or set default values.
- **4. Schema Validation:** Enforces API schema rules, required fields, and immutability constraints.
- **5. Validating Admission Webhooks:** Webhooks (e.g. Kyverno, OPA Gatekeeper) run final compliance checks (e.g. enforcing non-root execution or image registry whitelisting) and reject invalid manifests.

**Execution Flow:** `Authentication (Who are you?)` ➔ `Authorization / RBAC (Can you do this?)` ➔ `Mutating Webhooks (Inject defaults)` ➔ `Object Schema Validation` ➔ `Validating Webhooks (Accept or Reject)`

##### 3️⃣ etcd: State Persistence & Consensus

The single source of truth commits the change:

- Once admission passes, kube-apiserver serializes the Deployment object into protocol buffers and writes it into **etcd** at key `/registry/deployments/default/my-app`.
- etcd commits the write across a quorum of nodes using the **Raft consensus algorithm**.
- The API server returns an HTTP `201 Created` or `200 OK` response back to the client CLI.
- **Important:** At this exact second, NO containers or pods exist yet! Only the *desired state* is recorded.

##### 4️⃣ Deployment Controller & ReplicaSet Controller (kube-controller-manager)

The control loops take over asynchronously:

- **Deployment Controller:** Watches the API server for Deployment changes. Detects the new Deployment and creates a child `ReplicaSet` object with pod template hash.
- **ReplicaSet Controller:** Detects the new ReplicaSet desiring e.g. 3 replicas. Compares desired replicas (3) with existing replicas (0).
- It issues 3 API requests to create 3 `Pod` objects. Crucially, these Pod objects have **no assigned node** (`spec.nodeName: ''`) and enter the **Pending** state.

**Execution Flow:** `API Server Watch Notification` ➔ `Deployment Controller` ➔ `Create ReplicaSet` ➔ `ReplicaSet Controller` ➔ `Create Unassigned Pods`

##### 5️⃣ kube-scheduler: Node Filtering & Scoring

Matching unbound pods to healthy worker nodes:

- **Watch Loop:** kube-scheduler continuously watches the API server for Pods where `spec.nodeName == ''`.
- **Phase 1 (Filtering / Predicates):** Eliminates ineligible nodes that lack sufficient CPU/memory requests, have untolerated taints, or fail nodeSelector / affinity constraints.
- **Phase 2 (Scoring / Priorities):** Scores remaining nodes based on image locality, topology spread, and resource fragmentation (least/most requested).
- **Binding:** Scheduler picks the highest-scoring node and sends a `Binding` API call to the API server, setting `spec.nodeName: 'worker-node-2'`.

##### 6️⃣ Kubelet & Container Runtime (CRI containerd)

The local node agent brings the container to life:

- **Kubelet Watch:** The kubelet daemon running on `worker-node-2` observes that a Pod has been assigned to its node name.
- **Container Runtime Interface (CRI):** Kubelet calls containerd via gRPC.
- **Image Pull:** containerd checks if the image exists in local cache; if not, pulls it from registry using node IAM credentials or imagePullSecrets.
- **Pod Sandbox Creation:** Kubelet instructs containerd to create the Pod Sandbox (pause container) establishing Linux namespaces (IPC, UTS, PID, Network).

##### 7️⃣ CNI Plugin: Network Namespace & Pod IP Allocation

Plumbing the container into the cluster network:

- Kubelet invokes the **CNI plugin** (AWS VPC CNI, Calico, Flannel, Cilium).
- The CNI creates a virtual ethernet pair (`veth`), moves one interface into the pod's network namespace as `eth0`, and connects the other interface to the host bridge or routing table.
- Allocates a dedicated Pod IP from the subnet CIDR and configures routing and MTU.
- Once networking is ready, containerd starts the application containers inside the pod sandbox.

##### 8️⃣ Readiness Probes & Service Endpoints Routing

Connecting the running pod to live client traffic:

- Kubelet continuously executes configured `startupProbe` and `readinessProbe`.
- Once probes return HTTP 200 / Success, kubelet reports pod status as `Ready` to the API server.
- The **Endpoints Controller** detects the Ready pod and appends the Pod IP to the Service's `Endpoints` / `EndpointSlices`.
- **kube-proxy** (or Cilium eBPF) on every node updates local iptables/IPVS rules, enabling load balancers and clients to route live traffic to the new pod!

#### 🎯 Key Architectural Takeaway
> Kubernetes is a Desired State System. Running 'kubectl apply' does not start containers directly; it commits desired state into etcd via the API server. An asynchronous chain of independent control loops (Deployment Controller -> ReplicaSet Controller -> Scheduler -> Kubelet -> CRI -> CNI -> Endpoints Controller) works continuously to bring physical reality to match your declared state.

#### ⏱️ 60-Second Elevator Pitch Summary

- 1. kubectl: Computes strategic 3-way merge patch and sends HTTP POST to kube-apiserver.
- 2. API Server: Authenticates caller, checks RBAC, runs Mutating/Validating admission webhooks, and writes desired state to etcd via Raft consensus.
- 3. Deployment & ReplicaSet Controllers: Detect the change via API watches and create unbound Pod definitions (spec.nodeName empty).
- 4. kube-scheduler: Filters nodes (predicates) and scores nodes (priorities), then writes a Binding object assigning the pod to a node.
- 5. Kubelet: Detects the assigned pod, instructs CRI (containerd) to create the pause container sandbox, and pulls the image.
- 6. CNI: Configures pod network namespace, veth pair, and assigns the Pod IP.
- 7. Service Ingress: Once readiness probes pass, Endpoints Controller adds Pod IP to Service Endpoints, and kube-proxy updates iptables/IPVS.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-21-kubernetes-q1-your-pod-is-stuck-in-pending-state-what-do-you-do-l1"></a>
### 21. Kubernetes Q1: Your pod is stuck in Pending state What do you do [L1]

**Level:** `Junior / Associate DevOps [L1]` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Core Fundamentals [L1]`

**Tags:** `Kubernetes` `Troubleshooting & Debugging` `L1` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your pod is stuck in `Pending` state. What do you do?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. The interviewer is testing: Basic Kubernetes debugging workflow.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

First run `kubectl describe pod ` and look at the **Events** section at the bottom. Common reasons for Pending:

- **No nodes with enough resources** — the node doesn't have enough CPU or memory. Check with `kubectl get nodes` and `kubectl describe node`.
- **No matching node selector or affinity** — the pod has a `nodeSelector` that doesn't match any node label.
- **Taints not tolerated** — the node has a taint the pod doesn't tolerate.

##### 2️⃣ Remediation & Permanent Safeguards

Fix based on the root cause shown in the events. ---

- **PVC not bound** — if the pod needs a volume, the PersistentVolumeClaim may be stuck.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: No nodes with enough resources — the node doesn't have enough CPU or memory. Check with kubectl get nodes and kubectl describe nod.

#### ⏱️ 60-Second Elevator Pitch Summary

- No nodes with enough resources — the node doesn't have enough CPU or memory. Check with kubectl g...
- No matching node selector or affinity — the pod has a nodeSelector that doesn't match any node la...
- Taints not tolerated — the node has a taint the pod doesn't tolerate.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-22-kubernetes-q2-a-pod-is-in-crashloopbackoff-how-do-you-debug-it-l1"></a>
### 22. Kubernetes Q2: A pod is in CrashLoopBackOff How do you debug it [L1]

**Level:** `Junior / Associate DevOps [L1]` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Core Fundamentals [L1]`

**Tags:** `Kubernetes` `Troubleshooting & Debugging` `L1` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A pod is in `CrashLoopBackOff`. How do you debug it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. The interviewer is testing: Log investigation and restart behavior understanding.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

`CrashLoopBackOff` means the container starts, crashes, and Kubernetes keeps restarting it with increasing delay.

- `kubectl logs ` — read the logs. If the container already restarted, use `kubectl logs  --previous` to get logs from the last crashed instance.
- `kubectl describe pod ` — check exit codes. Exit code `1` = app error, `137` = OOM killed, `139` = segfault.
- If logs are empty, the container may be crashing before writing anything — check the image and entrypoint command.

##### 2️⃣ Remediation & Permanent Safeguards

Steps: Common causes: app error on startup, wrong config/env vars, missing secrets, OOM. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl logs  — read the logs. If the container already restarted, use kubectl logs  --previous to get logs from the last crashed .

#### ⏱️ 60-Second Elevator Pitch Summary

- kubectl logs  — read the logs. If the container already restarted, use kubectl logs  --previous t...
- kubectl describe pod  — check exit codes. Exit code 1 = app error, 137 = OOM killed, 139 = segfault.
- If logs are empty, the container may be crashing before writing anything — check the image and en...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-23-kubernetes-q3-a-pod-shows-oomkilled-in-its-status-what-happened-and-how-do-you-fix-it-l2"></a>
### 23. Kubernetes Q3: A pod shows OOMKilled in its status What happened and how do you fix it [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Troubleshooting & Debugging` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A pod shows `OOMKilled` in its status. What happened and how do you fix it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. The interviewer is testing: Resource limits understanding.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

OOMKilled means the container exceeded its memory limit and the kernel killed it.

- Check current limits: `kubectl describe pod ` — look at the `Limits` section.
- Increase the memory limit in the deployment spec under `resources.limits.memory`.
- If you're unsure what the right value is, set a higher limit temporarily and monitor actual usage with `kubectl top pod `.

##### 2️⃣ Remediation & Permanent Safeguards

Fix: ---

- Long term: use VPA (Vertical Pod Autoscaler) to auto-tune resource requests and limits.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Check current limits: kubectl describe pod  — look at the Limits section..

#### ⏱️ 60-Second Elevator Pitch Summary

- Check current limits: kubectl describe pod  — look at the Limits section.
- Increase the memory limit in the deployment spec under resources.limits.memory.
- If you're unsure what the right value is, set a higher limit temporarily and monitor actual usage...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-24-kubernetes-q4-your-deployment-rollout-is-stuck-pods-from-the-new-version-arent-coming-up-but-old-ones-are-still-running-whats-happening-l2"></a>
### 24. Kubernetes Q4: Your deployment rollout is stuck Pods from the new version arent coming up but old ones are still running Whats happening [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Troubleshooting & Debugging` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your deployment rollout is stuck. Pods from the new version aren't coming up but old ones are still running. What's happening?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. The interviewer is testing: RollingUpdate strategy and rollout debugging.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

This is typical RollingUpdate behavior when new pods fail healthchecks.

- Liveness or readiness probe failing in the new version.
- New image has a bug and is crashing.
- Resource limits hit — new pods can't schedule.

##### 2️⃣ Remediation & Permanent Safeguards

Check: `kubectl rollout status deployment/` — it will show if it's stuck. Then `kubectl describe pod ` to see why new pods aren't ready. Common causes: To rollback immediately: `kubectl rollout undo deployment/` To investigate without rolling back, describe the new failing pods and check logs. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Liveness or readiness probe failing in the new version..

#### ⏱️ 60-Second Elevator Pitch Summary

- Liveness or readiness probe failing in the new version.
- New image has a bug and is crashing.
- Resource limits hit — new pods can't schedule.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-25-kubernetes-q5-a-pod-is-running-but-your-app-is-not-reachable-via-the-service-what-do-you-check-l2"></a>
### 25. Kubernetes Q5: A pod is Running but your app is not reachable via the Service What do you check [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Troubleshooting & Debugging` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A pod is `Running` but your app is not reachable via the Service. What do you check?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. The interviewer is testing: Service-to-pod connectivity debugging.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

---

- **Check pod labels vs service selector** — `kubectl describe service ` shows the selector. `kubectl get pod --show-labels` shows pod labels. They must match exactly.
- **Check endpoints** — `kubectl get endpoints `. If it shows ``, the selector doesn't match any pod.
- **Check if the pod is Ready** — even if Running, if the readiness probe fails, the pod is removed from endpoints.

##### 2️⃣ Remediation & Permanent Safeguards

Execute the resolution runbook and verify workload health:

- **Check the port mapping** — service `targetPort` must match the container's listening port.
- **Test from inside the cluster** — `kubectl exec -it  -- curl :` to isolate if it's a network policy or external routing issue.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Check pod labels vs service selector — kubectl describe service  shows the selector. kubectl get pod --show-labels shows pod label.

#### ⏱️ 60-Second Elevator Pitch Summary

- Check pod labels vs service selector — kubectl describe service  shows the selector. kubectl get ...
- Check endpoints — kubectl get endpoints . If it shows , the selector doesn't match any pod.
- Check if the pod is Ready — even if Running, if the readiness probe fails, the pod is removed fro...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-26-kubernetes-q6-a-node-in-your-cluster-shows-notready-your-team-is-panicking-because-several-services-are-on-it-whats-your-action-plan-l3"></a>
### 26. Kubernetes Q6: A node in your cluster shows NotReady Your team is panicking because several services are on it Whats your action plan [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Troubleshooting & Debugging` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A node in your cluster shows `NotReady`. Your team is panicking because several services are on it. What's your action plan?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. The interviewer is testing: Incident response, node troubleshooting, pod eviction understanding.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

---

- **Don't panic — check if pods already rescheduled.** Kubernetes evicts pods from NotReady nodes after `pod-eviction-timeout` (default 5 min). Check `kubectl get pods -A -o wide | grep `.
- **Cordon the node** — `kubectl cordon ` prevents new pods from scheduling there while you investigate.
- **SSH into the node** and check:
- `systemctl status kubelet` — is kubelet running?
- `journalctl -u kubelet -n 100` — kubelet logs.

##### 2️⃣ Remediation & Permanent Safeguards

Execute the resolution runbook and verify workload health:

- Disk space: `df -h`. Full disk is a common cause.
- Memory: `free -m`.
- **Check the node's conditions**: `kubectl describe node ` — look for MemoryPressure, DiskPressure, PIDPressure.
- If unrecoverable, drain and delete: `kubectl drain  --ignore-daemonsets --delete-emptydir-data` then terminate the VM.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Don't panic — check if pods already rescheduled. Kubernetes evicts pods from NotReady nodes after pod-eviction-timeout (default 5 .

#### ⏱️ 60-Second Elevator Pitch Summary

- Don't panic — check if pods already rescheduled. Kubernetes evicts pods from NotReady nodes after...
- Cordon the node — kubectl cordon  prevents new pods from scheduling there while you investigate.
- SSH into the node and check:

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-27-kubernetes-q7-your-hpa-horizontal-pod-autoscaler-is-not-scaling-up-even-though-cpu-usage-is-high-why-l2"></a>
### 27. Kubernetes Q7: Your HPA (Horizontal Pod Autoscaler) is not scaling up even though CPU usage is high Why [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Troubleshooting & Debugging` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your HPA (Horizontal Pod Autoscaler) is not scaling up even though CPU usage is high. Why?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. The interviewer is testing: HPA prerequisites and metrics-server dependency.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

HPA needs `metrics-server` to be installed and working. Without it, HPA can't read CPU/memory metrics and shows `` in `kubectl get hpa`.

- `kubectl get hpa` — if it shows `/50%` for current metric, metrics-server is missing or broken.
- `kubectl top pods` — if this fails, metrics-server is the problem.
- Also check that pods have **resource requests defined** — HPA calculates usage as a percentage of the request value. No requests = HPA can't calculate.

##### 2️⃣ Remediation & Permanent Safeguards

Check: Fix: Install metrics-server, set resource requests on pods. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl get hpa — if it shows /50% for current metric, metrics-server is missing or broken..

#### ⏱️ 60-Second Elevator Pitch Summary

- kubectl get hpa — if it shows /50% for current metric, metrics-server is missing or broken.
- kubectl top pods — if this fails, metrics-server is the problem.
- Also check that pods have resource requests defined — HPA calculates usage as a percentage of the...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-28-kubernetes-q8-a-pod-has-been-running-fine-for-weeks-and-suddenly-starts-failing-with-imagepullbackoff-nothing-in-the-pod-spec-changed-what-could-cause-this-l3"></a>
### 28. Kubernetes Q8: A pod has been running fine for weeks and suddenly starts failing with ImagePullBackOff Nothing in the pod spec changed What could cause this [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Troubleshooting & Debugging` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A pod has been running fine for weeks and suddenly starts failing with `ImagePullBackOff`. Nothing in the pod spec changed. What could cause this?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. The interviewer is testing: Image registry auth and image availability awareness.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Since nothing changed in the spec, suspect external changes:

- **Registry credentials expired** — imagePullSecret token rotated or expired.
- **Image was deleted from the registry** — someone deleted the tag from Docker Hub or ECR.
- **Registry is down or unreachable** — network issue or registry outage.

##### 2️⃣ Remediation & Permanent Safeguards

Check: `kubectl describe pod ` — the event will say exactly which registry returned what error (401 Unauthorized, 404 Not Found, etc.). ---

- **Rate limiting** — Docker Hub has pull rate limits for unauthenticated/free accounts.
- **Private registry changed auth** — ECR tokens expire every 12 hours if not refreshed.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Registry credentials expired — imagePullSecret token rotated or expired..

#### ⏱️ 60-Second Elevator Pitch Summary

- Registry credentials expired — imagePullSecret token rotated or expired.
- Image was deleted from the registry — someone deleted the tag from Docker Hub or ECR.
- Registry is down or unreachable — network issue or registry outage.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-29-kubernetes-q9-you-run-kubectl-exec-it-pod-bash-and-get-container-not-found-whats-wrong-l2"></a>
### 29. Kubernetes Q9: You run kubectl exec -it <pod> -- bash and get container not found Whats wrong [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Troubleshooting & Debugging` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You run `kubectl exec -it  -- bash` and get "container not found." What's wrong?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. The interviewer is testing: Multi-container pod awareness.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

If a pod has multiple containers, you need to specify which one: Get container names with: `kubectl get pod  -o jsonpath='{.spec.containers[*].name}'` Also — some minimal images (Alpine, distroless) don't have `bash`. Try `sh` instead. ---

```bash
kubectl exec -it <pod> -c <container-name> -- bash
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: If a pod has multiple containers, you need to specify which one:.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: If a pod has multiple containers, you need to specify which one:
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-30-kubernetes-q10-your-init-container-is-stuck-and-the-main-container-never-starts-how-do-you-debug-l2"></a>
### 30. Kubernetes Q10: Your init container is stuck and the main container never starts How do you debug [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Troubleshooting & Debugging` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your init container is stuck and the main container never starts. How do you debug?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. The interviewer is testing: Init container execution order and logging.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Init containers run sequentially before the main container. If one fails, the pod stays in `Init:0/1` or similar state.

- `kubectl describe pod ` — check init container status.
- `kubectl logs  -c ` — get init container logs.
- Common causes: init container script fails (wrong path, missing file), waiting for a service that's not up (like a DB), permissions issue.

##### 2️⃣ Remediation & Permanent Safeguards

--- ## 🔵 Deployments & Workloads ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl describe pod  — check init container status..

#### ⏱️ 60-Second Elevator Pitch Summary

- kubectl describe pod  — check init container status.
- kubectl logs  -c  — get init container logs.
- Common causes: init container script fails (wrong path, missing file), waiting for a service that...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-31-kubernetes-q11-whats-the-difference-between-a-deployment-and-a-statefulset-when-would-you-use-each-l1"></a>
### 31. Kubernetes Q11: Whats the difference between a Deployment and a StatefulSet When would you use each [L1]

**Level:** `Junior / Associate DevOps [L1]` | **Category:** `Kubernetes` • `Deployments & Workloads` | **Type:** `Core Fundamentals [L1]`

**Tags:** `Kubernetes` `Deployments & Workloads` `L1` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What's the difference between a Deployment and a StatefulSet? When would you use each?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

If your app needs to remember who it is (stable network ID, stable storage), use StatefulSet. Otherwise use Deployment.

- **Deployment** — for stateless apps. Pods are interchangeable. Any pod can handle any request. Use for web servers, APIs, workers.
- **StatefulSet** — for stateful apps. Each pod gets a stable hostname (pod-0, pod-1...) and its own persistent volume. Pods start and stop in order. Use for databases, Kafka, Elasticsearch, Zookeeper.

##### 2️⃣ Remediation & Permanent Safeguards

---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Deployment — for stateless apps. Pods are interchangeable. Any pod can handle any request. Use for web servers, APIs, workers..

#### ⏱️ 60-Second Elevator Pitch Summary

- Deployment — for stateless apps. Pods are interchangeable. Any pod can handle any request. Use fo...
- StatefulSet — for stateful apps. Each pod gets a stable hostname (pod-0, pod-1...) and its own pe...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-32-kubernetes-q12-you-need-to-run-a-database-in-kubernetes-someone-says-just-use-a-deployment-with-a-pvc-is-that-okay-l2"></a>
### 32. Kubernetes Q12: You need to run a database in Kubernetes Someone says just use a Deployment with a PVC Is that okay [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Deployments & Workloads` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Deployments & Workloads` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You need to run a database in Kubernetes. Someone says just use a Deployment with a PVC. Is that okay?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. The interviewer is testing: StatefulSet necessity understanding.. I structure my answer around systematic triage first, root cause analysis second, and permanent remediation third."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Not ideal. A Deployment doesn't guarantee stable pod identity or ordered startup/shutdown, which matters for clustered databases (Postgres HA, MySQL replication, Cassandra). Also, if a Deployment has multiple replicas, all pods might try to bind the same PVC — which only one can do (unless using ReadWriteMany).

- Each replica gets its own PVC via `volumeClaimTemplates`.
- Pods get stable DNS names (e.g., `mysql-0.mysql`, `mysql-1.mysql`) needed for replication setup.
- Ordered startup ensures primary starts before replicas.

##### 2️⃣ Remediation & Permanent Safeguards

StatefulSet is the right choice because: For a single-instance DB with no replication, a Deployment + PVC works fine but is still a corner case. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Each replica gets its own PVC via volumeClaimTemplates..

#### ⏱️ 60-Second Elevator Pitch Summary

- Each replica gets its own PVC via volumeClaimTemplates.
- Pods get stable DNS names (e.g., mysql-0.mysql, mysql-1.mysql) needed for replication setup.
- Ordered startup ensures primary starts before replicas.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-33-kubernetes-q13-you-updated-a-configmap-thats-mounted-as-an-environment-variable-in-a-pod-the-pod-still-shows-the-old-value-why-l2"></a>
### 33. Kubernetes Q13: You updated a ConfigMap thats mounted as an environment variable in a pod The pod still shows the old value Why [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Deployments & Workloads` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Deployments & Workloads` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You updated a ConfigMap that's mounted as an environment variable in a pod. The pod still shows the old value. Why?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Environment variables are loaded at pod start time. Changing a ConfigMap doesn't restart running pods, so they keep the old values. Fix: **Rolling restart** the deployment — `kubectl rollout restart deployment/`. This creates new pods that pick up the new ConfigMap values. Note: If the ConfigMap is mounted as a **volume file** (not env var), Kubernetes will eventually update the file in the running pod without restart (takes ~1 min). But env vars never auto-update. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Environment variables are loaded at pod start time. Changing a ConfigMap doesn't restart running pods, so they keep the old values.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Environment variables are loaded at pod start time. Changing a ConfigMap doesn't restart runnin
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-34-kubernetes-q14-how-would-you-ensure-a-critical-pod-always-runs-on-the-same-node-l2"></a>
### 34. Kubernetes Q14: How would you ensure a critical pod always runs on the same node [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Deployments & Workloads` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Deployments & Workloads` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How would you ensure a critical pod always runs on the same node?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Two approaches:

- **NodeSelector** — add a label to the node (`kubectl label node  type=critical`) and add `nodeSelector: {type: critical}` to the pod spec. Simple but inflexible.
- **Node Affinity** — more expressive, supports `requiredDuringSchedulingIgnoredDuringExecution` (hard rule) or `preferredDuringScheduling...` (soft preference).

##### 2️⃣ Remediation & Permanent Safeguards

For "always the same node" — use `requiredDuringSchedulingIgnoredDuringExecution` with `nodeAffinity`. But be careful: if that node goes down, the pod won't reschedule elsewhere. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: NodeSelector — add a label to the node (kubectl label node  type=critical) and add nodeSelector: {type: critical} to the pod spec..

#### ⏱️ 60-Second Elevator Pitch Summary

- NodeSelector — add a label to the node (kubectl label node  type=critical) and add nodeSelector: ...
- Node Affinity — more expressive, supports requiredDuringSchedulingIgnoredDuringExecution (hard ru...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-35-kubernetes-q15-you-want-to-make-sure-two-pods-of-the-same-app-never-run-on-the-same-node-how-l2"></a>
### 35. Kubernetes Q15: You want to make sure two pods of the same app NEVER run on the same node How [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Deployments & Workloads` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Deployments & Workloads` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You want to make sure two pods of the same app NEVER run on the same node. How?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use **Pod Anti-Affinity**: `topologyKey: kubernetes.io/hostname` means "don't put two pods with label `app: myapp` on the same host." Use `required` for a hard rule or `preferred` to let Kubernetes still schedule if no option exists. ---

```bash
affinity:
  podAntiAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
    - labelSelector:
        matchLabels:
          app: myapp
      topologyKey: kubernetes.io/hostname
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use Pod Anti-Affinity:.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use Pod Anti-Affinity:
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-36-kubernetes-q16-your-deployment-has-10-replicas-you-need-to-do-a-zero-downtime-deploy-of-a-new-version-how-do-you-configure-and-verify-it-l3"></a>
### 36. Kubernetes Q16: Your deployment has 10 replicas You need to do a zero-downtime deploy of a new version How do you configure and verify it [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Deployments & Workloads` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Deployments & Workloads` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your deployment has 10 replicas. You need to do a zero-downtime deploy of a new version. How do you configure and verify it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Configure RollingUpdate strategy:

- `kubectl rollout status deployment/` — watch it progress.
- Monitor your health endpoint / app metrics during rollout.
- If something goes wrong: `kubectl rollout undo deployment/`.

##### 2️⃣ Remediation & Permanent Safeguards

`maxUnavailable: 0` ensures old pods aren't removed until new ones pass readiness probes. Verify: Also make sure your **readiness probe is accurate** — this is the gating mechanism for zero-downtime. A bad probe that returns ready too early defeats the whole strategy. ---

```bash
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxSurge: 2        # max extra pods during update
    maxUnavailable: 0  # never kill old pod before new one is ready
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl rollout status deployment/ — watch it progress..

#### ⏱️ 60-Second Elevator Pitch Summary

- kubectl rollout status deployment/ — watch it progress.
- Monitor your health endpoint / app metrics during rollout.
- If something goes wrong: kubectl rollout undo deployment/.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-37-kubernetes-q17-what-is-a-daemonset-and-when-do-you-use-it-l1"></a>
### 37. Kubernetes Q17: What is a DaemonSet and when do you use it [L1]

**Level:** `Junior / Associate DevOps [L1]` | **Category:** `Kubernetes` • `Deployments & Workloads` | **Type:** `Core Fundamentals [L1]`

**Tags:** `Kubernetes` `Deployments & Workloads` `L1` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a DaemonSet and when do you use it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

A DaemonSet ensures one pod runs on every node (or a subset of nodes). When a new node joins the cluster, the DaemonSet automatically places a pod on it.

- Log collectors (Fluentd, Filebeat) — need to run on every node to collect logs.
- Monitoring agents (Prometheus node-exporter) — need node-level metrics from every node.
- Network plugins (Calico, Weave) — need to run on every node.

##### 2️⃣ Remediation & Permanent Safeguards

Use cases: ---

- Security agents (Falco, Wazuh) — need to watch every node.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Log collectors (Fluentd, Filebeat) — need to run on every node to collect logs..

#### ⏱️ 60-Second Elevator Pitch Summary

- Log collectors (Fluentd, Filebeat) — need to run on every node to collect logs.
- Monitoring agents (Prometheus node-exporter) — need node-level metrics from every node.
- Network plugins (Calico, Weave) — need to run on every node.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-38-kubernetes-q18-you-have-a-daemonset-but-some-nodes-arent-getting-a-pod-why-l2"></a>
### 38. Kubernetes Q18: You have a DaemonSet but some nodes arent getting a pod Why [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Deployments & Workloads` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Deployments & Workloads` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You have a DaemonSet but some nodes aren't getting a pod. Why?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Common reasons:

- **Node selector or affinity mismatch** — DaemonSet has a `nodeSelector` or affinity rule that doesn't match those nodes.
- **Node has a taint** — the DaemonSet pods don't have a matching toleration. Add the toleration to the DaemonSet spec.
- **Node is cordoned** — `kubectl cordon` prevents any new pod scheduling.

##### 2️⃣ Remediation & Permanent Safeguards

Check: `kubectl describe daemonset ` — look at the Selector and Tolerations. Compare with `kubectl describe node `. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Node selector or affinity mismatch — DaemonSet has a nodeSelector or affinity rule that doesn't match those nodes..

#### ⏱️ 60-Second Elevator Pitch Summary

- Node selector or affinity mismatch — DaemonSet has a nodeSelector or affinity rule that doesn't m...
- Node has a taint — the DaemonSet pods don't have a matching toleration. Add the toleration to the...
- Node is cordoned — kubectl cordon prevents any new pod scheduling.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-39-kubernetes-q19-when-would-you-use-a-job-vs-a-cronjob-l2"></a>
### 39. Kubernetes Q19: When would you use a Job vs a CronJob [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Deployments & Workloads` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Deployments & Workloads` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"When would you use a Job vs a CronJob?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

CronJob creates a new Job object on each schedule trigger. Both ensure the task runs to completion and can be configured to retry on failure.

- **Job** — run a task once to completion. E.g., database migration on deploy, one-time data processing, sending a batch of emails.
- **CronJob** — run a task on a schedule (like cron in Linux). E.g., nightly backups, hourly reports, weekly cleanup jobs.

##### 2️⃣ Remediation & Permanent Safeguards

---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Job — run a task once to completion. E.g., database migration on deploy, one-time data processing, sending a batch of emails..

#### ⏱️ 60-Second Elevator Pitch Summary

- Job — run a task once to completion. E.g., database migration on deploy, one-time data processing...
- CronJob — run a task on a schedule (like cron in Linux). E.g., nightly backups, hourly reports, w...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-40-kubernetes-q20-your-cronjob-is-creating-overlapping-runs-the-previous-job-hasnt-finished-when-the-next-one-starts-how-do-you-fix-it-l2"></a>
### 40. Kubernetes Q20: Your CronJob is creating overlapping runs — the previous job hasnt finished when the next one starts How do you fix it [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Deployments & Workloads` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Deployments & Workloads` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your CronJob is creating overlapping runs — the previous job hasn't finished when the next one starts. How do you fix it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Set `concurrencyPolicy: Forbid` in the CronJob spec. This skips the new run if the previous one is still running.

- `Allow` (default) — multiple jobs can run at the same time.
- `Forbid` — skip the new run if old one still running.
- `Replace` — kill the old run and start a new one.

##### 2️⃣ Remediation & Permanent Safeguards

Options: Also check `startingDeadlineSeconds` — if a job is missed (e.g., cluster was down), Kubernetes may try to catch up on missed runs. --- ## 🟢 Networking ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Allow (default) — multiple jobs can run at the same time..

#### ⏱️ 60-Second Elevator Pitch Summary

- Allow (default) — multiple jobs can run at the same time.
- Forbid — skip the new run if old one still running.
- Replace — kill the old run and start a new one.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-41-kubernetes-q21-what-is-the-difference-between-clusterip-nodeport-and-loadbalancer-service-types-l1"></a>
### 41. Kubernetes Q21: What is the difference between ClusterIP NodePort and LoadBalancer service types [L1]

**Level:** `Junior / Associate DevOps [L1]` | **Category:** `Kubernetes` • `Networking` | **Type:** `Core Fundamentals [L1]`

**Tags:** `Kubernetes` `Networking` `L1` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the difference between ClusterIP, NodePort, and LoadBalancer service types?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

---

- **ClusterIP** — only accessible inside the cluster. Default type. Used for internal service-to-service communication.
- **NodePort** — opens a port (30000–32767) on every node. Traffic to `:` reaches the service. Used for dev/testing or when you manage your own load balancer.
- **LoadBalancer** — creates a cloud load balancer (AWS ELB, GCP LB) and assigns an external IP. Used in production to expose services to the internet. Only works in cloud environments.

##### 2️⃣ Remediation & Permanent Safeguards

Execute the resolution runbook and verify workload health:

#### 🎯 Key Architectural Takeaway
> Pro-Tip: ClusterIP — only accessible inside the cluster. Default type. Used for internal service-to-service communication..

#### ⏱️ 60-Second Elevator Pitch Summary

- ClusterIP — only accessible inside the cluster. Default type. Used for internal service-to-servic...
- NodePort — opens a port (30000–32767) on every node. Traffic to : reaches the service. Used for d...
- LoadBalancer — creates a cloud load balancer (AWS ELB, GCP LB) and assigns an external IP. Used i...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-42-kubernetes-q22-what-is-an-ingress-and-why-do-you-need-it-when-you-already-have-loadbalancer-services-l2"></a>
### 42. Kubernetes Q22: What is an Ingress and why do you need it when you already have LoadBalancer services [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Networking` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Networking` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is an Ingress and why do you need it when you already have LoadBalancer services?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Every LoadBalancer service creates a new cloud load balancer = new cost + new IP address. For 10 services, that's 10 load balancers.

- `api.myapp.com` → API service
- `app.myapp.com` → Frontend service
- `myapp.com/admin` → Admin service

##### 2️⃣ Remediation & Permanent Safeguards

Ingress uses **one** load balancer (the Ingress Controller) and routes HTTP/HTTPS traffic to different services based on hostname or URL path rules. Much cheaper and cleaner. Example: All through one load balancer. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: api.myapp.com → API service.

#### ⏱️ 60-Second Elevator Pitch Summary

- api.myapp.com → API service
- app.myapp.com → Frontend service
- myapp.com/admin → Admin service

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-43-kubernetes-q23-your-ingress-is-returning-404-for-a-path-that-youve-configured-what-do-you-check-l2"></a>
### 43. Kubernetes Q23: Your Ingress is returning 404 for a path that youve configured What do you check [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Networking` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Networking` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your Ingress is returning 404 for a path that you've configured. What do you check?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

---

- **Check the Ingress resource** — `kubectl describe ingress ` — verify the path and service name are correct.
- **Check the IngressClass** — does the Ingress have the right `ingressClassName`? If multiple controllers exist (nginx, traefik), the wrong one might be handling it.
- **Check path type** — `Exact` vs `Prefix` vs `ImplementationSpecific`. `Exact` only matches `/api`, not `/api/users`. Use `Prefix` to match all subpaths.

##### 2️⃣ Remediation & Permanent Safeguards

Execute the resolution runbook and verify workload health:

- **Check backend service** — is the service name and port correct? Does the service have endpoints?
- **Ingress controller logs** — `kubectl logs -n ingress-nginx ` — nginx logs will show 404 details.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Check the Ingress resource — kubectl describe ingress  — verify the path and service name are correct..

#### ⏱️ 60-Second Elevator Pitch Summary

- Check the Ingress resource — kubectl describe ingress  — verify the path and service name are cor...
- Check the IngressClass — does the Ingress have the right ingressClassName? If multiple controller...
- Check path type — Exact vs Prefix vs ImplementationSpecific. Exact only matches /api, not /api/us...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-44-kubernetes-q24-you-have-a-microservices-app-where-service-a-should-never-talk-directly-to-service-c-only-through-service-b-how-do-you-enforce-this-in-kubernetes-l3"></a>
### 44. Kubernetes Q24: You have a microservices app where Service A should never talk directly to Service C only through Service B How do you enforce this in Kubernetes [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Networking` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Networking` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You have a microservices app where Service A should never talk directly to Service C, only through Service B. How do you enforce this in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use **NetworkPolicy**. By default, all pods can talk to all other pods. NetworkPolicy lets you restrict this. Example — block direct traffic to Service C except from Service B: This says: "Only accept incoming traffic to pods labeled `app: service-c` if it comes from pods labeled `app: service-b`." Note: NetworkPolicy requires a CNI plugin that supports it (Calico, Cilium, Weave). Flannel does not support NetworkPolicy by default. ---

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-only-from-b
spec:
  podSelector:
    matchLabels:
      app: service-c
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: service-b
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use NetworkPolicy. By default, all pods can talk to all other pods. NetworkPolicy lets you restrict this..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use NetworkPolicy. By default, all pods can talk to all other pods. NetworkPolicy lets you rest
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-45-kubernetes-q25-what-is-a-headless-service-and-why-would-you-use-it-l2"></a>
### 45. Kubernetes Q25: What is a headless service and why would you use it [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Networking` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Networking` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a headless service and why would you use it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

A headless service has `clusterIP: None`. Instead of a single virtual IP, DNS queries for a headless service return the actual pod IPs directly.

- **StatefulSets** — each pod needs its own DNS name (`pod-0.service`, `pod-1.service`) for inter-pod communication (like database replication).
- **Client-side load balancing** — let the app choose which pod to connect to instead of going through kube-proxy.
- **Service discovery** — let your app discover all pod IPs directly.

##### 2️⃣ Remediation & Permanent Safeguards

Use cases: ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: StatefulSets — each pod needs its own DNS name (pod-0.service, pod-1.service) for inter-pod communication (like database replicati.

#### ⏱️ 60-Second Elevator Pitch Summary

- StatefulSets — each pod needs its own DNS name (pod-0.service, pod-1.service) for inter-pod commu...
- Client-side load balancing — let the app choose which pod to connect to instead of going through ...
- Service discovery — let your app discover all pod IPs directly.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-46-kubernetes-q26-a-request-is-going-from-pod-a-to-pod-b-via-a-service-and-its-very-slow-how-do-you-troubleshoot-network-latency-in-kubernetes-l3"></a>
### 46. Kubernetes Q26: A request is going from Pod A to Pod B via a Service and its very slow How do you troubleshoot network latency in Kubernetes [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Networking` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Networking` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A request is going from Pod A to Pod B via a Service and it's very slow. How do you troubleshoot network latency in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

---

- **Baseline test** — `kubectl exec -it  -- curl -o /dev/null -s -w "%{time_total}" http://:` to measure actual latency.
- **Bypass the service** — test pod-to-pod directly using the pod IP to see if latency is in kube-proxy/iptables: `kubectl exec -it  -- curl http://:`.
- **Check kube-proxy mode** — iptables vs ipvs. ipvs is faster at scale.
- **Check CNI** — network plugin issues. Run `ping` between pods to test raw network latency.

##### 2️⃣ Remediation & Permanent Safeguards

Execute the resolution runbook and verify workload health:

- **DNS latency** — `kubectl exec -it  -- time nslookup ` — DNS lookups through CoreDNS add latency. Consider `ndots:5` setting impact.
- **Node-level network** — check if nodes are on the same AZ. Cross-AZ traffic adds ~1-2ms.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Baseline test — kubectl exec -it  -- curl -o /dev/null -s -w "%{time_total}" http://: to measure actual latency..

#### ⏱️ 60-Second Elevator Pitch Summary

- Baseline test — kubectl exec -it  -- curl -o /dev/null -s -w "%{time_total}" http://: to measure ...
- Bypass the service — test pod-to-pod directly using the pod IP to see if latency is in kube-proxy...
- Check kube-proxy mode — iptables vs ipvs. ipvs is faster at scale.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-47-kubernetes-q27-dns-resolution-is-failing-inside-your-cluster-pods-cant-resolve-service-names-what-do-you-check-l2"></a>
### 47. Kubernetes Q27: DNS resolution is failing inside your cluster Pods cant resolve service names What do you check [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Networking` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Networking` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"DNS resolution is failing inside your cluster. Pods can't resolve service names. What do you check?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

---

- `kubectl get pods -n kube-system | grep coredns` — is CoreDNS running?
- `kubectl logs -n kube-system ` — any errors?
- Test DNS from inside a pod: `kubectl exec -it  -- nslookup kubernetes.default` — this should always resolve.

##### 2️⃣ Remediation & Permanent Safeguards

## 🟡 Storage ---

- Check `resolv.conf` inside the pod: `kubectl exec -it  -- cat /etc/resolv.conf` — should point to the cluster DNS IP.
- Check CoreDNS ConfigMap: `kubectl get configmap coredns -n kube-system -o yaml` — misconfigured forwarders can break external DNS resolution.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl get pods -n kube-system | grep coredns — is CoreDNS running?.

#### ⏱️ 60-Second Elevator Pitch Summary

- kubectl get pods -n kube-system | grep coredns — is CoreDNS running?
- kubectl logs -n kube-system  — any errors?
- Test DNS from inside a pod: kubectl exec -it  -- nslookup kubernetes.default — this should always...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-48-kubernetes-q28-what-is-the-difference-between-a-persistentvolume-pv-and-a-persistentvolumeclaim-pvc-l1"></a>
### 48. Kubernetes Q28: What is the difference between a PersistentVolume (PV) and a PersistentVolumeClaim (PVC) [L1]

**Level:** `Junior / Associate DevOps [L1]` | **Category:** `Kubernetes` • `Storage` | **Type:** `Core Fundamentals [L1]`

**Tags:** `Kubernetes` `Storage` `L1` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the difference between a PersistentVolume (PV) and a PersistentVolumeClaim (PVC)?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Think of PV as the actual parking spot and PVC as the parking ticket that reserves it.

- **PV (PersistentVolume)** — the actual storage resource. Could be an AWS EBS volume, NFS share, local disk. Created by a cluster admin or dynamically provisioned.
- **PVC (PersistentVolumeClaim)** — a request for storage by a pod. The pod says "I need 10GB of ReadWriteOnce storage" — the PVC finds a matching PV and binds to it.

##### 2️⃣ Remediation & Permanent Safeguards

---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: PV (PersistentVolume) — the actual storage resource. Could be an AWS EBS volume, NFS share, local disk. Created by a cluster admin.

#### ⏱️ 60-Second Elevator Pitch Summary

- PV (PersistentVolume) — the actual storage resource. Could be an AWS EBS volume, NFS share, local...
- PVC (PersistentVolumeClaim) — a request for storage by a pod. The pod says "I need 10GB of ReadWr...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-49-kubernetes-q29-a-pvc-is-stuck-in-pending-state-what-do-you-check-l2"></a>
### 49. Kubernetes Q29: A PVC is stuck in Pending state What do you check [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Storage` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Storage` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A PVC is stuck in `Pending` state. What do you check?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

---

- **No matching PV** — check if a PV exists with matching `storageClassName`, `accessMode`, and enough capacity: `kubectl get pv`.
- **StorageClass doesn't exist** — `kubectl get storageclass`. If the PVC references a storage class that doesn't exist, it stays Pending.
- **Dynamic provisioner not working** — if using dynamic provisioning (like AWS EBS CSI driver), check if the CSI driver pods are running: `kubectl get pods -n kube-system | grep csi`.

##### 2️⃣ Remediation & Permanent Safeguards

Execute the resolution runbook and verify workload health:

- **Volume binding mode** — if the StorageClass has `volumeBindingMode: WaitForFirstConsumer`, the PVC stays Pending until a pod that uses it is scheduled. That's normal behavior.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: No matching PV — check if a PV exists with matching storageClassName, accessMode, and enough capacity: kubectl get pv..

#### ⏱️ 60-Second Elevator Pitch Summary

- No matching PV — check if a PV exists with matching storageClassName, accessMode, and enough capa...
- StorageClass doesn't exist — kubectl get storageclass. If the PVC references a storage class that...
- Dynamic provisioner not working — if using dynamic provisioning (like AWS EBS CSI driver), check ...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-50-kubernetes-q30-you-deleted-a-pvc-but-the-data-is-gone-how-could-you-have-protected-it-l2"></a>
### 50. Kubernetes Q30: You deleted a PVC but the data is gone How could you have protected it [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Storage` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Storage` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You deleted a PVC but the data is gone. How could you have protected it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

By setting the **Reclaim Policy** on the PV or StorageClass:

- `Delete` (default for dynamic provisioning) — deletes the underlying volume when PVC is deleted. Data is gone.
- `Retain` — PV stays after PVC deletion. Data is preserved. Admin must manually reclaim.
- `Recycle` — deprecated, performed basic cleanup.

##### 2️⃣ Remediation & Permanent Safeguards

Also: use **VolumeSnapshot** to take backups before deleting. Or enable backup tools like Velero that snapshot PVC data. Lesson: Always check the StorageClass reclaim policy in production. Default `Delete` on cloud providers will wipe your data. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Delete (default for dynamic provisioning) — deletes the underlying volume when PVC is deleted. Data is gone..

#### ⏱️ 60-Second Elevator Pitch Summary

- Delete (default for dynamic provisioning) — deletes the underlying volume when PVC is deleted. Da...
- Retain — PV stays after PVC deletion. Data is preserved. Admin must manually reclaim.
- Recycle — deprecated, performed basic cleanup.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-51-kubernetes-q31-a-statefulset-pod-cant-start-because-its-trying-to-attach-a-volume-thats-still-attached-to-a-terminated-pod-on-a-dead-node-how-do-you-fix-it-l3"></a>
### 51. Kubernetes Q31: A StatefulSet pod cant start because its trying to attach a volume thats still attached to a terminated pod on a dead node How do you fix it [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Storage` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Storage` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A StatefulSet pod can't start because it's trying to attach a volume that's still attached to a terminated pod on a dead node. How do you fix it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

This is a common scenario when a node dies without gracefully releasing its volumes. The PV shows `Terminating` or the pod shows volume attach error.

- Force delete the stuck pod: `kubectl delete pod  --grace-period=0 --force`
- Check if the PV is stuck: `kubectl describe pv ` — look for the node it's attached to.
- On AWS (EBS): use AWS CLI to force detach the volume: `aws ec2 detach-volume --volume-id  --force`

##### 2️⃣ Remediation & Permanent Safeguards

Steps: --- ## 🟣 RBAC & Security ---

- Check the VolumeAttachment object: `kubectl get volumeattachment` — delete the stuck one.
- The new pod should then attach the volume successfully.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Force delete the stuck pod: kubectl delete pod  --grace-period=0 --force.

#### ⏱️ 60-Second Elevator Pitch Summary

- Force delete the stuck pod: kubectl delete pod  --grace-period=0 --force
- Check if the PV is stuck: kubectl describe pv  — look for the node it's attached to.
- On AWS (EBS): use AWS CLI to force detach the volume: aws ec2 detach-volume --volume-id  --force

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-52-kubernetes-q32-a-developer-says-they-cant-list-pods-in-the-production-namespace-but-they-can-in-staging-how-do-you-debug-this-l2"></a>
### 52. Kubernetes Q32: A developer says they cant list pods in the production namespace but they can in staging How do you debug this [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `RBAC & Security` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `RBAC & Security` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A developer says they can't list pods in the `production` namespace but they can in `staging`. How do you debug this?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

RBAC controls are namespace-scoped. Check:

- `kubectl auth can-i list pods --namespace=production --as=` — quick check.
- `kubectl get rolebinding -n production` — see what roles are bound in the production namespace.
- `kubectl get clusterrolebinding | grep ` — check if there's a cluster-level binding.

##### 2️⃣ Remediation & Permanent Safeguards

Fix: Create a RoleBinding in the `production` namespace giving the user the `view` or appropriate role: ---

```bash
kubectl create rolebinding dev-view --clusterrole=view --user=<username> -n production
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl auth can-i list pods --namespace=production --as= — quick check..

#### ⏱️ 60-Second Elevator Pitch Summary

- kubectl auth can-i list pods --namespace=production --as= — quick check.
- kubectl get rolebinding -n production — see what roles are bound in the production namespace.
- kubectl get clusterrolebinding | grep  — check if there's a cluster-level binding.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-53-kubernetes-q33-you-run-a-pod-that-needs-to-call-the-kubernetes-api-eg-to-list-other-pods-how-do-you-set-this-up-securely-l2"></a>
### 53. Kubernetes Q33: You run a pod that needs to call the Kubernetes API (eg to list other pods) How do you set this up securely [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `RBAC & Security` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `RBAC & Security` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You run a pod that needs to call the Kubernetes API (e.g., to list other pods). How do you set this up securely?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

The pod will then have a token mounted at `/var/run/secrets/kubernetes.io/serviceaccount/token` which it can use to authenticate to the API server.

- Create a **ServiceAccount**: `kubectl create serviceaccount my-app -n my-namespace`
- Create a **Role** with only the needed permissions (principle of least privilege):
- Create a **RoleBinding** linking the ServiceAccount to the Role.

##### 2️⃣ Remediation & Permanent Safeguards

Avoid using the default ServiceAccount — it often has more permissions than needed. ---

- Set `serviceAccountName: my-app` in the pod spec.

```bash
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list"]
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Create a ServiceAccount: kubectl create serviceaccount my-app -n my-namespace.

#### ⏱️ 60-Second Elevator Pitch Summary

- Create a ServiceAccount: kubectl create serviceaccount my-app -n my-namespace
- Create a Role with only the needed permissions (principle of least privilege):
- Create a RoleBinding linking the ServiceAccount to the Role.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-54-kubernetes-q34-someone-accidentally-ran-kubectl-delete-clusterrolebinding-cluster-admin-and-deleted-the-cluster-admin-binding-now-no-one-can-manage-the-cluster-what-do-you-do-l3"></a>
### 54. Kubernetes Q34: Someone accidentally ran kubectl delete clusterrolebinding cluster-admin and deleted the cluster admin binding Now no one can manage the cluster What do you do [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `RBAC & Security` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `RBAC & Security` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Someone accidentally ran `kubectl delete clusterrolebinding cluster-admin` and deleted the cluster admin binding. Now no one can manage the cluster. What do you do?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

This is a serious situation. If you're locked out of the API server entirely:

- **SSH directly to a control plane node**.
- Use `kubectl` with the admin kubeconfig at `/etc/kubernetes/admin.conf` (set `KUBECONFIG=/etc/kubernetes/admin.conf`). This uses certificate-based auth that bypasses RBAC.
- Recreate the cluster-admin binding:

##### 2️⃣ Remediation & Permanent Safeguards

Prevention: Never give a single ClusterRoleBinding a name that might be confused with a default. Back up RBAC configs. Use `--dry-run=client` before destructive commands. --- ## 🔵 Scaling & Performance ---

```bash
kubectl create clusterrolebinding cluster-admin \
  --clusterrole=cluster-admin \
  --user=<your-user>
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: SSH directly to a control plane node..

#### ⏱️ 60-Second Elevator Pitch Summary

- SSH directly to a control plane node.
- Use kubectl with the admin kubeconfig at /etc/kubernetes/admin.conf (set KUBECONFIG=/etc/kubernet...
- Recreate the cluster-admin binding:

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-55-kubernetes-q35-your-app-gets-a-traffic-spike-every-day-at-9-am-when-offices-open-hpa-isnt-fast-enough-what-do-you-do-l2"></a>
### 55. Kubernetes Q35: Your app gets a traffic spike every day at 9 AM when offices open HPA isnt fast enough What do you do [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Scaling & Performance` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Scaling & Performance` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your app gets a traffic spike every day at 9 AM when offices open. HPA isn't fast enough. What do you do?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

HPA is reactive — it waits for metrics to breach thresholds before scaling. By then you've already had a slowdown.

- **Predictive scaling with KEDA** — KEDA supports cron-based scaling. Scale up at 8:45 AM before the spike hits.
- **VPA + HPA combo** — pre-tune pod sizes so each pod handles more load.
- **Keep minimum replicas higher** — set HPA `minReplicas` higher during business hours using a CronJob that patches the HPA.

##### 2️⃣ Remediation & Permanent Safeguards

Solutions: ---

- **Cluster Autoscaler tuning** — pre-warm nodes so pod scheduling isn't delayed when HPA does fire.
- **Horizontal + Cache** — add caching (Redis) to reduce per-request load.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Predictive scaling with KEDA — KEDA supports cron-based scaling. Scale up at 8:45 AM before the spike hits..

#### ⏱️ 60-Second Elevator Pitch Summary

- Predictive scaling with KEDA — KEDA supports cron-based scaling. Scale up at 8:45 AM before the s...
- VPA + HPA combo — pre-tune pod sizes so each pod handles more load.
- Keep minimum replicas higher — set HPA minReplicas higher during business hours using a CronJob t...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-56-kubernetes-q36-hpa-is-scaling-pods-up-and-down-too-aggressively-causing-instability-how-do-you-fix-it-l2"></a>
### 56. Kubernetes Q36: HPA is scaling pods up and down too aggressively causing instability How do you fix it [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Scaling & Performance` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Scaling & Performance` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"HPA is scaling pods up and down too aggressively, causing instability. How do you fix it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

HPA has a stabilization window to prevent thrashing. Tune it: Scale up fast, scale down slow — this is the recommended pattern to handle spiky traffic without instability. ---

```bash
behavior:
  scaleDown:
    stabilizationWindowSeconds: 300  # wait 5 min before scaling down
    policies:
    - type: Pods
      value: 1
      periodSeconds: 60  # scale down max 1 pod per minute
  scaleUp:
    stabilizationWindowSeconds: 0
    policies:
    - type: Pods
      value: 4
      periodSeconds: 60
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: HPA has a stabilization window to prevent thrashing. Tune it:.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: HPA has a stabilization window to prevent thrashing. Tune it:
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-57-kubernetes-q37-your-cluster-has-50-nodes-and-pod-scheduling-is-taking-10-seconds-what-could-cause-this-and-how-do-you-fix-it-l3"></a>
### 57. Kubernetes Q37: Your cluster has 50 nodes and pod scheduling is taking 10+ seconds What could cause this and how do you fix it [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Scaling & Performance` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Scaling & Performance` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your cluster has 50 nodes and pod scheduling is taking 10+ seconds. What could cause this and how do you fix it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

The kube-scheduler evaluates all nodes for each pod. At 50 nodes it shouldn't be slow unless:

- **High pod churn** — many pods being created/deleted rapidly, overwhelming the scheduler queue.
- **Complex affinity rules** — complex pod/node affinity is O(n) per scheduling cycle.
- **Scheduler config `percentageOfNodesToScore`** — default is 100% for small clusters but can be lowered for large ones.

##### 2️⃣ Remediation & Permanent Safeguards

Fix: Profile with scheduler metrics, simplify affinity rules, tune `percentageOfNodesToScore`, optimize admission webhooks. --- ## 🟠 Advanced Scenarios ---

- **etcd latency** — scheduler reads from etcd. If etcd is slow, scheduling slows.
- **Webhook admission controllers** — mutating or validating webhooks add latency per-pod.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: High pod churn — many pods being created/deleted rapidly, overwhelming the scheduler queue..

#### ⏱️ 60-Second Elevator Pitch Summary

- High pod churn — many pods being created/deleted rapidly, overwhelming the scheduler queue.
- Complex affinity rules — complex pod/node affinity is O(n) per scheduling cycle.
- Scheduler config percentageOfNodesToScore — default is 100% for small clusters but can be lowered...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-58-kubernetes-q38-you-need-to-run-a-privileged-pod-that-can-modify-kernel-parameters-on-the-host-how-do-you-do-this-and-what-are-the-security-implications-l3"></a>
### 58. Kubernetes Q38: You need to run a privileged pod that can modify kernel parameters on the host How do you do this and what are the security implications [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You need to run a privileged pod that can modify kernel parameters on the host. How do you do this and what are the security implications?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Set `securityContext` on the pod/container:

- A privileged container can escape to the host — it's essentially root on the node.
- If the app is compromised, the attacker owns the node.
- Never run privileged in production unless absolutely necessary (CNI plugins, node debuggers).

##### 2️⃣ Remediation & Permanent Safeguards

Or use specific capabilities instead of full privileged mode (much safer): Security implications: ---

- Use PSA (Pod Security Admission) or OPA/Gatekeeper to block privileged pods cluster-wide unless explicitly exempted.

```bash
securityContext:
  privileged: true
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: A privileged container can escape to the host — it's essentially root on the node..

#### ⏱️ 60-Second Elevator Pitch Summary

- A privileged container can escape to the host — it's essentially root on the node.
- If the app is compromised, the attacker owns the node.
- Never run privileged in production unless absolutely necessary (CNI plugins, node debuggers).

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-59-kubernetes-q39-you-need-to-do-a-zero-downtime-migration-of-a-statefulset-eg-upgrading-postgres-version-walk-me-through-your-approach-l3"></a>
### 59. Kubernetes Q39: You need to do a zero-downtime migration of a StatefulSet (eg upgrading Postgres version) Walk me through your approach [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You need to do a zero-downtime migration of a StatefulSet (e.g., upgrading Postgres version). Walk me through your approach."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

StatefulSets don't support zero-downtime rolling updates as cleanly as Deployments because each pod has unique state.

- **Take a backup first** — always. Snapshot the PVC with VolumeSnapshot or pg_dump.
- **Set `updateStrategy` to `OnDelete`** — this lets you control which pods update manually.
- **Update the StatefulSet spec** (new image version).
- **Delete pods one at a time** — start with replicas (highest ordinal), not the primary. Let each pod restart with the new version and come up healthy before proceeding.

##### 2️⃣ Remediation & Permanent Safeguards

Approach: For major Postgres version upgrades: consider blue-green approach — spin up new StatefulSet, replicate data, cut traffic over. ---

- **Verify replication health** between each pod update.
- **Update the primary last** — failover to a replica first if needed.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Take a backup first — always. Snapshot the PVC with VolumeSnapshot or pg_dump..

#### ⏱️ 60-Second Elevator Pitch Summary

- Take a backup first — always. Snapshot the PVC with VolumeSnapshot or pg_dump.
- Set updateStrategy to OnDelete — this lets you control which pods update manually.
- Update the StatefulSet spec (new image version).

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-60-kubernetes-q40-your-team-wants-to-implement-gitops-for-kubernetes-what-tools-would-you-recommend-and-what-does-the-workflow-look-like-l3"></a>
### 60. Kubernetes Q40: Your team wants to implement GitOps for Kubernetes What tools would you recommend and what does the workflow look like [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your team wants to implement GitOps for Kubernetes. What tools would you recommend and what does the workflow look like?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Tools: **ArgoCD** or **Flux** — both are CNCF projects.

- Developer pushes code → CI pipeline builds image, pushes to registry, updates the image tag in the Git repo (Helm values or kustomize overlay).
- ArgoCD/Flux watches the Git repo. Detects the change.
- ArgoCD/Flux applies the new manifests to the cluster.
- If the cluster state drifts from Git (someone does `kubectl apply` manually), ArgoCD marks the app as OutOfSync and can auto-correct.
- Git is the single source of truth.

##### 2️⃣ Remediation & Permanent Safeguards

GitOps workflow: Benefits: ---

- All changes are auditable (git log = change history).
- Rollback = `git revert`.
- No kubectl access needed for developers in production.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Developer pushes code → CI pipeline builds image, pushes to registry, updates the image tag in the Git repo (Helm values or kustom.

#### ⏱️ 60-Second Elevator Pitch Summary

- Developer pushes code → CI pipeline builds image, pushes to registry, updates the image tag in th...
- ArgoCD/Flux watches the Git repo. Detects the change.
- ArgoCD/Flux applies the new manifests to the cluster.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-61-kubernetes-q41-how-do-you-handle-secrets-in-kubernetes-what-are-the-problems-with-default-kubernetes-secrets-l2"></a>
### 61. Kubernetes Q41: How do you handle secrets in Kubernetes What are the problems with default Kubernetes Secrets [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you handle secrets in Kubernetes? What are the problems with default Kubernetes Secrets?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Default Kubernetes Secrets problems:

- They're only base64 encoded, not encrypted. Anyone with etcd access can read them.
- They're stored in etcd in plaintext by default (unless etcd encryption is enabled).
- RBAC can restrict who reads them, but it's easy to accidentally over-grant.
- **Encrypt etcd at rest** — enable `EncryptionConfiguration` in the API server.

##### 2️⃣ Remediation & Permanent Safeguards

Better approaches: Production recommendation: External Secrets Operator + AWS Secrets Manager or HashiCorp Vault. ---

- **External secrets** — use **External Secrets Operator** to sync secrets from AWS Secrets Manager, HashiCorp Vault, or GCP Secret Manager into Kubernetes Secrets.
- **Vault Agent Injector** — inject secrets directly into pods as files without storing in etcd at all.
- **Sealed Secrets (Bitnami)** — encrypt secrets before storing in Git. Safe to commit.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: They're only base64 encoded, not encrypted. Anyone with etcd access can read them..

#### ⏱️ 60-Second Elevator Pitch Summary

- They're only base64 encoded, not encrypted. Anyone with etcd access can read them.
- They're stored in etcd in plaintext by default (unless etcd encryption is enabled).
- RBAC can restrict who reads them, but it's easy to accidentally over-grant.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-62-kubernetes-q42-a-developer-wants-to-test-a-microservice-that-depends-on-8-other-services-setting-up-the-full-cluster-locally-is-impractical-what-would-you-suggest-l3"></a>
### 62. Kubernetes Q42: A developer wants to test a microservice that depends on 8 other services Setting up the full cluster locally is impractical What would you suggest [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A developer wants to test a microservice that depends on 8 other services. Setting up the full cluster locally is impractical. What would you suggest?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Several approaches:

- **Telepresence** — run the developer's service locally but connected to the real cluster. Traffic from/to the real cluster routes through the local process. Feels like running in-cluster.
- **Skaffold** — automates build-deploy cycles. Code change → auto-build → auto-deploy to dev namespace. Fast inner loop.
- **Namespace-based isolation** — give the developer their own namespace with all dependencies deployed but pointing to shared/mocked backends.

##### 2️⃣ Remediation & Permanent Safeguards

Best combo: Telepresence + a shared dev cluster where real dependent services run. ---

- **Service virtualization** — mock the dependencies the developer doesn't care about using tools like WireMock or Microcks.
- **KinD or k3d** — lightweight local Kubernetes for running the full stack locally if resources allow.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Telepresence — run the developer's service locally but connected to the real cluster. Traffic from/to the real cluster routes thro.

#### ⏱️ 60-Second Elevator Pitch Summary

- Telepresence — run the developer's service locally but connected to the real cluster. Traffic fro...
- Skaffold — automates build-deploy cycles. Code change → auto-build → auto-deploy to dev namespace...
- Namespace-based isolation — give the developer their own namespace with all dependencies deployed...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-63-kubernetes-q43-your-cluster-upgrade-from-126-to-127-failed-halfway-through-control-plane-is-on-127-but-worker-nodes-are-still-on-126-is-this-okay-l2"></a>
### 63. Kubernetes Q43: Your cluster upgrade from 126 to 127 failed halfway through Control plane is on 127 but worker nodes are still on 126 Is this okay [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your cluster upgrade from 1.26 to 1.27 failed halfway through. Control plane is on 1.27 but worker nodes are still on 1.26. Is this okay?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Yes — this is a supported temporary state during upgrades. Kubernetes supports **N-2 version skew** between control plane and nodes. A 1.27 control plane can manage 1.25, 1.26, and 1.27 nodes.

- Verify the control plane is healthy: `kubectl get nodes` — control plane nodes should show 1.27.
- Continue upgrading worker nodes one by one: drain, upgrade kubelet/kubectl/kubeadm, uncordon.
- Do not skip more than one minor version during upgrades.

##### 2️⃣ Remediation & Permanent Safeguards

Next steps: Never upgrade worker nodes before the control plane — that would be an unsupported configuration. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Verify the control plane is healthy: kubectl get nodes — control plane nodes should show 1.27..

#### ⏱️ 60-Second Elevator Pitch Summary

- Verify the control plane is healthy: kubectl get nodes — control plane nodes should show 1.27.
- Continue upgrading worker nodes one by one: drain, upgrade kubelet/kubectl/kubeadm, uncordon.
- Do not skip more than one minor version during upgrades.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-64-kubernetes-q44-how-do-you-handle-configuration-that-differs-between-environments-dev-staging-prod-in-kubernetes-l2"></a>
### 64. Kubernetes Q44: How do you handle configuration that differs between environments (dev staging prod) in Kubernetes [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you handle configuration that differs between environments (dev, staging, prod) in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Two main approaches:

- **Kustomize** — base manifests + environment-specific overlays. Overlay patches change values (image tags, resource limits, replica counts) per environment without duplicating YAML.
- **Helm** — use different `values.yaml` files per environment. `helm install -f values.prod.yaml` applies prod-specific values.
- Use same manifests for all environments (promotes "production parity").

##### 2️⃣ Remediation & Permanent Safeguards

Best practice: ---

- Only override what genuinely differs: image tags, replica counts, resource limits, ingress hostnames, secret references.
- Don't use separate Deployment files per environment — too much duplication and drift.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Kustomize — base manifests + environment-specific overlays. Overlay patches change values (image tags, resource limits, replica co.

#### ⏱️ 60-Second Elevator Pitch Summary

- Kustomize — base manifests + environment-specific overlays. Overlay patches change values (image ...
- Helm — use different values.yaml files per environment. helm install -f values.prod.yaml applies ...
- Use same manifests for all environments (promotes "production parity").

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-65-kubernetes-q45-you-want-to-implement-pod-disruption-budgets-across-your-cluster-what-is-a-pdb-and-how-does-it-protect-your-services-l3"></a>
### 65. Kubernetes Q45: You want to implement pod disruption budgets across your cluster What is a PDB and how does it protect your services [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You want to implement pod disruption budgets across your cluster. What is a PDB and how does it protect your services?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

A **PodDisruptionBudget (PDB)** limits how many pods of a deployment can be voluntarily disrupted at the same time. "Voluntary disruption" includes node drains, rolling updates, and cluster upgrades.

- `minAvailable: 2` — at least 2 pods must remain.
- `maxUnavailable: 1` — at most 1 pod can be down at a time.

##### 2️⃣ Remediation & Permanent Safeguards

Example: This says: "When draining a node, don't proceed if it would bring my-app below 2 running pods." Use: During a cluster upgrade when nodes are drained, without PDBs your entire deployment could go down if all pods happen to be on the nodes being drained. ---

```yaml
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
  name: my-app-pdb
spec:
  minAvailable: 2
  selector:
    matchLabels:
      app: my-app
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: minAvailable: 2 — at least 2 pods must remain..

#### ⏱️ 60-Second Elevator Pitch Summary

- minAvailable: 2 — at least 2 pods must remain.
- maxUnavailable: 1 — at most 1 pod can be down at a time.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-66-kubernetes-q46-what-happens-to-pods-when-you-run-kubectl-drain-on-a-node-l2"></a>
### 66. Kubernetes Q46: What happens to pods when you run kubectl drain on a node [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What happens to pods when you run `kubectl drain` on a node?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

`kubectl drain` does two things:

- **Cordons the node** — marks it unschedulable so no new pods land on it.
- **Evicts all pods** — sends eviction requests (not delete) for every pod. Eviction respects PodDisruptionBudgets.
- DaemonSet pods (need `--ignore-daemonsets` flag to proceed).

##### 2️⃣ Remediation & Permanent Safeguards

Exceptions — these pods are NOT evicted by default: After drain: the node is empty and safe to maintain/terminate. ---

- Pods with local storage (need `--delete-emptydir-data` flag).
- Pods not managed by a controller (standalone pods) — drain will fail unless you force it.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Cordons the node — marks it unschedulable so no new pods land on it..

#### ⏱️ 60-Second Elevator Pitch Summary

- Cordons the node — marks it unschedulable so no new pods land on it.
- Evicts all pods — sends eviction requests (not delete) for every pod. Eviction respects PodDisrup...
- DaemonSet pods (need --ignore-daemonsets flag to proceed).

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-67-kubernetes-q47-explain-how-the-kubernetes-scheduler-makes-a-placement-decision-for-a-new-pod-l3"></a>
### 67. Kubernetes Q47: Explain how the Kubernetes scheduler makes a placement decision for a new pod [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Explain how the Kubernetes scheduler makes a placement decision for a new pod."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

The scheduler goes through two phases:

- Does the node have enough CPU and memory?
- Does the node match the pod's `nodeSelector`?
- Does the pod tolerate the node's taints?
- Are the required volumes available in that zone?
- Does the pod's affinity/anti-affinity rule allow this node?

##### 2️⃣ Remediation & Permanent Safeguards

**Phase 1: Filtering (Predicates)** Eliminate nodes that can't run the pod: **Phase 2: Scoring (Priorities)** Rank the remaining nodes: The highest-scoring node wins. If tied, a random one is picked. The scheduler then writes the chosen node name into the pod's spec (`nodeName` field), and the kubelet on that node picks it up and starts the pod. ---

- Least requested resources (prefer emptier nodes for better bin-packing).
- Affinity preference scores.
- Topology spread.
- Image locality (prefer nodes that already have the image pulled).

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Does the node have enough CPU and memory?.

#### ⏱️ 60-Second Elevator Pitch Summary

- Does the node have enough CPU and memory?
- Does the node match the pod's nodeSelector?
- Does the pod tolerate the node's taints?

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-68-kubernetes-q48-what-is-a-limitrange-and-why-would-you-use-it-l2"></a>
### 68. Kubernetes Q48: What is a LimitRange and why would you use it [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a LimitRange and why would you use it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

A LimitRange sets default and maximum resource requests/limits for pods in a namespace. If a pod doesn't specify resources, LimitRange fills in defaults.

- **Prevent runaway pods** — without limits, one pod can consume all node CPU/memory.
- **Ensure HPA works** — HPA needs resource requests set. LimitRange auto-sets them.
- **Fair resource sharing** — prevent a single team's namespace from monopolizing the cluster.

##### 2️⃣ Remediation & Permanent Safeguards

Why use it: Example: ---

```bash
limits:
- default:
    cpu: 500m
    memory: 256Mi
  defaultRequest:
    cpu: 100m
    memory: 128Mi
  type: Container
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Prevent runaway pods — without limits, one pod can consume all node CPU/memory..

#### ⏱️ 60-Second Elevator Pitch Summary

- Prevent runaway pods — without limits, one pod can consume all node CPU/memory.
- Ensure HPA works — HPA needs resource requests set. LimitRange auto-sets them.
- Fair resource sharing — prevent a single team's namespace from monopolizing the cluster.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-69-kubernetes-q49-you-have-a-multi-tenant-cluster-where-different-teams-share-the-cluster-how-do-you-isolate-them-l3"></a>
### 69. Kubernetes Q49: You have a multi-tenant cluster where different teams share the cluster How do you isolate them [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You have a multi-tenant cluster where different teams share the cluster. How do you isolate them?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Soft multi-tenancy in Kubernetes (hard isolation requires separate clusters):

- **Namespaces** — one namespace per team.
- **RBAC** — teams can only access their own namespace.
- **ResourceQuotas** — limit total CPU/memory/pods per namespace.
- **LimitRanges** — default limits per pod/container.

##### 2️⃣ Remediation & Permanent Safeguards

True hard isolation (different teams can't see each other's API resources at all) requires separate clusters or a multi-tenant solution like vCluster. ---

- **NetworkPolicies** — namespace-to-namespace traffic blocked by default.
- **Pod Security Admission** — enforce security baselines (no privileged pods, no hostPath, etc.).
- **OPA/Gatekeeper or Kyverno** — custom policy enforcement (e.g., all images must come from internal registry).

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Namespaces — one namespace per team..

#### ⏱️ 60-Second Elevator Pitch Summary

- Namespaces — one namespace per team.
- RBAC — teams can only access their own namespace.
- ResourceQuotas — limit total CPU/memory/pods per namespace.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-70-kubernetes-q50-explain-the-difference-between-kubectl-apply-and-kubectl-create-when-would-you-use-each-l3"></a>
### 70. Kubernetes Q50: Explain the difference between kubectl apply and kubectl create When would you use each [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Explain the difference between `kubectl apply` and `kubectl create`. When would you use each?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

In CI/CD pipelines, always use `kubectl apply` — it's idempotent. Running the pipeline twice won't fail.

- **`kubectl create`** — imperative. Creates the resource. Fails if it already exists. Good for one-time resource creation.
- **`kubectl apply`** — declarative. Creates if not exists, updates if it does. Tracks changes using the `kubectl.kubernetes.io/last-applied-configuration` annotation. Good for GitOps and automation.

##### 2️⃣ Remediation & Permanent Safeguards

Use `kubectl create` when you specifically want the command to fail if the resource exists (e.g., to prevent accidental overwrites in a script). `kubectl apply` with `--server-side` (SSA) is the modern approach — the server handles merge strategy instead of the client annotation. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl create — imperative. Creates the resource. Fails if it already exists. Good for one-time resource creation..

#### ⏱️ 60-Second Elevator Pitch Summary

- kubectl create — imperative. Creates the resource. Fails if it already exists. Good for one-time ...
- kubectl apply — declarative. Creates if not exists, updates if it does. Tracks changes using the ...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-71-kubernetes-q51-your-readiness-probe-keeps-failing-even-though-the-app-is-working-fine-what-could-be-wrong-l2"></a>
### 71. Kubernetes Q51: Your readiness probe keeps failing even though the app is working fine What could be wrong [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your readiness probe keeps failing even though the app is working fine. What could be wrong?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Debug: `kubectl describe pod` shows probe failure reason. Also exec into the pod and manually curl the readiness endpoint to see what it returns.

- **Wrong port or path** — probe is checking a different port/endpoint than the app actually serves.
- **Probe timeout too short** — if the app takes 2 seconds to respond and `timeoutSeconds: 1`, it always times out.
- **App returns non-200 for the health path under load** — the readiness endpoint has a bug.

##### 2️⃣ Remediation & Permanent Safeguards

---

- **initialDelaySeconds too short** — app needs more time to start before readiness checks begin.
- **Checking the wrong container port name** — if using `port: http` and the port isn't named, it fails.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Wrong port or path — probe is checking a different port/endpoint than the app actually serves..

#### ⏱️ 60-Second Elevator Pitch Summary

- Wrong port or path — probe is checking a different port/endpoint than the app actually serves.
- Probe timeout too short — if the app takes 2 seconds to respond and timeoutSeconds: 1, it always ...
- App returns non-200 for the health path under load — the readiness endpoint has a bug.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-72-kubernetes-q52-what-is-the-difference-between-liveness-and-readiness-probes-give-a-scenario-where-each-is-important-l2"></a>
### 72. Kubernetes Q52: What is the difference between liveness and readiness probes Give a scenario where each is important [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the difference between liveness and readiness probes? Give a scenario where each is important."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Key: failed liveness = restart. Failed readiness = remove from load balancer rotation, but don't restart.

- **Liveness probe** — "is this container still alive?" If it fails, Kubernetes restarts the container. Use for detecting deadlocks or infinite loops where the process is running but not making progress.
- Scenario: A Java app has a thread deadlock. The JVM is running but requests hang forever. Liveness probe detects no HTTP response → restarts container.
- **Readiness probe** — "is this container ready to serve traffic?" If it fails, the pod is removed from Service endpoints. Use for apps that need warmup time or temporarily can't serve (e.g., during a DB connection retry).

##### 2️⃣ Remediation & Permanent Safeguards

---

- Scenario: App just started and is loading a 5GB ML model. Readiness fails until load completes. No traffic is sent yet. App is not restarted (liveness probe is fine).

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Liveness probe — "is this container still alive?" If it fails, Kubernetes restarts the container. Use for detecting deadlocks or i.

#### ⏱️ 60-Second Elevator Pitch Summary

- Liveness probe — "is this container still alive?" If it fails, Kubernetes restarts the container....
- Scenario: A Java app has a thread deadlock. The JVM is running but requests hang forever. Livenes...
- Readiness probe — "is this container ready to serve traffic?" If it fails, the pod is removed fro...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-73-kubernetes-q53-describe-the-pod-lifecycle-from-kubectl-apply-to-the-app-serving-traffic-l3"></a>
### 73. Kubernetes Q53: Describe the pod lifecycle from kubectl apply to the app serving traffic [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Describe the pod lifecycle from `kubectl apply` to the app serving traffic."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

---

- **API server** receives the pod spec, validates it, stores it in etcd. Pod status: `Pending`.
- **kube-scheduler** notices the unscheduled pod, runs filtering + scoring, writes the `nodeName` to the pod spec.
- **kubelet on the chosen node** watches for pods assigned to it. Sees the new pod.
- **kubelet calls the CRI** (Container Runtime Interface — containerd/CRI-O) to pull the image.
- **Init containers run** sequentially to completion.

##### 2️⃣ Remediation & Permanent Safeguards

Execute the resolution runbook and verify workload health:

- **Main containers start**. `postStart` lifecycle hook runs if defined.
- **Liveness and readiness probes start** (after `initialDelaySeconds`).
- Once **readiness probe passes**, kube-proxy adds the pod IP to the Service endpoints.
- **Traffic flows** to the pod.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: API server receives the pod spec, validates it, stores it in etcd. Pod status: Pending..

#### ⏱️ 60-Second Elevator Pitch Summary

- API server receives the pod spec, validates it, stores it in etcd. Pod status: Pending.
- kube-scheduler notices the unscheduled pod, runs filtering + scoring, writes the nodeName to the ...
- kubelet on the chosen node watches for pods assigned to it. Sees the new pod.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-74-kubernetes-q54-someone-applied-a-bad-networkpolicy-thats-blocking-all-traffic-in-the-cluster-how-do-you-recover-l2"></a>
### 74. Kubernetes Q54: Someone applied a bad NetworkPolicy thats blocking all traffic in the cluster How do you recover [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Someone applied a bad NetworkPolicy that's blocking all traffic in the cluster. How do you recover?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Prevention:

- **Identify the policy**: `kubectl get networkpolicy -A` — list all NetworkPolicies across namespaces.
- **Delete the bad one**: `kubectl delete networkpolicy  -n `.
- Traffic should restore immediately after deletion (NetworkPolicy is applied in near-real-time by the CNI plugin).
- Always test NetworkPolicy changes in a staging namespace first.

##### 2️⃣ Remediation & Permanent Safeguards

---

- Use `kubectl apply --dry-run=server` to validate.
- For complex policies, use tools like Cilium's policy editor to visualize impact before applying.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Identify the policy: kubectl get networkpolicy -A — list all NetworkPolicies across namespaces..

#### ⏱️ 60-Second Elevator Pitch Summary

- Identify the policy: kubectl get networkpolicy -A — list all NetworkPolicies across namespaces.
- Delete the bad one: kubectl delete networkpolicy  -n .
- Traffic should restore immediately after deletion (NetworkPolicy is applied in near-real-time by ...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-75-kubernetes-q55-what-is-the-role-of-etcd-in-kubernetes-and-what-happens-if-etcd-goes-down-l3"></a>
### 75. Kubernetes Q55: What is the role of etcd in Kubernetes and what happens if etcd goes down [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the role of etcd in Kubernetes and what happens if etcd goes down?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

etcd is the key-value store that is Kubernetes' "brain." Every cluster state (pod specs, node info, secrets, configmaps, events) is stored in etcd.

- **Existing pods keep running** — kubelet runs pods independently of the API server.
- **No new pods can be created** — API server can't write new state.
- **No changes work** — no scaling, no new deployments, no config changes.

##### 2️⃣ Remediation & Permanent Safeguards

If etcd goes down: Recovery: restore etcd from a snapshot backup. This is why etcd backups are critical (using `etcdctl snapshot save`). Production setup: etcd should have an **odd number of nodes (3, 5)** for quorum. With 3 nodes, cluster can tolerate 1 failure. With 5 nodes, 2 failures. ---

- **The cluster is effectively read-only and frozen**.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Existing pods keep running — kubelet runs pods independently of the API server..

#### ⏱️ 60-Second Elevator Pitch Summary

- Existing pods keep running — kubelet runs pods independently of the API server.
- No new pods can be created — API server can't write new state.
- No changes work — no scaling, no new deployments, no config changes.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-76-kubernetes-q56-how-do-you-pass-sensitive-configuration-like-db-passwords-to-a-pod-without-hardcoding-them-l2"></a>
### 76. Kubernetes Q56: How do you pass sensitive configuration (like DB passwords) to a pod without hardcoding them [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you pass sensitive configuration (like DB passwords) to a pod without hardcoding them?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Use **Kubernetes Secrets**:

- Create a secret: `kubectl create secret generic db-creds --from-literal=password=mypassword`
- Reference in pod as env var:

##### 2️⃣ Remediation & Permanent Safeguards

Or mount as a file: File mounting is more secure — env vars can leak in logs and process listings. Also avoid printing env vars in app error messages. ---

```bash
env:
- name: DB_PASSWORD
  valueFrom:
    secretKeyRef:
      name: db-creds
      key: password
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Create a secret: kubectl create secret generic db-creds --from-literal=password=mypassword.

#### ⏱️ 60-Second Elevator Pitch Summary

- Create a secret: kubectl create secret generic db-creds --from-literal=password=mypassword
- Reference in pod as env var:

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-77-kubernetes-q57-you-need-to-run-a-pod-that-requires-access-to-the-host-network-like-a-network-monitoring-tool-how-do-you-configure-this-l3"></a>
### 77. Kubernetes Q57: You need to run a pod that requires access to the host network (like a network monitoring tool) How do you configure this [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You need to run a pod that requires access to the host network (like a network monitoring tool). How do you configure this?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

`hostNetwork: true` makes the pod share the node's network namespace. It can bind to host ports and see all host network interfaces.

- The pod can sniff all traffic on the node.
- Port conflicts — if the pod binds port 80, it conflicts with anything else on port 80 on the host.
- Should only be used for legitimate infrastructure tools (network debuggers, CNI components).

##### 2️⃣ Remediation & Permanent Safeguards

Security implications: ---

- Block with PSA policy in production namespaces.

```bash
spec:
  hostNetwork: true
  hostPID: true  # if also needs host PID namespace
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: The pod can sniff all traffic on the node..

#### ⏱️ 60-Second Elevator Pitch Summary

- The pod can sniff all traffic on the node.
- Port conflicts — if the pod binds port 80, it conflicts with anything else on port 80 on the host.
- Should only be used for legitimate infrastructure tools (network debuggers, CNI components).

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-78-kubernetes-q58-explain-the-concept-of-resource-requests-vs-limits-what-happens-if-you-only-set-limits-and-not-requests-l2"></a>
### 78. Kubernetes Q58: Explain the concept of resource requests vs limits What happens if you only set limits and not requests [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Explain the concept of resource requests vs limits. What happens if you only set limits and not requests?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

If you only set limits and not requests: Kubernetes sets requests equal to limits. This can make scheduling harder because the scheduler thinks each pod needs the full limit amount even if actual usage is much less.

- **Request** — the guaranteed amount. Scheduler uses this to decide which node has enough room.
- **Limit** — the maximum. Container is throttled (CPU) or killed (memory) if it exceeds this.
- Set requests accurately based on average usage.

##### 2️⃣ Remediation & Permanent Safeguards

If you set neither: pod gets `BestEffort` QoS class — it's the first to be evicted under node memory pressure. Recommended practice: ---

- Set limits higher to allow burst.
- For CPU: it's okay to have a 5x ratio. For memory: be careful — exceeding limit = OOM kill.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Request — the guaranteed amount. Scheduler uses this to decide which node has enough room..

#### ⏱️ 60-Second Elevator Pitch Summary

- Request — the guaranteed amount. Scheduler uses this to decide which node has enough room.
- Limit — the maximum. Container is throttled (CPU) or killed (memory) if it exceeds this.
- Set requests accurately based on average usage.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-79-kubernetes-q59-what-are-the-three-qos-classes-in-kubernetes-and-how-does-each-affect-eviction-l3"></a>
### 79. Kubernetes Q59: What are the three QoS classes in Kubernetes and how does each affect eviction [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What are the three QoS classes in Kubernetes and how does each affect eviction?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

When a node runs out of memory, kubelet evicts pods in this order: BestEffort → Burstable (lowest priority score first) → Guaranteed.

- **Guaranteed** — `requests == limits` for all containers. Both CPU and memory. Highest priority. Evicted last.
- **Burstable** — at least one container has requests < limits, or not all containers have both set. Medium priority.
- **BestEffort** — no requests or limits set at all. Lowest priority. Evicted first when node is under memory pressure.

##### 2️⃣ Remediation & Permanent Safeguards

For critical production workloads: use **Guaranteed** QoS (set requests = limits for memory at minimum) to protect them from eviction. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Guaranteed — requests == limits for all containers. Both CPU and memory. Highest priority. Evicted last..

#### ⏱️ 60-Second Elevator Pitch Summary

- Guaranteed — requests == limits for all containers. Both CPU and memory. Highest priority. Evicte...
- Burstable — at least one container has requests < limits, or not all containers have both set. Me...
- BestEffort — no requests or limits set at all. Lowest priority. Evicted first when node is under ...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-80-kubernetes-q60-you-have-a-multi-container-pod-sidecar-pattern-how-do-the-containers-share-data-with-each-other-l2"></a>
### 80. Kubernetes Q60: You have a multi-container pod (sidecar pattern) How do the containers share data with each other [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You have a multi-container pod (sidecar pattern). How do the containers share data with each other?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Containers in the same pod share:

- **Network namespace** — they can communicate via `localhost`. If container A serves on port 8080, container B can reach it at `localhost:8080`.
- **Volumes** — mount a shared `emptyDir` volume. Both containers read/write to the same directory.

##### 2️⃣ Remediation & Permanent Safeguards

Example use case — log shipping sidecar: main app writes logs to `/var/log/app` (emptyDir volume), Fluentd sidecar reads from the same path and ships to Elasticsearch. They do NOT share the filesystem by default — only through shared volumes. --- **Q61-Q100 — Additional Kubernetes Scenarios** ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Network namespace — they can communicate via localhost. If container A serves on port 8080, container B can reach it at localhost:.

#### ⏱️ 60-Second Elevator Pitch Summary

- Network namespace — they can communicate via localhost. If container A serves on port 8080, conta...
- Volumes — mount a shared emptyDir volume. Both containers read/write to the same directory.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-81-kubernetes-q61-what-is-the-difference-between-emptydir-and-hostpath-volumes-l2"></a>
### 81. Kubernetes Q61: What is the difference between emptyDir and hostPath volumes [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the difference between `emptyDir` and `hostPath` volumes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Use `emptyDir` for temporary shared data. Avoid `hostPath` in production unless absolutely necessary (e.g., running Docker-in-Docker or accessing host logs).

- `emptyDir` — temporary directory created when pod starts, deleted when pod is removed. Shared between containers in the pod. Good for scratch space or sidecar data sharing.
- `hostPath` — mounts a path from the host node's filesystem. Survives pod restarts as long as the pod stays on the same node. Risky in production — pod is now tied to a specific node and can access host files.

##### 2️⃣ Remediation & Permanent Safeguards

---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: emptyDir — temporary directory created when pod starts, deleted when pod is removed. Shared between containers in the pod. Good fo.

#### ⏱️ 60-Second Elevator Pitch Summary

- emptyDir — temporary directory created when pod starts, deleted when pod is removed. Shared betwe...
- hostPath — mounts a path from the host node's filesystem. Survives pod restarts as long as the po...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-82-kubernetes-q62-a-cluster-autoscaler-is-not-scaling-up-even-though-pods-are-pending-what-could-be-wrong-l3"></a>
### 82. Kubernetes Q62: A cluster-autoscaler is not scaling up even though pods are Pending What could be wrong [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A cluster-autoscaler is not scaling up even though pods are Pending. What could be wrong?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Check: CA logs — `kubectl logs -n kube-system ` — it logs exactly why it's not scaling.

- **Pod is unschedulable for a reason other than resources** — e.g., node affinity requires a specific label that no node type has. CA won't add nodes it can't schedule the pod on.
- **Max node count reached** — CA has a configured max. `--max-nodes-total` or per-node-group limit.
- **Pod has `cluster-autoscaler.kubernetes.io/safe-to-evict: false`** — CA may refuse to scale if eviction of existing pods is blocked.
- **Cooldown period** — CA has a scale-up cooldown (default 10 min). May be waiting.

##### 2️⃣ Remediation & Permanent Safeguards

---

- **Budget exhausted** — cloud account has hit EC2/VM quota.
- **CA can't provision the requested instance type** — spot capacity unavailable.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Pod is unschedulable for a reason other than resources — e.g., node affinity requires a specific label that no node type has. CA w.

#### ⏱️ 60-Second Elevator Pitch Summary

- Pod is unschedulable for a reason other than resources — e.g., node affinity requires a specific ...
- Max node count reached — CA has a configured max. --max-nodes-total or per-node-group limit.
- Pod has cluster-autoscaler.kubernetes.io/safe-to-evict: false — CA may refuse to scale if evictio...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-83-kubernetes-q63-how-do-you-roll-back-a-helm-release-l2"></a>
### 83. Kubernetes Q63: How do you roll back a Helm release [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you roll back a Helm release?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Helm keeps a history of all deployed revisions (stored as Secrets in the namespace). Each revision has a snapshot of the values and chart used. If `--history-max` is set, older revisions are pruned automatically, limiting how far back you can roll. ---

```bash
helm history <release-name>         # see all revisions
helm rollback <release-name> 2      # roll back to revision 2
helm rollback <release-name>        # roll back to previous revision
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Helm keeps a history of all deployed revisions (stored as Secrets in the namespace). Each revision has a snapshot of the values an.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: bash
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-84-kubernetes-q64-what-is-helm-and-why-is-it-used-instead-of-raw-yaml-l2"></a>
### 84. Kubernetes Q64: What is Helm and why is it used instead of raw YAML [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is Helm and why is it used instead of raw YAML?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Helm is a package manager for Kubernetes. A Helm chart bundles all the Kubernetes YAML for an application (Deployment, Service, ConfigMap, Ingress, etc.) with templating.

- **Reusability** — parameterize with values instead of duplicating YAML per environment.
- **Versioning** — charts have versions. Rollback to a previous chart version.
- **Dependency management** — a chart can depend on other charts (e.g., your app chart depends on a Redis chart).

##### 2️⃣ Remediation & Permanent Safeguards

Why use it: Downside: Helm templates can get complex. For simpler cases, Kustomize is often cleaner. ---

- **Community charts** — Artifact Hub has thousands of pre-built charts for common software.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Reusability — parameterize with values instead of duplicating YAML per environment..

#### ⏱️ 60-Second Elevator Pitch Summary

- Reusability — parameterize with values instead of duplicating YAML per environment.
- Versioning — charts have versions. Rollback to a previous chart version.
- Dependency management — a chart can depend on other charts (e.g., your app chart depends on a Red...

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-85-kubernetes-q65-explain-how-kubernetes-handles-pod-eviction-during-node-memory-pressure-l3"></a>
### 85. Kubernetes Q65: Explain how Kubernetes handles pod eviction during node memory pressure [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Explain how Kubernetes handles pod eviction during node memory pressure."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

kubelet monitors node memory usage against eviction thresholds:

- **Soft eviction** — e.g., `memory.available < 500Mi`. kubelet gives pods a grace period (`eviction-soft-grace-period`, default 90s) to shut down before killing.
- **Hard eviction** — e.g., `memory.available < 100Mi`. kubelet immediately kills pods with no grace period.
- BestEffort pods first.

##### 2️⃣ Remediation & Permanent Safeguards

Eviction order: After eviction, the node reports `MemoryPressure` condition and is tainted. New pods won't schedule there until pressure resolves. ---

- Burstable pods that exceed their memory request (most over request first).
- Guaranteed pods (last resort).

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Soft eviction — e.g., memory.available . kubelet gives pods a grace period (eviction-soft-grace-period, default 90s) to shut down .

#### ⏱️ 60-Second Elevator Pitch Summary

- Soft eviction — e.g., memory.available . kubelet gives pods a grace period (eviction-soft-grace-p...
- Hard eviction — e.g., memory.available . kubelet immediately kills pods with no grace period.
- BestEffort pods first.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-86-kubernetes-q66-what-is-the-purpose-of-terminationgraceperiodseconds-l2"></a>
### 86. Kubernetes Q66: What is the purpose of terminationGracePeriodSeconds [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the purpose of `terminationGracePeriodSeconds`?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

When a pod is deleted, Kubernetes sends `SIGTERM` to the container and waits `terminationGracePeriodSeconds` (default: 30s) for the app to shut down gracefully. After the grace period, `SIGKILL` is sent.

- Your app should handle `SIGTERM` by finishing in-flight requests and closing connections before exiting.
- If your app needs more than 30s to drain (e.g., it's processing long jobs), increase the grace period.
- If `preStop` hook is defined, it runs before SIGTERM and counts against the grace period.

##### 2️⃣ Remediation & Permanent Safeguards

Why it matters: For web servers: graceful shutdown means finishing current HTTP requests. For consumers: finish processing the current message before stopping. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Your app should handle SIGTERM by finishing in-flight requests and closing connections before exiting..

#### ⏱️ 60-Second Elevator Pitch Summary

- Your app should handle SIGTERM by finishing in-flight requests and closing connections before exi...
- If your app needs more than 30s to drain (e.g., it's processing long jobs), increase the grace pe...
- If preStop hook is defined, it runs before SIGTERM and counts against the grace period.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-87-kubernetes-q67-you-need-to-run-a-pod-that-will-only-start-after-a-specific-configmap-exists-in-the-cluster-how-do-you-implement-this-l3"></a>
### 87. Kubernetes Q67: You need to run a pod that will only start after a specific ConfigMap exists in the cluster How do you implement this [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You need to run a pod that will only start after a specific ConfigMap exists in the cluster. How do you implement this?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use an **init container** that polls for the ConfigMap: The init container keeps checking every 5 seconds until the ConfigMap exists, then exits (allowing the main container to start). This pattern is common for sequencing: wait for a database to be ready, wait for a service to exist, wait for a secret to be populated. ---

```bash
initContainers:
- name: wait-for-config
  image: bitnami/kubectl
  command: ['sh', '-c', 'until kubectl get configmap my-config; do echo waiting; sleep 5; done']
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use an init container that polls for the ConfigMap:.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use an init container that polls for the ConfigMap:
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-88-kubernetes-q68-what-is-the-purpose-of-podantiaffinity-with-topologykey-topologykubernetesio-zone-l2"></a>
### 88. Kubernetes Q68: What is the purpose of podAntiAffinity with topologyKey topologykubernetesio/zone [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the purpose of `podAntiAffinity` with `topologyKey: topology.kubernetes.io/zone`?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

This spreads pods across availability zones rather than just across nodes. If your cluster spans 3 AZs (us-east-1a, 1b, 1c), this anti-affinity ensures no two pods of the same app land in the same AZ. Why: Even with node anti-affinity, all your "different nodes" could be in the same AZ. If that AZ goes down, you lose everything. Zone-spread anti-affinity ensures true high availability across data center failures. Combine with `topologySpreadConstraints` for finer control over pod distribution across zones and nodes. ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: This spreads pods across availability zones rather than just across nodes. If your cluster spans 3 AZs (us-east-1a, 1b, 1c), this .

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: This spreads pods across availability zones rather than just across nodes. If your cluster span
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-89-kubernetes-q69-describe-the-container-storage-interface-csi-and-why-it-replaced-in-tree-volume-plugins-l3"></a>
### 89. Kubernetes Q69: Describe the Container Storage Interface (CSI) and why it replaced in-tree volume plugins [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Describe the Container Storage Interface (CSI) and why it replaced in-tree volume plugins."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

In-tree volume plugins (like the old AWS EBS plugin built into kubelet) had problems:

- They had to be updated with Kubernetes releases.
- Bugs in storage plugins could crash kubelet.
- Storage vendors couldn't release independently of Kubernetes.
- PVC created → external-provisioner (CSI sidecar) calls the CSI driver to provision a volume.

##### 2️⃣ Remediation & Permanent Safeguards

**CSI (Container Storage Interface)** is a standard API that lets storage vendors write drivers that run as pods in the cluster, independent of Kubernetes core. Flow: Vendors like AWS (EBS CSI), Azure Disk, GCP PD, and Portworx all now have CSI drivers. In-tree plugins are deprecated and being removed. ---

- Pod scheduled → node-driver-registrar mounts the volume on the node.
- Container starts with the volume attached.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: They had to be updated with Kubernetes releases..

#### ⏱️ 60-Second Elevator Pitch Summary

- They had to be updated with Kubernetes releases.
- Bugs in storage plugins could crash kubelet.
- Storage vendors couldn't release independently of Kubernetes.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-90-kubernetes-q70-what-is-a-mutating-admission-webhook-and-give-a-practical-use-case-l3"></a>
### 90. Kubernetes Q70: What is a mutating admission webhook and give a practical use case [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a mutating admission webhook and give a practical use case?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Admission webhooks intercept API requests before they're stored in etcd. **Mutating** webhooks can modify the request (add/change fields). **Validating** webhooks can accept or reject it.

- **Istio/Linkerd sidecar injection** — automatically inject the sidecar proxy container into every pod in labeled namespaces.
- **Default resource limits** — if a pod has no resource limits, auto-add safe defaults.
- **Label injection** — add team/cost-center labels to all pods.

##### 2️⃣ Remediation & Permanent Safeguards

Practical use cases for mutating webhooks: The webhook is an HTTPS server (usually running as a pod). Kubernetes sends the resource spec to it, the server returns a JSON Patch with modifications. --- **Q71-Q100. Rapid-fire Kubernetes Scenarios**

- **Image tag enforcement** — replace `latest` tag with the actual SHA digest.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Istio/Linkerd sidecar injection — automatically inject the sidecar proxy container into every pod in labeled namespaces..

#### ⏱️ 60-Second Elevator Pitch Summary

- Istio/Linkerd sidecar injection — automatically inject the sidecar proxy container into every pod...
- Default resource limits — if a pod has no resource limits, auto-add safe defaults.
- Label injection — add team/cost-center labels to all pods.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-91-kubernetes-q71-pod-shows-errimagepull-l1"></a>
### 91. Kubernetes Q71: Pod shows ErrImagePull [L1]

**Level:** `Junior / Associate DevOps [L1]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Core Fundamentals [L1]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L1` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Pod shows `ErrImagePull`."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Image not found or wrong tag. Check image name/tag. For private registry, ensure imagePullSecret is configured.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Image not found or wrong tag. Check image name/tag. For private registry, ensure imagePullSecret is configured..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Image not found or wrong tag. Check image name/tag. For private registry, ensure imagePullSecre
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-92-kubernetes-q72-deployment-has-0-ready-pods-but-desired-is-3-l2"></a>
### 92. Kubernetes Q72: Deployment has 0 ready pods but desired is 3 [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Deployment has 0 ready pods but desired is 3."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

All pods failing readiness. Check probe config and app logs.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: All pods failing readiness. Check probe config and app logs..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: All pods failing readiness. Check probe config and app logs.
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-93-kubernetes-q73-how-do-you-scale-a-deployment-to-5-replicas-l1"></a>
### 93. Kubernetes Q73: How do you scale a deployment to 5 replicas [L1]

**Level:** `Junior / Associate DevOps [L1]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Core Fundamentals [L1]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L1` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you scale a deployment to 5 replicas?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`kubectl scale deployment  --replicas=5` or update spec.replicas.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl scale deployment  --replicas=5 or update spec.replicas..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: kubectl scale deployment  --replicas=5 or update spec.replicas.
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-94-kubernetes-q74-nodeport-service-not-reachable-from-outside-l2"></a>
### 94. Kubernetes Q74: NodePort service not reachable from outside [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"NodePort service not reachable from outside."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Check firewall/security group rules allow the NodePort (30000-32767) range.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Check firewall/security group rules allow the NodePort (30000-32767) range..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Check firewall/security group rules allow the NodePort (30000-32767) range.
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-95-kubernetes-q75-two-pods-cant-communicate-even-though-networkpolicy-allows-it-l2"></a>
### 95. Kubernetes Q75: Two pods cant communicate even though NetworkPolicy allows it [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Two pods can't communicate even though NetworkPolicy allows it."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

CNI plugin may not support NetworkPolicy. Check CNI (Flannel doesn't, Calico does).

#### 🎯 Key Architectural Takeaway
> Pro-Tip: CNI plugin may not support NetworkPolicy. Check CNI (Flannel doesn't, Calico does)..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: CNI plugin may not support NetworkPolicy. Check CNI (Flannel doesn't, Calico does).
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-96-kubernetes-q76-how-do-you-upgrade-kubernetes-version-with-zero-downtime-l3"></a>
### 96. Kubernetes Q76: How do you upgrade Kubernetes version with zero downtime [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you upgrade Kubernetes version with zero downtime?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Upgrade control plane first (API server, etcd, scheduler). Then drain, upgrade, uncordon worker nodes one by one.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Upgrade control plane first (API server, etcd, scheduler). Then drain, upgrade, uncordon worker nodes one by one..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Upgrade control plane first (API server, etcd, scheduler). Then drain, upgrade, uncordon worker
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-97-kubernetes-q77-ingress-shows-address-pending-l2"></a>
### 97. Kubernetes Q77: Ingress shows Address <pending> [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Ingress shows `Address: `."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

No LoadBalancer IP assigned yet. On bare-metal, need MetalLB. On cloud, wait 1-2 min for cloud LB provisioning.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: No LoadBalancer IP assigned yet. On bare-metal, need MetalLB. On cloud, wait 1-2 min for cloud LB provisioning..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: No LoadBalancer IP assigned yet. On bare-metal, need MetalLB. On cloud, wait 1-2 min for cloud
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-98-kubernetes-q78-how-do-you-get-logs-from-all-pods-of-a-deployment-l1"></a>
### 98. Kubernetes Q78: How do you get logs from all pods of a deployment [L1]

**Level:** `Junior / Associate DevOps [L1]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Core Fundamentals [L1]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L1` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you get logs from all pods of a deployment?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`kubectl logs -l app=` or use label selector.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl logs -l app= or use label selector..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: kubectl logs -l app= or use label selector.
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-99-kubernetes-q79-horizontal-pod-autoscaler-shows-unknown-50-for-current-metric-l2"></a>
### 99. Kubernetes Q79: Horizontal Pod Autoscaler shows unknown/50% for current metric [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Horizontal Pod Autoscaler shows `unknown/50%` for current metric."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

metrics-server not installed or pods have no resource requests set.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: metrics-server not installed or pods have no resource requests set..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: metrics-server not installed or pods have no resource requests set.
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-100-kubernetes-q80-etcd-backup-failed-recovery-steps-l3"></a>
### 100. Kubernetes Q80: etcd backup failed Recovery steps [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"etcd backup failed. Recovery steps?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`etcdctl snapshot save backup.db`. Restore: stop API server, restore snapshot, restart.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: etcdctl snapshot save backup.db. Restore: stop API server, restore snapshot, restart..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: etcdctl snapshot save backup.db. Restore: stop API server, restore snapshot, restart.
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-101-kubernetes-q81-a-developer-accidentally-deleted-a-namespace-how-do-you-recover-l2"></a>
### 101. Kubernetes Q81: A developer accidentally deleted a namespace How do you recover [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A developer accidentally deleted a namespace. How do you recover?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

From backup/GitOps. There's no undo in kubectl. This is why GitOps (ArgoCD/Flux) matters — re-apply the Git state.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: From backup/GitOps. There's no undo in kubectl. This is why GitOps (ArgoCD/Flux) matters — re-apply the Git state..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: From backup/GitOps. There's no undo in kubectl. This is why GitOps (ArgoCD/Flux) matters — re-a
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-102-kubernetes-q82-pod-shows-terminating-for-hours-and-wont-delete-l2"></a>
### 102. Kubernetes Q82: Pod shows Terminating for hours and wont delete [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Pod shows `Terminating` for hours and won't delete."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Force delete: `kubectl delete pod  --grace-period=0 --force`. Usually caused by finalizers or stuck volumes.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Force delete: kubectl delete pod  --grace-period=0 --force. Usually caused by finalizers or stuck volumes..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Force delete: kubectl delete pod  --grace-period=0 --force. Usually caused by finalizers or stu
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-103-kubernetes-q83-service-mesh-vs-networkpolicy-when-do-you-use-each-l3"></a>
### 103. Kubernetes Q83: Service mesh vs NetworkPolicy — when do you use each [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Service mesh vs NetworkPolicy — when do you use each?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

NetworkPolicy = L3/L4 (IP/port). Service mesh (Istio/Linkerd) = L7 (HTTP routing, mTLS, retries, circuit breaking). Use both for layered security.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: NetworkPolicy = L3/L4 (IP/port). Service mesh (Istio/Linkerd) = L7 (HTTP routing, mTLS, retries, circuit breaking). Use both for l.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: NetworkPolicy = L3/L4 (IP/port). Service mesh (Istio/Linkerd) = L7 (HTTP routing, mTLS, retries
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-104-kubernetes-q84-how-do-you-make-a-pod-restart-on-config-change-without-a-code-change-l2"></a>
### 104. Kubernetes Q84: How do you make a pod restart on config change without a code change [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you make a pod restart on config change without a code change?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Add annotation with configmap hash: `checksum/config: {{ include (print .Template.BasePath "/configmap.yaml") . | sha256sum }}` in Helm. Or use Reloader operator.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Add annotation with configmap hash: checksum/config: {{ include (print .Template.BasePath "/configmap.yaml") . | sha256sum }} in H.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Add annotation with configmap hash: checksum/config: {{ include (print .Template.BasePath "/con
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-105-kubernetes-q85-a-cronjob-job-ran-but-the-pod-isnt-showing-in-kubectl-get-jobs-l2"></a>
### 105. Kubernetes Q85: A CronJob job ran but the pod isnt showing in kubectl get jobs [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A CronJob job ran but the pod isn't showing in `kubectl get jobs`."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`successfulJobsHistoryLimit` may be 0 or 1 and old jobs were cleaned. Adjust to keep history.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: successfulJobsHistoryLimit may be 0 or 1 and old jobs were cleaned. Adjust to keep history..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: successfulJobsHistoryLimit may be 0 or 1 and old jobs were cleaned. Adjust to keep history.
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-106-kubernetes-q86-your-admission-webhook-is-blocking-all-pod-creation-cluster-wide-how-do-you-recover-l3"></a>
### 106. Kubernetes Q86: Your admission webhook is blocking all pod creation cluster-wide How do you recover [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Your admission webhook is blocking all pod creation cluster-wide. How do you recover?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

If webhook server is down, set `failurePolicy: Ignore` on the webhook or delete the `MutatingWebhookConfiguration` object.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: If webhook server is down, set failurePolicy: Ignore on the webhook or delete the MutatingWebhookConfiguration object..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: If webhook server is down, set failurePolicy: Ignore on the webhook or delete the MutatingWebho
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-107-kubernetes-q87-how-do-you-check-if-a-service-account-has-permission-to-create-pods-l2"></a>
### 107. Kubernetes Q87: How do you check if a service account has permission to create pods [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you check if a service account has permission to create pods?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`kubectl auth can-i create pods --as=system:serviceaccount::`

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl auth can-i create pods --as=system:serviceaccount::.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: kubectl auth can-i create pods --as=system:serviceaccount::
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-108-kubernetes-q88-what-is-the-difference-between-kubectl-get-and-kubectl-describe-l1"></a>
### 108. Kubernetes Q88: What is the difference between kubectl get and kubectl describe [L1]

**Level:** `Junior / Associate DevOps [L1]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Core Fundamentals [L1]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L1` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the difference between `kubectl get` and `kubectl describe`?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`get` = brief summary table. `describe` = full detail including events. Use describe for debugging.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: get = brief summary table. describe = full detail including events. Use describe for debugging..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: get = brief summary table. describe = full detail including events. Use describe for debugging.
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-109-kubernetes-q89-you-want-to-run-a-one-off-debug-pod-on-a-specific-node-how-l2"></a>
### 109. Kubernetes Q89: You want to run a one-off debug pod on a specific node How [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You want to run a one-off debug pod on a specific node. How?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`kubectl debug node/ -it --image=ubuntu` or use `nodeName` field in pod spec.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl debug node/ -it --image=ubuntu or use nodeName field in pod spec..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: kubectl debug node/ -it --image=ubuntu or use nodeName field in pod spec.
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-110-kubernetes-q90-explain-how-kube-proxy-implements-services-using-iptables-l3"></a>
### 110. Kubernetes Q90: Explain how kube-proxy implements Services using iptables [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Explain how kube-proxy implements Services using iptables."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

kube-proxy watches Services/Endpoints. Creates iptables DNAT rules: traffic to ClusterIP is redirected to one of the pod IPs using a round-robin probability chain.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kube-proxy watches Services/Endpoints. Creates iptables DNAT rules: traffic to ClusterIP is redirected to one of the pod IPs using.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: kube-proxy watches Services/Endpoints. Creates iptables DNAT rules: traffic to ClusterIP is red
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-111-kubernetes-q91-what-is-topology-spread-constraints-and-when-would-you-use-it-over-pod-anti-affinity-l2"></a>
### 111. Kubernetes Q91: What is topology spread constraints and when would you use it over pod anti-affinity [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is topology spread constraints and when would you use it over pod anti-affinity?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

TopologySpreadConstraints gives fine-grained control over pod distribution (e.g., max skew of 1 between zones). Anti-affinity is binary. Use topology spread for better distribution control.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: TopologySpreadConstraints gives fine-grained control over pod distribution (e.g., max skew of 1 between zones). Anti-affinity is b.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: TopologySpreadConstraints gives fine-grained control over pod distribution (e.g., max skew of 1
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-112-kubernetes-q92-a-pod-needs-gpu-resources-how-do-you-configure-it-l2"></a>
### 112. Kubernetes Q92: A pod needs GPU resources How do you configure it [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A pod needs GPU resources. How do you configure it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Node must have GPU + GPU device plugin installed. Pod requests: `resources.limits: nvidia.com/gpu: 1`. Scheduler finds a node with available GPU.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Node must have GPU + GPU device plugin installed. Pod requests: resources.limits: nvidia.com/gpu: 1. Scheduler finds a node with a.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Node must have GPU + GPU device plugin installed. Pod requests: resources.limits: nvidia.com/gp
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-113-kubernetes-q93-describe-leader-election-in-kubernetes-control-plane-components-l3"></a>
### 113. Kubernetes Q93: Describe leader election in Kubernetes control plane components [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Describe leader election in Kubernetes control plane components."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Scheduler and controller-manager use Lease objects in etcd. Only the leader processes work. Others watch. If leader fails to renew its lease, another takes over. Prevents split-brain in HA setups.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Scheduler and controller-manager use Lease objects in etcd. Only the leader processes work. Others watch. If leader fails to renew.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Scheduler and controller-manager use Lease objects in etcd. Only the leader processes work. Oth
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-114-kubernetes-q94-what-is-a-finalizer-and-when-would-you-use-one-l2"></a>
### 114. Kubernetes Q94: What is a finalizer and when would you use one [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a finalizer and when would you use one?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Finalizer is a string in `metadata.finalizers`. Prevents object deletion until the finalizer is removed. Use case: ensure external resources (cloud volumes, DNS records) are cleaned up before the Kubernetes object is deleted.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Finalizer is a string in metadata.finalizers. Prevents object deletion until the finalizer is removed. Use case: ensure external r.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Finalizer is a string in metadata.finalizers. Prevents object deletion until the finalizer is r
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-115-kubernetes-q95-how-does-the-kubernetes-garbage-collector-work-l3"></a>
### 115. Kubernetes Q95: How does the Kubernetes garbage collector work [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How does the Kubernetes garbage collector work?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Uses owner references. When a parent object (Deployment) is deleted, GC deletes owned objects (ReplicaSets → Pods) in cascade. `--cascade=orphan` flag leaves children running.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Uses owner references. When a parent object (Deployment) is deleted, GC deletes owned objects (ReplicaSets → Pods) in cascade. --c.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Uses owner references. When a parent object (Deployment) is deleted, GC deletes owned objects (
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-116-kubernetes-q96-how-do-you-run-a-privileged-debug-container-on-a-running-pod-without-modifying-the-pod-spec-l2"></a>
### 116. Kubernetes Q96: How do you run a privileged debug container on a running pod without modifying the pod spec [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you run a privileged debug container on a running pod without modifying the pod spec?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`kubectl debug -it  --image=ubuntu --share-processes --copy-to=debug-pod` — creates a copy of the pod with an extra debug container.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl debug -it  --image=ubuntu --share-processes --copy-to=debug-pod — creates a copy of the pod with an extra debug container..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: kubectl debug -it  --image=ubuntu --share-processes --copy-to=debug-pod — creates a copy of the
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-117-kubernetes-q97-what-is-the-kubernetes-watch-mechanism-and-how-do-informers-use-it-l3"></a>
### 117. Kubernetes Q97: What is the Kubernetes watch mechanism and how do informers use it [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the Kubernetes watch mechanism and how do informers use it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

The API server supports a `watch` query param. Client gets a stream of events (ADDED/MODIFIED/DELETED) instead of polling. Informers use this + a local cache to efficiently react to changes without hammering the API server.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: The API server supports a watch query param. Client gets a stream of events (ADDED/MODIFIED/DELETED) instead of polling. Informers.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: The API server supports a watch query param. Client gets a stream of events (ADDED/MODIFIED/DEL
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-118-kubernetes-q98-explain-the-difference-between-kubectl-apply-with-a-file-vs-kubectl-apply-k-kustomize-l2"></a>
### 118. Kubernetes Q98: Explain the difference between kubectl apply with a file vs kubectl apply -k (kustomize) [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Explain the difference between `kubectl apply` with a file vs `kubectl apply -k` (kustomize)."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`-f` applies a single file or directory of raw YAML. `-k` runs Kustomize, applying base + overlays, generating configs, and applying the merged result.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: -f applies a single file or directory of raw YAML. -k runs Kustomize, applying base + overlays, generating configs, and applying t.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: -f applies a single file or directory of raw YAML. -k runs Kustomize, applying base + overlays,
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-119-kubernetes-q99-how-would-you-migrate-a-stateful-workload-from-one-kubernetes-cluster-to-another-with-minimal-downtime-l3"></a>
### 119. Kubernetes Q99: How would you migrate a stateful workload from one Kubernetes cluster to another with minimal downtime [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How would you migrate a stateful workload from one Kubernetes cluster to another with minimal downtime?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

1) Snapshot PVC data (Velero). 2) Deploy workload in new cluster from same Git source. 3) Restore data snapshot to new cluster PVCs. 4) Test new cluster. 5) Switch DNS/load balancer to new cluster. 6) Decommission old cluster.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: 1) Snapshot PVC data (Velero). 2) Deploy workload in new cluster from same Git source. 3) Restore data snapshot to new cluster PVC.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: 1) Snapshot PVC data (Velero). 2) Deploy workload in new cluster from same Git source. 3) Resto
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-120-kubernetes-q100-what-is-keda-and-how-does-it-extend-hpa-l3"></a>
### 120. Kubernetes Q100: What is KEDA and how does it extend HPA [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Advanced Scenarios` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Advanced Scenarios` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is KEDA and how does it extend HPA?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

KEDA (Kubernetes Event-Driven Autoscaling) scales pods based on external event sources: Kafka topic lag, RabbitMQ queue depth, HTTP request rate, Azure Service Bus, AWS SQS, cron schedules. Standard HPA only uses CPU/memory. KEDA plugs in as a custom metrics source to HPA, enabling scale-to-zero and event-driven scaling. --- *More Kubernetes scenarios added periodically. PRs welcome.* --- ## 🟤 Additional Kubernetes Scenarios (Q101-Q200) ---

#### 🎯 Key Architectural Takeaway
> Pro-Tip: KEDA (Kubernetes Event-Driven Autoscaling) scales pods based on external event sources: Kafka topic lag, RabbitMQ queue depth, HTT.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: KEDA (Kubernetes Event-Driven Autoscaling) scales pods based on external event sources: Kafka t
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-121-kubernetes-q101-how-do-you-expose-a-grpc-service-in-kubernetes-l2"></a>
### 121. Kubernetes Q101: How do you expose a gRPC service in Kubernetes [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you expose a gRPC service in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use a Service with the correct port and protocol annotation. For Ingress: you need an ingress controller that supports gRPC (nginx-ingress with `nginx.ingress.kubernetes.io/backend-protocol: GRPC` annotation, or Istio). gRPC requires HTTP/2, so TLS is typically required. With Istio: define a VirtualService with gRPC routing rules.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use a Service with the correct port and protocol annotation. For Ingress: you need an ingress controller that supports gRPC (nginx.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use a Service with the correct port and protocol annotation. For Ingress: you need an ingress c
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-122-kubernetes-q102-explain-how-kubernetes-handles-rolling-back-a-daemonset-update-l3"></a>
### 122. Kubernetes Q102: Explain how Kubernetes handles rolling back a DaemonSet update [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Explain how Kubernetes handles rolling back a DaemonSet update."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

DaemonSets support `kubectl rollout undo daemonset/` similar to Deployments. DaemonSet keeps rollout history (configurable via `revisionHistoryLimit`). During rollback, it re-applies the previous pod template spec, updating nodes one by one based on `updateStrategy`. The main difference from Deployments: there's no concept of "unavailable" limit since each node must have exactly one pod.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: DaemonSets support kubectl rollout undo daemonset/ similar to Deployments. DaemonSet keeps rollout history (configurable via revis.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: DaemonSets support kubectl rollout undo daemonset/ similar to Deployments. DaemonSet keeps roll
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-123-kubernetes-q103-a-kubernetes-job-is-stuck-at-0-1-running-and-never-starts-what-do-you-check-l2"></a>
### 123. Kubernetes Q103: A Kubernetes Job is stuck at 0/1 Running and never starts What do you check [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A Kubernetes Job is stuck at "0/1 Running" and never starts. What do you check?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Same as any pod: `kubectl describe job `, check the created pod's events. Common issues: image pull error, no nodes with enough resources, node selector mismatch, parallelism setting. For Jobs with `completions > 1`, check if `parallelism` is set too low or if previous failed pods are blocking.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Same as any pod: kubectl describe job , check the created pod's events. Common issues: image pull error, no nodes with enough reso.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Same as any pod: kubectl describe job , check the created pod's events. Common issues: image pu
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-124-kubernetes-q104-how-do-you-configure-a-pod-to-get-secrets-from-hashicorp-vault-without-modifying-app-code-l2"></a>
### 124. Kubernetes Q104: How do you configure a pod to get secrets from HashiCorp Vault without modifying app code [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you configure a pod to get secrets from HashiCorp Vault without modifying app code?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use Vault Agent Injector (Vault installed in K8s). Annotate the pod: The Vault Agent sidecar is injected into the pod. It authenticates with Vault using K8s ServiceAccount token, fetches the secrets, and writes them to a shared volume at `/vault/secrets/`. App reads files. No code change needed.

```bash
annotations:
  vault.hashicorp.com/agent-inject: "true"
  vault.hashicorp.com/role: "my-app"
  vault.hashicorp.com/agent-inject-secret-config: "secret/data/myapp"
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use Vault Agent Injector (Vault installed in K8s). Annotate the pod:.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use Vault Agent Injector (Vault installed in K8s). Annotate the pod:
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-125-kubernetes-q105-what-is-the-kubernetes-control-loop-and-how-does-it-apply-to-custom-operators-l3"></a>
### 125. Kubernetes Q105: What is the Kubernetes control loop and how does it apply to custom operators [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the Kubernetes control loop and how does it apply to custom operators?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

The control loop pattern: watch current state → compare with desired state → take action to reconcile. Controllers (Deployment controller, ReplicaSet controller) do this continuously. Custom operators use the same pattern for custom resources. You define a Custom Resource Definition (CRD) and write a controller that watches those CRs and reconciles. Example: a PostgreSQL operator watches `Postgres` CRs and creates/manages actual Postgres pods, services, and backups. Tools: kubebuilder, Operator SDK.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: The control loop pattern: watch current state → compare with desired state → take action to reconcile. Controllers (Deployment con.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: The control loop pattern: watch current state → compare with desired state → take action to rec
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-126-kubernetes-q106-how-do-you-restrict-a-pod-from-accessing-the-cloud-metadata-endpoint-eg-169254169254-l2"></a>
### 126. Kubernetes Q106: How do you restrict a pod from accessing the cloud metadata endpoint (eg 169254169254) [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you restrict a pod from accessing the cloud metadata endpoint (e.g., 169.254.169.254)?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Without restriction, any pod can query the EC2 metadata endpoint and potentially steal the node's IAM role credentials. Block it with NetworkPolicy: On EKS: use IMDSv2 which requires a hop limit of 1 (pods can't reach it since they're an extra hop). Configure in the launch template.

```bash
spec:
  podSelector: {}  # all pods
  policyTypes: [Egress]
  egress:
  - to:
    - ipBlock:
        cidr: 0.0.0.0/0
        except:
          - 169.254.169.254/32
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Without restriction, any pod can query the EC2 metadata endpoint and potentially steal the node's IAM role credentials. Block it w.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Without restriction, any pod can query the EC2 metadata endpoint and potentially steal the node
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-127-kubernetes-q107-what-is-a-serviceaccount-token-and-when-does-it-expire-l2"></a>
### 127. Kubernetes Q107: What is a ServiceAccount token and when does it expire [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a ServiceAccount token and when does it expire?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

In K8s 1.21+, ServiceAccount tokens are **bound tokens** — time-limited (default 1 hour), audience-specific, automatically rotated by the kubelet. Older clusters used long-lived JWTs stored as Secrets. Pods access the token at `/var/run/secrets/kubernetes.io/serviceaccount/token`. The kubelet refreshes it before expiry, so the mounted file is always valid.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: In K8s 1.21+, ServiceAccount tokens are bound tokens — time-limited (default 1 hour), audience-specific, automatically rotated by .

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: In K8s 1.21+, ServiceAccount tokens are bound tokens — time-limited (default 1 hour), audience-
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-128-kubernetes-q108-explain-kubernetes-operator-pattern-vs-helm-chart-when-would-you-build-an-operator-l3"></a>
### 128. Kubernetes Q108: Explain Kubernetes Operator pattern vs Helm chart When would you build an Operator [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Explain Kubernetes Operator pattern vs Helm chart. When would you build an Operator?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Helm chart = templated K8s YAML for stateless deployment. No runtime intelligence. Good for most stateless apps. Operator = custom controller with domain logic. It knows about the application's lifecycle and handles complex operational tasks: automated backups, failover, rolling upgrades with application-level validation, auto-scaling based on app-specific metrics. Build an operator when: your app has complex stateful operations, you need automated operational tasks, or you're building a platform component that other teams will consume (like a database operator). Don't build one for simple stateless apps — Helm is simpler.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Helm chart = templated K8s YAML for stateless deployment. No runtime intelligence. Good for most stateless apps..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Helm chart = templated K8s YAML for stateless deployment. No runtime intelligence. Good for mos
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-129-kubernetes-q109-how-do-you-do-a-canary-deployment-on-kubernetes-without-a-service-mesh-l2"></a>
### 129. Kubernetes Q109: How do you do a canary deployment on Kubernetes without a service mesh [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you do a canary deployment on Kubernetes without a service mesh?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Use two Deployments with the same Service label selector but different replica counts:

- `app-stable`: 9 replicas, version v1
- `app-canary`: 1 replica, version v2

##### 2️⃣ Remediation & Permanent Safeguards

The Service routes to all pods matching `app: myapp`. Traffic split ≈ 90%/10% based on replica ratio. Pros: simple, no extra tools. Cons: rough traffic split (not exact percentage), all users might hit canary randomly. For precise splits, use Argo Rollouts or Flagger.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: app-stable: 9 replicas, version v1.

#### ⏱️ 60-Second Elevator Pitch Summary

- app-stable: 9 replicas, version v1
- app-canary: 1 replica, version v2

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-130-kubernetes-q110-what-is-the-purpose-of-the-kube-proxy-and-what-happens-if-it-goes-down-l3"></a>
### 130. Kubernetes Q110: What is the purpose of the kube-proxy and what happens if it goes down [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the purpose of the `kube-proxy` and what happens if it goes down?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

kube-proxy runs on every node (as a DaemonSet) and maintains network rules (iptables or ipvs) that implement Services. It watches the API server for Service/Endpoint changes and updates the rules.

- Existing connections continue (iptables rules still exist).
- New Service/Endpoint changes won't be applied on that node.
- New pods that need to reach a new Service may fail.

##### 2️⃣ Remediation & Permanent Safeguards

If kube-proxy goes down on a node: Recovery: restart the kube-proxy pod. It re-syncs all rules.

- Pods on that node may route to removed pods.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Existing connections continue (iptables rules still exist)..

#### ⏱️ 60-Second Elevator Pitch Summary

- Existing connections continue (iptables rules still exist).
- New Service/Endpoint changes won't be applied on that node.
- New pods that need to reach a new Service may fail.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-131-kubernetes-q111-how-do-you-share-a-single-nginx-config-across-multiple-pods-l2"></a>
### 131. Kubernetes Q111: How do you share a single Nginx config across multiple pods [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you share a single Nginx config across multiple pods?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Store the nginx.conf in a ConfigMap. Mount it as a volume in the Deployment. All pods get the same config from the same source. When config changes, update the ConfigMap, then trigger a rolling restart (`kubectl rollout restart deployment/`).

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Store the nginx.conf in a ConfigMap. Mount it as a volume in the Deployment. All pods get the same config from the same source. Wh.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Store the nginx.conf in a ConfigMap. Mount it as a volume in the Deployment. All pods get the s
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-132-kubernetes-q112-what-is-pod-topology-spread-constraints-and-how-is-it-different-from-podantiaffinity-l3"></a>
### 132. Kubernetes Q112: What is Pod Topology Spread Constraints and how is it different from podAntiAffinity [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is Pod Topology Spread Constraints and how is it different from `podAntiAffinity`?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Both spread pods across topology domains (nodes, zones). `podAntiAffinity`: binary — either pods can or can't be on the same node. Doesn't control HOW spread out they are. Topology Spread Constraints: specifies `maxSkew` — the maximum difference in pod count between any two topology domains. `maxSkew: 1` means: never have more than 1 extra pod in one zone vs another. More granular control for even distribution. Example: 10 pods across 3 zones. With `maxSkew: 1`: could be 4/3/3. Anti-affinity would just say "no two pods on same node" which doesn't ensure zone balance.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Both spread pods across topology domains (nodes, zones)..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Both spread pods across topology domains (nodes, zones).
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-133-kubernetes-q113-how-do-you-implement-health-checks-for-a-grpc-service-in-kubernetes-l2"></a>
### 133. Kubernetes Q113: How do you implement health checks for a gRPC service in Kubernetes [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you implement health checks for a gRPC service in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use the gRPC Health Checking Protocol. Your service implements `grpc.health.v1.Health/Check`. In the probe: This is available since K8s 1.24. For older versions: use `exec` probe with `grpc_health_probe` binary copied into the container.

```bash
grpc:
  port: 50051
  service: "myapp"  # optional service name
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use the gRPC Health Checking Protocol. Your service implements grpc.health.v1.Health/Check. In the probe:.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use the gRPC Health Checking Protocol. Your service implements grpc.health.v1.Health/Check. In
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-134-kubernetes-q114-describe-how-kubernetes-implements-services-using-ipvs-mode-instead-of-iptables-l3"></a>
### 134. Kubernetes Q114: Describe how Kubernetes implements Services using IPVS mode instead of iptables [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Describe how Kubernetes implements Services using IPVS mode instead of iptables."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

In iptables mode: kube-proxy creates a chain of iptables rules for each Service. With thousands of Services, rule traversal becomes linear (O(n)). Performance degrades. In IPVS mode: kube-proxy creates an IPVS virtual server for each Service ClusterIP. IPVS uses hash tables for O(1) lookup. Scales to tens of thousands of Services. Also supports more load balancing algorithms: round-robin, least connections, IPIP, etc. Enable: `--proxy-mode=ipvs` in kube-proxy config. Requires `ipvs` kernel modules. Recommended for large clusters.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: In iptables mode: kube-proxy creates a chain of iptables rules for each Service. With thousands of Services, rule traversal become.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: In iptables mode: kube-proxy creates a chain of iptables rules for each Service. With thousands
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-135-kubernetes-q115-you-have-a-kubernetes-cluster-in-two-regions-for-disaster-recovery-how-do-you-sync-workloads-l2"></a>
### 135. Kubernetes Q115: You have a Kubernetes cluster in two regions for disaster recovery How do you sync workloads [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"You have a Kubernetes cluster in two regions for disaster recovery. How do you sync workloads?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use GitOps (ArgoCD) with a shared Git repository. Both clusters sync from the same manifests repo. Each cluster has its own ArgoCD instance. If primary cluster fails: the DR cluster already has all the workload definitions; just ensure the workloads are running (they might be scaled to 0 in DR to save cost, scale them up). For data: use database replication (Aurora Global, DynamoDB Global Tables). For traffic: Route 53 health checks with failover routing. If primary endpoint goes down, Route 53 automatically routes to DR cluster.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use GitOps (ArgoCD) with a shared Git repository. Both clusters sync from the same manifests repo. Each cluster has its own ArgoCD.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use GitOps (ArgoCD) with a shared Git repository. Both clusters sync from the same manifests re
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-136-kubernetes-q116-what-is-the-container-runtime-interface-cri-and-what-runtimes-are-commonly-used-l3"></a>
### 136. Kubernetes Q116: What is the Container Runtime Interface (CRI) and what runtimes are commonly used [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the Container Runtime Interface (CRI) and what runtimes are commonly used?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

CRI is the API between kubelet and the container runtime. kubelet doesn't care what runtime is used as long as it speaks CRI.

- **containerd** — most popular. Lightweight, CNCF project. Used in EKS, AKS, GKE.
- **CRI-O** — designed specifically for K8s. Used in OpenShift.
- **Docker** (via dockershim) — removed from K8s 1.24. Docker now uses containerd internally anyway.

##### 2️⃣ Remediation & Permanent Safeguards

Common runtimes: The runtime handles: pulling images, creating/stopping containers, managing namespaces. kubelet just calls CRI APIs.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: containerd — most popular. Lightweight, CNCF project. Used in EKS, AKS, GKE..

#### ⏱️ 60-Second Elevator Pitch Summary

- containerd — most popular. Lightweight, CNCF project. Used in EKS, AKS, GKE.
- CRI-O — designed specifically for K8s. Used in OpenShift.
- Docker (via dockershim) — removed from K8s 1.24. Docker now uses containerd internally anyway.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-137-kubernetes-q117-how-do-you-implement-autoscaling-based-on-custom-metrics-eg-queue-depth-l2"></a>
### 137. Kubernetes Q117: How do you implement autoscaling based on custom metrics (eg queue depth) [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you implement autoscaling based on custom metrics (e.g., queue depth)?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use KEDA (Kubernetes Event-Driven Autoscaling). KEDA supports 50+ built-in scalers: This scales the worker deployment based on SQS queue depth — 1 pod per 5 messages. Scales to zero when queue is empty.

```yaml
apiVersion: keda.sh/v1alpha1
kind: ScaledObject
metadata:
  name: worker-scaler
spec:
  scaleTargetRef:
    name: worker-deployment
  triggers:
  - type: aws-sqs-queue
    metadata:
      queueURL: https://sqs.us-east-1.amazonaws.com/123/my-queue
      queueLength: "5"
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use KEDA (Kubernetes Event-Driven Autoscaling). KEDA supports 50+ built-in scalers:.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use KEDA (Kubernetes Event-Driven Autoscaling). KEDA supports 50+ built-in scalers:
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-138-kubernetes-q118-a-pod-is-being-scheduled-and-then-immediately-evicted-whats-happening-l2"></a>
### 138. Kubernetes Q118: A pod is being scheduled and then immediately evicted Whats happening [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"A pod is being scheduled and then immediately evicted. What's happening?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Node is under resource pressure. kubelet evicts lower-priority pods to free resources. Check: `kubectl describe pod ` — reason will say `Evicted` with a reason (memory, disk). Check node conditions: `kubectl describe node ` — MemoryPressure, DiskPressure, PIDPressure. Fix: increase node size, add more nodes, reduce pod resource requests, clean up eviction-causing pressure (disk full, memory leak).

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Node is under resource pressure. kubelet evicts lower-priority pods to free resources. Check: kubectl describe pod  — reason will .

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Node is under resource pressure. kubelet evicts lower-priority pods to free resources. Check: k
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-139-kubernetes-q119-how-do-you-implement-multi-cluster-service-discovery-so-service-a-in-cluster-1-can-call-service-b-in-cluster-2-l3"></a>
### 139. Kubernetes Q119: How do you implement multi-cluster service discovery so Service A in cluster 1 can call Service B in cluster 2 [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you implement multi-cluster service discovery so Service A in cluster 1 can call Service B in cluster 2?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Initial Diagnostics & Root Cause Analysis

Options:

- **Submariner** — CNCF project. Creates IPsec tunnels between clusters, enables pod-to-pod communication across clusters.
- **Istio multi-cluster** — Istio service mesh spanning multiple clusters with shared control plane or separate control planes with federation.
- **AWS Cloud Map + Route 53** — register services from both clusters in Cloud Map. Use DNS for discovery.

##### 2️⃣ Remediation & Permanent Safeguards

Execute the resolution runbook and verify workload health:

- **External Ingress** — expose Service B via Ingress/NLB in cluster 2. Service A calls it via the external DNS name. Simple but requires internet or VPC peering.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Submariner — CNCF project. Creates IPsec tunnels between clusters, enables pod-to-pod communication across clusters..

#### ⏱️ 60-Second Elevator Pitch Summary

- Submariner — CNCF project. Creates IPsec tunnels between clusters, enables pod-to-pod communicati...
- Istio multi-cluster — Istio service mesh spanning multiple clusters with shared control plane or ...
- AWS Cloud Map + Route 53 — register services from both clusters in Cloud Map. Use DNS for discovery.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-140-kubernetes-q120-what-is-a-pause-container-and-why-is-it-in-every-pod-l2"></a>
### 140. Kubernetes Q120: What is a pause container and why is it in every pod [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a pause container and why is it in every pod?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

The "infra container" or "sandbox container" that holds the network namespace for the pod. All containers in the pod join its network namespace (that's how they share localhost). If the app container dies and restarts, the network namespace (and IP address) is preserved because the pause container keeps running. Image: `pause:3.x` (few hundred KB). Managed by containerd/CRI-O, not visible in `kubectl get pods`. **Q121-Q150. More Kubernetes Rapid-fire**

#### 🎯 Key Architectural Takeaway
> Pro-Tip: The "infra container" or "sandbox container" that holds the network namespace for the pod. All containers in the pod join its netw.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: The "infra container" or "sandbox container" that holds the network namespace for the pod. All
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-141-kubernetes-q121-what-is-imagepullpolicy-always-vs-ifnotpresent-l2"></a>
### 141. Kubernetes Q121: What is imagePullPolicy Always vs IfNotPresent [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is `imagePullPolicy: Always` vs `IfNotPresent`?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Always: pulls from registry every pod start (ensures latest changes). IfNotPresent: uses local cache if image tag exists. Production: use specific tags + IfNotPresent (predictable). Dev with `latest`: Always (but avoid `latest` in prod).

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Always: pulls from registry every pod start (ensures latest changes). IfNotPresent: uses local cache if image tag exists. Producti.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Always: pulls from registry every pod start (ensures latest changes). IfNotPresent: uses local
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-142-kubernetes-q122-how-do-you-configure-resource-requests-and-limits-for-init-containers-l2"></a>
### 142. Kubernetes Q122: How do you configure resource requests and limits for init containers [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you configure resource requests and limits for init containers?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Same as regular containers under `initContainers[].resources`. Init containers don't run simultaneously, so effective pod request = max(init container requests, sum of app container requests).

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Same as regular containers under initContainers[].resources. Init containers don't run simultaneously, so effective pod request = .

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Same as regular containers under initContainers[].resources. Init containers don't run simultan
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-143-kubernetes-q123-what-is-a-projected-volume-in-kubernetes-l3"></a>
### 143. Kubernetes Q123: What is a projected volume in Kubernetes [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a projected volume in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Combines multiple volume sources (secrets, configmaps, serviceAccountToken, downward API) into a single directory mount. Useful when the app expects all config in one place.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Combines multiple volume sources (secrets, configmaps, serviceAccountToken, downward API) into a single directory mount. Useful wh.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Combines multiple volume sources (secrets, configmaps, serviceAccountToken, downward API) into
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-144-kubernetes-q124-how-do-you-check-what-labels-are-on-a-node-l2"></a>
### 144. Kubernetes Q124: How do you check what labels are on a node [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you check what labels are on a node?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`kubectl get node  --show-labels` or `kubectl describe node `. Add labels: `kubectl label node  key=value`.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl get node  --show-labels or kubectl describe node . Add labels: kubectl label node  key=value..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: kubectl get node  --show-labels or kubectl describe node . Add labels: kubectl label node  key=
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-145-kubernetes-q125-what-is-the-downward-api-in-kubernetes-l2"></a>
### 145. Kubernetes Q125: What is the downward API in Kubernetes [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the downward API in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Exposes pod/node metadata (pod name, namespace, labels, annotations, resource limits) to the container as env vars or volume files. Useful for apps that need to know their own pod name or resource limits without calling the API server.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Exposes pod/node metadata (pod name, namespace, labels, annotations, resource limits) to the container as env vars or volume files.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Exposes pod/node metadata (pod name, namespace, labels, annotations, resource limits) to the co
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-146-kubernetes-q126-how-do-you-handle-pod-disruptions-during-kubernetes-version-upgrades-l3"></a>
### 146. Kubernetes Q126: How do you handle pod disruptions during Kubernetes version upgrades [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you handle pod disruptions during Kubernetes version upgrades?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Set PodDisruptionBudgets on all critical workloads. `kubectl drain --ignore-daemonsets --delete-emptydir-data`. The drain respects PDBs — won't proceed if it would violate them. Upgrade one node at a time. Monitor workloads between each node upgrade.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Set PodDisruptionBudgets on all critical workloads. kubectl drain --ignore-daemonsets --delete-emptydir-data. The drain respects P.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Set PodDisruptionBudgets on all critical workloads. kubectl drain --ignore-daemonsets --delete-
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-147-kubernetes-q127-what-is-kubectl-diff-l2"></a>
### 147. Kubernetes Q127: What is kubectl diff [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is `kubectl diff`?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Shows what would change if you applied a manifest, compared to what's currently running. Like `terraform plan` for Kubernetes.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Shows what would change if you applied a manifest, compared to what's currently running. Like terraform plan for Kubernetes..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Shows what would change if you applied a manifest, compared to what's currently running. Like t
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-148-kubernetes-q128-how-do-you-enforce-that-all-pods-in-a-namespace-must-have-resource-limits-l2"></a>
### 148. Kubernetes Q128: How do you enforce that all pods in a namespace must have resource limits [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you enforce that all pods in a namespace must have resource limits?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

LimitRange with `defaultRequest` and `default` limits OR use OPA/Gatekeeper/Kyverno policy that rejects pods without resource limits.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: LimitRange with defaultRequest and default limits OR use OPA/Gatekeeper/Kyverno policy that rejects pods without resource limits..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: LimitRange with defaultRequest and default limits OR use OPA/Gatekeeper/Kyverno policy that rej
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-149-kubernetes-q129-what-is-vertical-pod-autoscaler-vpa-and-when-should-you-use-it-vs-hpa-l3"></a>
### 149. Kubernetes Q129: What is Vertical Pod Autoscaler (VPA) and when should you use it vs HPA [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is Vertical Pod Autoscaler (VPA) and when should you use it vs HPA?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

VPA adjusts CPU/memory requests of running pods based on actual usage. Use VPA for: workloads where you know they need more resources but can't scale horizontally (stateful single replicas). Use HPA for: stateless apps where horizontal scaling makes sense. Don't use both on the same deployment (conflict on CPU metrics).

#### 🎯 Key Architectural Takeaway
> Pro-Tip: VPA adjusts CPU/memory requests of running pods based on actual usage. Use VPA for: workloads where you know they need more resour.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: VPA adjusts CPU/memory requests of running pods based on actual usage. Use VPA for: workloads w
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-150-kubernetes-q130-how-do-you-temporarily-expose-a-service-from-a-remote-cluster-to-your-local-machine-for-debugging-l2"></a>
### 150. Kubernetes Q130: How do you temporarily expose a service from a remote cluster to your local machine for debugging [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you temporarily expose a service from a remote cluster to your local machine for debugging?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`kubectl port-forward service/ 8080:80` — forwards local port 8080 to the service's port 80. Works through the API server tunnel. Kills when you close the terminal.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl port-forward service/ 8080:80 — forwards local port 8080 to the service's port 80. Works through the API server tunnel. Ki.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: kubectl port-forward service/ 8080:80 — forwards local port 8080 to the service's port 80. Work
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-151-kubernetes-q131-what-is-kubectl-top-and-what-does-it-need-to-work-l2"></a>
### 151. Kubernetes Q131: What is kubectl top and what does it need to work [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is `kubectl top` and what does it need to work?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Shows real-time CPU/memory usage of nodes and pods. Requires metrics-server to be installed. `kubectl top nodes` and `kubectl top pods`.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Shows real-time CPU/memory usage of nodes and pods. Requires metrics-server to be installed. kubectl top nodes and kubectl top pod.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Shows real-time CPU/memory usage of nodes and pods. Requires metrics-server to be installed. ku
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-152-kubernetes-q132-how-does-kubernetes-handle-pod-security-with-the-pod-security-standards-l3"></a>
### 152. Kubernetes Q132: How does Kubernetes handle pod security with the Pod Security Standards [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How does Kubernetes handle pod security with the Pod Security Standards?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Three levels: Privileged (no restrictions), Baseline (blocks most dangerous capabilities — no privileged, no hostPath), Restricted (most secure — non-root, no capabilities, seccomp required). Apply per-namespace with PodSecurityAdmission: `pod-security.kubernetes.io/enforce: restricted` label on the namespace.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Three levels: Privileged (no restrictions), Baseline (blocks most dangerous capabilities — no privileged, no hostPath), Restricted.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Three levels: Privileged (no restrictions), Baseline (blocks most dangerous capabilities — no p
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-153-kubernetes-q133-what-is-a-kubernetes-lease-l2"></a>
### 153. Kubernetes Q133: What is a Kubernetes lease [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a Kubernetes lease?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Lightweight K8s object used for leader election by control plane components (scheduler, controller-manager) and custom controllers. The holder updates the lease's `renewTime` periodically. If it misses renewal (dies), another candidate takes over by writing its identity to the lease.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Lightweight K8s object used for leader election by control plane components (scheduler, controller-manager) and custom controllers.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Lightweight K8s object used for leader election by control plane components (scheduler, control
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-154-kubernetes-q134-how-do-you-get-events-for-a-specific-namespace-sorted-by-time-l2"></a>
### 154. Kubernetes Q134: How do you get events for a specific namespace sorted by time [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you get events for a specific namespace sorted by time?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`kubectl get events -n  --sort-by='.lastTimestamp'`. Events are a great first stop when debugging — they capture all resource state changes.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl get events -n  --sort-by='.lastTimestamp'. Events are a great first stop when debugging — they capture all resource state .

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: kubectl get events -n  --sort-by='.lastTimestamp'. Events are a great first stop when debugging
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-155-kubernetes-q135-what-is-a-service-mesh-and-when-is-the-complexity-worth-it-l3"></a>
### 155. Kubernetes Q135: What is a Service Mesh and when is the complexity worth it [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a Service Mesh and when is the complexity worth it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Service mesh (Istio, Linkerd) adds a sidecar proxy to every pod, enabling: mTLS, traffic policies, retries, circuit breaking, distributed tracing, traffic splitting. Complex to operate. Worth it when: you have 10+ services and need consistent observability across all, you need mTLS for compliance (zero-trust), you want traffic management (canary deployments, circuit breaking) without code changes. Not worth it for: small number of services, team without mesh expertise.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Service mesh (Istio, Linkerd) adds a sidecar proxy to every pod, enabling: mTLS, traffic policies, retries, circuit breaking, dist.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Service mesh (Istio, Linkerd) adds a sidecar proxy to every pod, enabling: mTLS, traffic polici
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-156-kubernetes-q136-how-do-you-forward-all-logs-from-a-kubernetes-pod-to-elasticsearch-l2"></a>
### 156. Kubernetes Q136: How do you forward all logs from a Kubernetes pod to Elasticsearch [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you forward all logs from a Kubernetes pod to Elasticsearch?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use Fluentd or Filebeat as a DaemonSet. They read container logs from `/var/log/containers/` on each node and ship to Elasticsearch. Alternatively: configure your app to log in JSON format to stdout, and the DaemonSet collects and forwards.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use Fluentd or Filebeat as a DaemonSet. They read container logs from /var/log/containers/ on each node and ship to Elasticsearch..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use Fluentd or Filebeat as a DaemonSet. They read container logs from /var/log/containers/ on e
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-157-kubernetes-q137-what-is-ebpf-and-how-is-it-used-in-kubernetes-networking-l3"></a>
### 157. Kubernetes Q137: What is eBPF and how is it used in Kubernetes networking [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is eBPF and how is it used in Kubernetes networking?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Extended Berkeley Packet Filter — runs sandboxed programs in the Linux kernel. In K8s: Cilium uses eBPF instead of iptables for service routing. Benefits: much faster (kernel bypass for Service lookup), better observability (Hubble), network policy at L7. Becoming the modern replacement for iptables-based kube-proxy.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Extended Berkeley Packet Filter — runs sandboxed programs in the Linux kernel. In K8s: Cilium uses eBPF instead of iptables for se.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Extended Berkeley Packet Filter — runs sandboxed programs in the Linux kernel. In K8s: Cilium u
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-158-kubernetes-q138-what-happens-when-you-delete-a-namespace-that-has-resources-in-it-l2"></a>
### 158. Kubernetes Q138: What happens when you delete a namespace that has resources in it [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What happens when you delete a namespace that has resources in it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

K8s deletes all resources in the namespace in dependency order. The namespace stays in `Terminating` until all resources are deleted. If a resource has a finalizer that never gets removed, the namespace is stuck terminating forever. Fix: remove finalizers from stuck resources.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: K8s deletes all resources in the namespace in dependency order. The namespace stays in Terminating until all resources are deleted.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: K8s deletes all resources in the namespace in dependency order. The namespace stays in Terminat
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-159-kubernetes-q139-how-do-you-run-a-pod-on-the-control-plane-node-l2"></a>
### 159. Kubernetes Q139: How do you run a pod on the control plane node [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you run a pod on the control plane node?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Control plane nodes are tainted with `node-role.kubernetes.io/control-plane:NoSchedule`. Add a toleration to your pod: `tolerations: [{key: "node-role.kubernetes.io/control-plane", operator: "Exists"}]`. Or use `nodeSelector` with the control-plane node label.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Control plane nodes are tainted with node-role.kubernetes.io/control-plane:NoSchedule. Add a toleration to your pod: tolerations: .

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Control plane nodes are tainted with node-role.kubernetes.io/control-plane:NoSchedule. Add a to
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-160-kubernetes-q140-explain-kubernetes-network-policies-default-behavior-and-why-it-can-be-a-security-risk-l3"></a>
### 160. Kubernetes Q140: Explain Kubernetes Network Policies default behavior and why it can be a security risk [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"Explain Kubernetes Network Policies' default behavior and why it can be a security risk."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

By default, K8s has NO network isolation. All pods can talk to all other pods in the cluster, across namespaces. This is intentional (for ease of use) but dangerous in multi-tenant clusters. A pod in namespace A can directly reach a DB pod in namespace B if it knows the IP. Fix: create a "default deny all" NetworkPolicy in every namespace, then explicitly allow required traffic. This is the secure-by-default approach.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: By default, K8s has NO network isolation. All pods can talk to all other pods in the cluster, across namespaces. This is intention.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: By default, K8s has NO network isolation. All pods can talk to all other pods in the cluster, a
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-161-kubernetes-q141-what-is-a-sidecar-container-pattern-l2"></a>
### 161. Kubernetes Q141: What is a sidecar container pattern [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is a sidecar container pattern?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

A helper container that runs alongside the main app container in the same pod, sharing its network and volumes. Examples: Istio proxy (Envoy), Fluentd for log shipping, Vault agent for secrets, nginx as SSL terminator. The sidecar handles cross-cutting concerns without modifying the main app.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: A helper container that runs alongside the main app container in the same pod, sharing its network and volumes. Examples: Istio pr.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: A helper container that runs alongside the main app container in the same pod, sharing its netw
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-162-kubernetes-q142-how-do-you-pass-the-pods-own-name-to-the-app-running-inside-it-l2"></a>
### 162. Kubernetes Q142: How do you pass the pods own name to the app running inside it [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you pass the pod's own name to the app running inside it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use downward API:

```bash
env:
- name: POD_NAME
  valueFrom:
    fieldRef:
      fieldPath: metadata.name
```

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use downward API:.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use downward API:
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-163-kubernetes-q143-what-is-kubernetes-federation-and-is-it-still-recommended-l3"></a>
### 163. Kubernetes Q143: What is Kubernetes Federation and is it still recommended [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is Kubernetes Federation and is it still recommended?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Federation v1 (deprecated) tried to manage multiple clusters from a single control plane. It was complex and unreliable. Federation v2 (KubeFed) also proved difficult. Current recommendation: use GitOps (ArgoCD multi-cluster) or dedicated tools (Rancher, Anthos) for multi-cluster management instead.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Federation v1 (deprecated) tried to manage multiple clusters from a single control plane. It was complex and unreliable. Federatio.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Federation v1 (deprecated) tried to manage multiple clusters from a single control plane. It wa
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-164-kubernetes-q144-how-do-you-create-a-self-signed-tls-certificate-for-an-ingress-l2"></a>
### 164. Kubernetes Q144: How do you create a self-signed TLS certificate for an Ingress [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you create a self-signed TLS certificate for an Ingress?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Use cert-manager with `ClusterIssuer: selfsigned`. Or: `openssl req -x509 -nodes -newkey rsa:2048 -out tls.crt -keyout tls.key`, then `kubectl create secret tls my-tls --cert=tls.crt --key=tls.key`. Reference in Ingress `tls` section.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Use cert-manager with ClusterIssuer: selfsigned. Or: openssl req -x509 -nodes -newkey rsa:2048 -out tls.crt -keyout tls.key, then .

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Use cert-manager with ClusterIssuer: selfsigned. Or: openssl req -x509 -nodes -newkey rsa:2048
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-165-kubernetes-q145-what-is-an-admission-controller-and-how-does-kubernetes-use-them-l3"></a>
### 165. Kubernetes Q145: What is an Admission Controller and how does Kubernetes use them [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is an Admission Controller and how does Kubernetes use them?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Plugins that intercept API requests AFTER authentication/authorization but BEFORE persistence in etcd. Two types: Mutating (modify the resource) and Validating (accept/reject). Built-in examples: NamespaceLifecycle (rejects resources in terminating namespaces), ResourceQuota (rejects resources that exceed quota), LimitRanger (sets default limits). Custom ones use webhook admission.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Plugins that intercept API requests AFTER authentication/authorization but BEFORE persistence in etcd. Two types: Mutating (modify.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Plugins that intercept API requests AFTER authentication/authorization but BEFORE persistence i
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-166-kubernetes-q146-how-do-you-retrieve-only-the-logs-from-a-specific-container-in-a-pod-that-has-multiple-containers-l2"></a>
### 166. Kubernetes Q146: How do you retrieve only the logs from a specific container in a pod that has multiple containers [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you retrieve only the logs from a specific container in a pod that has multiple containers?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`kubectl logs  -c `. Get container names: `kubectl get pod  -o jsonpath='{.spec.containers[*].name}'`.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: kubectl logs  -c . Get container names: kubectl get pod  -o jsonpath='{.spec.containers[*].name}'..

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: kubectl logs  -c . Get container names: kubectl get pod  -o jsonpath='{.spec.containers[].name}
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-167-kubernetes-q147-what-is-kubectl-apply-prune-l2"></a>
### 167. Kubernetes Q147: What is kubectl apply --prune [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is `kubectl apply --prune`?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In one of our high-traffic production clusters, our SRE team handled this incident using a standardized runbook. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

When combined with a label selector, it deletes resources that were previously applied with `kubectl apply` but are no longer in the current manifest set. Useful for GitOps without a full GitOps controller — cleans up old resources.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: When combined with a label selector, it deletes resources that were previously applied with kubectl apply but are no longer in the.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: When combined with a label selector, it deletes resources that were previously applied with kub
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-168-kubernetes-q148-how-do-you-implement-an-egress-gateway-in-a-kubernetes-cluster-l3"></a>
### 168. Kubernetes Q148: How do you implement an egress gateway in a Kubernetes cluster [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you implement an egress gateway in a Kubernetes cluster?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"Kubernetes is a declarative desired state system; understanding the reconciliation loop is how you diagnose this quickly. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

Force all outbound traffic through a central point (useful for IP whitelisting at third-party APIs). With Istio: configure an EgressGateway service and VirtualService/DestinationRule to route external traffic through it. The gateway's pod IPs can be given static Elastic IPs on AWS. All external traffic appears from known IPs.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: Force all outbound traffic through a central point (useful for IP whitelisting at third-party APIs). With Istio: configure an Egre.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: Force all outbound traffic through a central point (useful for IP whitelisting at third-party A
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-169-kubernetes-q149-what-is-the-significance-of-the-dry-run-server-flag-vs-dry-run-client-l2"></a>
### 169. Kubernetes Q149: What is the significance of the --dry-run=server flag vs --dry-run=client [L2]

**Level:** `Senior DevOps / SRE [L2]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Production Scenario [L2]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L2` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"What is the significance of the `--dry-run=server` flag vs `--dry-run=client`?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"In our production Kubernetes clusters running microservices on EKS/AKS, this was a classic operational challenge. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

`client`: validates locally using the cached schema. `server`: sends to the API server which validates (including webhook admission controllers) without persisting. Server-side dry-run is more accurate — catches webhook validation issues that client-side misses.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: client: validates locally using the cached schema. server: sends to the API server which validates (including webhook admission co.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: client: validates locally using the cached schema. server: sends to the API server which valida
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-170-kubernetes-q150-how-do-you-implement-a-global-rate-limiter-for-all-requests-to-your-services-in-kubernetes-l3"></a>
### 170. Kubernetes Q150: How do you implement a global rate limiter for all requests to your services in Kubernetes [L3]

**Level:** `Staff SRE / Principal Architect [L3]` | **Category:** `Kubernetes` • `Additional Kubernetes Scenarios (Q101-Q200)` | **Type:** `Staff SRE Scenario [L3]`

**Tags:** `Kubernetes` `Additional Kubernetes Scenarios (Q101-Q200)` `L3` `Container Orchestration` `K8s`

> **Interview Question:**  
> *"How do you implement a global rate limiter for all requests to your services in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
"When troubleshooting Kubernetes, I always follow a structured layered model: Pod status -> Events -> Logs -> Network. When addressing this question, I walk the interviewer through our production incident runbook: isolating the blast radius, checking diagnostic logs and metrics, and applying a safe fix."

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Production Solution & Architecture

With Istio: EnvoyFilter or RateLimitPolicy using a Redis-backed rate limit service. With nginx-ingress: `nginx.ingress.kubernetes.io/limit-rps` annotation. With Envoy-based Ingress: global rate limiting service (Envoy Rate Limit) shared across all ingress instances for true global limits.

#### 🎯 Key Architectural Takeaway
> Pro-Tip: With Istio: EnvoyFilter or RateLimitPolicy using a Redis-backed rate limit service. With nginx-ingress: nginx.ingress.kubernetes.i.

#### ⏱️ 60-Second Elevator Pitch Summary

- Immediate Triage: With Istio: EnvoyFilter or RateLimitPolicy using a Redis-backed rate limit service. With nginx-
- Run targeted verification commands before modifying configuration.
- Automate permanent guardrails (CI check, alerts, IaC policy) to prevent recurrence.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-171-fine-grained-service-discovery-across-1-000-microservices-using-envoy-istio"></a>
### 171. Fine-Grained Service Discovery Across 1,000+ Microservices Using Envoy & Istio

**Level:** `Staff / Principal SRE` | **Category:** `Kubernetes` • `Service Mesh & Networking` | **Type:** `Netflix-Scale Systems`

**Tags:** `Envoy` `Istio` `Service Discovery` `Kubernetes` `Systems at Scale`

> **Interview Question:**  
> *"How would you implement fine-grained service discovery across 1000+ microservices using Envoy or Istio?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
At a scale of 1,000+ microservices and tens of thousands of pods, default 'flat mesh' service discovery causes catastrophic control plane saturation. By default, Istiod broadcasts every endpoint in the entire cluster to every Envoy sidecar via EDS (Endpoint Discovery Service). A cluster of 1,000 services with 10 replicas each forces every Envoy proxy to maintain 10,000 TCP connection pools and route tables, driving sidecar memory to 1GB+ per pod and triggering xDS CPU storms during routine pod churn. We solved this by decomposing the mesh using scoped discovery boundaries.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Scope Egress Discovery Boundaries with Istio Sidecar Resources

Never allow sidecars to watch the root namespace. Enforce strict egress host visibility per namespace:

- **Memory Drop:** Drops sidecar footprint from ~950MB to <35MB per pod by discarding 98% of unneeded route tables and listener configs.
- **Control Plane Headroom:** Istiod now only pushes updates to proxies that actually depend on the changing workload.

```yaml
apiVersion: networking.istio.io/v1beta1
kind: Sidecar
metadata:
  name: default
  namespace: payments
spec:
  egress:
  - hosts:
    - "./*"                  # Only discover services within the same namespace
    - "istio-system/*"       # Required telemetry and control plane
    - "auth/auth-service.auth.svc.cluster.local"  # Explicit cross-namespace dependency
```

##### 2️⃣ Migrate from State-of-the-World to Delta xDS

Configure Istiod and Envoy sidecars to use incremental (Delta) xDS protocol over gRPC instead of ADS (Aggregated Discovery Service) full snapshots:

- **Incremental Updates:** When a pod restarts in service B, Envoy only receives the specific IP diff rather than the serialized 1,000-service cluster configuration.
- **Network Egress:** Reduces mesh internal control plane traffic by over 85% during rolling deployment bursts.

```bash
# In IstioOperator or Helm values:
meshConfig:
  discoverySelectors:
    - matchLabels:
        istio-discovery: enabled
  defaultConfig:
    proxyMetadata:
      ISTIO_DELTA_XDS: "true"
```

##### 3️⃣ Partition Workloads with Discovery Selectors

Use Istio Discovery Selectors to completely exclude high-churn ephemeral jobs, database replicas, and batch workers from the service mesh control plane:

- Prevents batch jobs that cycle hundreds of pods per minute from triggering invalidation events across customer-facing API proxies.

```bash
kubectl label namespace batch-jobs spark-analytics istio-discovery=disabled
kubectl label namespace core-api checkout payments istio-discovery=enabled
```

##### 4️⃣ Diagnostic Verification Commands

Verify endpoint synchronization and proxy memory consumption on the live cluster:

```bash
# 1. Inspect total clusters known to a specific Envoy sidecar (target: < 25, not 1000+)
istioctl proxy-config clusters <pod-name>.<namespace> | wc -l

# 2. Check sync latency between Istiod control plane and proxies
istioctl proxy-status

# 3. Check memory consumption of the Envoy sidecar container
kubectl top pod <pod-name> -n <namespace> --containers | grep istio-proxy
```

> 💡 **Pro-Tip / Highlight:** In our benchmarks, scoping reduced P99 discovery synchronization latency from 4.8 seconds down to 110ms across 1,200 microservices.

#### 🎯 Key Architectural Takeaway
> At 1,000+ services, service discovery is an architectural partitioning problem, not a compute problem. You must treat the mesh as a federated set of localized dependency graphs using Sidecar egress hosts, Delta xDS, and Discovery Selectors.

#### ⏱️ 60-Second Elevator Pitch Summary

- By default, Istio pushes every cluster endpoint to every Envoy proxy, causing memory bloat (1GB+/pod) and xDS CPU storms at 1,000+ service scale.
- We enforce strict 'Sidecar' CRDs in every namespace, restricting proxy egress discovery to intra-namespace peers plus explicit external dependencies.
- We enable Delta xDS (incremental gRPC streaming) to transmit only endpoint diffs rather than full multi-megabyte cluster snapshots during pod churn.
- We apply Discovery Selectors at the mesh level to isolate high-churn batch/analytics workloads from customer-facing API sidecars.
- Result: Envoy sidecar memory dropped from 950MB to ~35MB, and control plane sync latency fell from 4.8s to 110ms.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-172-runtime-network-security-enforcement-with-ebpf-cilium-vs-traditional-iptables-cnis"></a>
### 172. Runtime Network Security Enforcement with eBPF & Cilium vs. Traditional iptables CNIs

**Level:** `Staff / Principal SRE` | **Category:** `Security` • `Cloud Native Security & eBPF` | **Type:** `Netflix-Scale Systems`

**Tags:** `eBPF` `Cilium` `Kubernetes` `DevSecOps` `Networking`

> **Interview Question:**  
> *"Explain how you’d leverage eBPF + Cilium to enforce network security policies at runtime, and what the advantages are over traditional CNIs?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
In hyper-scale Kubernetes environments with 50,000+ pods, traditional CNIs like Calico (iptables mode) or AWS VPC CNI with kube-proxy hit fundamental Linux kernel limits. iptables evaluates packet filtering rules sequentially O(N). At 20,000 rules, adding or deleting a rule locks the kernel packet filter table (`xtables_lock`), causing latency spikes of 500ms+ and packet drops. Cilium replaces iptables completely by compiling and injecting sandboxed eBPF bytecode directly into Linux socket and TC (traffic control) hooks.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Kernel Hook Insertion Points: How Cilium Operates

Cilium attaches eBPF programs at three strategic layers of the Linux networking stack:

- **XDP (eXpress Data Path):** Executes at the network driver level before SKB (socket buffer) allocation. Can drop DDoS syn-floods at line rate (10M+ pps) without kernel overhead.
- **TC (Traffic Control):** Attaches to `tc ingress/egress` to enforce security policies and rewrite L3/L4 headers without traversing netfilter.
- **Socket Layer (cgroup/sock_ops):** Short-circuits pod-to-pod communication on the same node directly via kernel memory (`sockmap`), bypassing the entire TCP/IP stack.

##### 2️⃣ Cryptographic Identity vs Ephemeral IP Filtering

Traditional CNIs bind policies to pod IPs. In dynamic Kubernetes clusters with pod churn, IP re-use causes security race conditions. Cilium assigns a unified Security Identity:

- **O(1) BPF Map Lookups:** Identity lookups execute in O(1) hash maps in memory rather than iterating through 20,000 sequential iptables rules.
- **L7 Protocol Filtering:** Enforces HTTP method/path and DNS-aware egress (`toFQDNs`) inside the kernel without injecting a heavy user-space sidecar.

```yaml
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
  name: secure-checkout-egress
  namespace: production
spec:
  endpointSelector:
    matchLabels:
      app: checkout
  egress:
  - toEndpoints:
    - matchLabels:
        app: payment-gateway
    toPorts:
    - ports:
      - port: "8443"
        protocol: TCP
      rules:
        http:
        - method: "POST"
          path: "/v1/charge"
```

##### 3️⃣ Runtime Diagnostic & Verification Runbook

Inspect active eBPF maps, drops, and flow logs via the Cilium CLI and Hubble:

```bash
# 1. Inspect live security identities and endpoints on the node
cilium endpoint list

# 2. Inspect active BPF maps loaded in the kernel
bpftool map show | grep cilium

# 3. Stream real-time dropped packets and policy denials via Hubble
hubble observe --verdict DROPPED --follow

# 4. Profile kernel latency of eBPF socket enforcement
cilium-dbg bpf metrics list
```

> 💡 **Pro-Tip / Highlight:** By leveraging eBPF socket-layer shortcuts (`sockmap`), pod-to-pod latency on the same host dropped from 1.2ms to 0.4ms while enforcing zero-trust L7 policies.

#### 🎯 Key Architectural Takeaway
> Cilium + eBPF moves network security from reactive, linear O(N) packet inspection to deterministic O(1) kernel-native identity enforcement, eliminating iptables lock contention and delivering zero-sidecar L7 visibility.

#### ⏱️ 60-Second Elevator Pitch Summary

- Traditional iptables CNIs suffer from O(N) sequential rule evaluation, where 10,000+ rules cause xtables_lock contention, latency spikes, and conntrack table exhaustion.
- Cilium attaches sandboxed eBPF programs directly to Linux kernel hooks (XDP, TC, and socket layers), evaluating policies via O(1) hash maps in nanoseconds.
- It decouples security from ephemeral pod IPs by assigning cryptographic Security Identities based on metadata labels.
- It enables transparent L7 policy enforcement (e.g. allowing only POST /v1/charge) and DNS-aware filtering without requiring sidecar proxies.
- Using Hubble, we get kernel-level observability on every packet drop without adding user-space telemetry overhead.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-173-advanced-kubernetes-health-probe-engineering-detecting-deep-business-logic-deadlocks-beyond-http-200"></a>
### 173. Advanced Kubernetes Health Probe Engineering: Detecting Deep Business Logic Deadlocks Beyond HTTP 200

**Level:** `Senior DevOps / Staff SRE` | **Category:** `Kubernetes` • `Pod Lifecycle & SRE` | **Type:** `Incident Runbook`

**Tags:** `Kubernetes` `Health Probes` `Liveness` `Readiness` `StartupProbe`

> **Interview Question:**  
> *"Walk through advanced kube-probe configurations to detect business logic failures, not just HTTP 200."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
The most common anti-pattern in Kubernetes is pointing both liveness and readiness probes to a shallow endpoint like `/health` that simply returns `200 OK` from the web framework. If the app's database connection pool deadlocks, or Kafka message consumers stall, the pod continues returning 200 OK, silently dropping user transactions. Conversely, if the liveness probe queries an external database and that database slows down, kubelet restarts all pods simultaneously, turning a localized DB latency hiccup into a catastrophic cluster-wide cascading outage.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Differentiate Probe Responsibilities (Startup vs Liveness vs Readiness)

Never conflate failure recovery with traffic routing. Each probe has a distinct purpose:

- **startupProbe:** Protects slow-starting applications (JVM, machine learning warmups). Disables liveness and readiness checks until the app is initialized, preventing premature crash loops.
- **livenessProbe:** ONLY checks internal, unrecoverable deadlocks (e.g. fatal JVM thread deadlock). If it fails, kubelet KILLS the pod.
- **readinessProbe:** Checks temporary capacity to serve traffic (e.g. connection pool saturation, cache warming). If it fails, pod is removed from Service Endpoints WITHOUT restarting.

##### 2️⃣ Deep Business Logic Readiness Handler

Implement a specialized `/healthz/ready` endpoint that verifies internal worker state with strict local timeouts:

- **Connection Pool Headroom:** Verifies at least 5% of DB pool connections are free.
- **Event Loop Latency:** In Node.js or Go, checks that event loop lag is below 200ms.
- **Consumer Heartbeat:** Verifies Kafka/RabbitMQ consumer consumer groups have committed offsets within the last 30 seconds.
- **Circuit Breaker State:** If external downstream dependencies are open, readiness returns HTTP 503, shedding traffic without pod restart.

```bash
readinessProbe:
  httpGet:
    path: /healthz/ready
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5
  timeoutSeconds: 2
  failureThreshold: 2
  successThreshold: 1
```

##### 3️⃣ Isolate Liveness from External Dependencies

Never let your liveness probe query external resources. It must evaluate strictly local process health:

- Returns HTTP 500 ONLY if internal process state is corrupt (e.g. out-of-memory worker threads, unhandled background exception in main thread).
- If downstream Redis or PostgreSQL fails, the liveness probe MUST still return 200 OK so kubelet does not restart the container.

```bash
livenessProbe:
  httpGet:
    path: /healthz/live
    port: 8080
  initialDelaySeconds: 15
  periodSeconds: 10
  timeoutSeconds: 2
  failureThreshold: 3
```

#### 🎯 Key Architectural Takeaway
> Liveness probes should only kill processes that cannot self-heal. Readiness probes should dynamically regulate traffic based on downstream backpressure and internal thread state.

#### ⏱️ 60-Second Elevator Pitch Summary

- Shallow probes that return 200 OK mask critical failures like database pool starvation and Kafka consumer stalls.
- We implement a strict 3-probe architecture: startupProbe covers initial cache warming, livenessProbe detects unrecoverable process deadlocks, and readinessProbe governs traffic ingress.
- Crucially, our liveness probe never queries external dependencies; if a database is down, killing the container only worsens the outage.
- Our readiness probe inspects deep application state: DB pool saturation, Kafka consumer heartbeats, and circuit breaker status. If overloaded, the pod sheds traffic gracefully without terminating.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-174-kubernetes-hpa-refuses-to-scale-despite-prometheus-cpu-80-cloud-metrics-server-triage"></a>
### 174. Kubernetes HPA Refuses to Scale Despite Prometheus CPU > 80%: Cloud & Metrics Server Triage

**Level:** `Senior SRE / Cloud Engineer` | **Category:** `Kubernetes` • `Autoscaling & Resource Management` | **Type:** `Production Fire Drill`

**Tags:** `Kubernetes` `HPA` `Prometheus` `Metrics Server` `Autoscaling`

> **Interview Question:**  
> *"HPA refuses to scale even though Prometheus shows CPU > 80%. Diagnose with cloud + K8s metrics."*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
During a flash sale, monitoring alerts page the on-call engineer: application CPU usage is sustained at 85% across all pods, customer latency is degrading, but the Deployment remains pinned at its minimum replica count of 3. The engineer reports that Prometheus shows the cluster on fire, but HPA refuses to scale out.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Understanding the Fundamental Decoupling: Prometheus vs Metrics Server

Kubernetes HPA does NOT read Prometheus by default. It queries the Kubernetes Metrics API (`metrics.k8s.io`):

- Prometheus collects metrics asynchronously via scraping agents (Node Exporter, cAdvisor).
- HPA relies on `metrics-server` scraping kubelet summary APIs every 15–60 seconds.
- If `metrics-server` is degraded, failing TLS verification, or hitting API limits, HPA is blinded.

##### 2️⃣ Execute Diagnostic CLI Triage

Inspect HPA conditions, resource definitions, and metrics API health:

- **Missing CPU Requests:** If `resources.requests.cpu` is omitted, HPA calculation is mathematically impossible. HPA computes target percentage as: `(actual usage / requested CPU) * 100`. Without requests, HPA shows `&lt;unknown&gt;`.
- **Max Replicas Reached:** Check if current replicas == `spec.maxReplicas`.
- **Stabilization Window:** Check if downscale/upscale stabilization windows are throttling scaling actions.

```bash
# 1. Check HPA status and conditions
kubectl describe hpa <hpa-name>

# Look for:
# Conditions:
#   AbleToScale: True
#   ScalingActive: False (FailedGetResourceMetric)
# Current: <unknown> / 80%

# 2. Check if metrics-server is serving metrics
kubectl top pods -l app=<app-name>
kubectl get apiservice v1beta1.metrics.k8s.io

# 3. Check container resources specification
kubectl get deployment <app-name> -o yaml | grep -A 8 resources
```

##### 3️⃣ Check Node Capacity & Cluster Autoscaler Blockades

If HPA updated `desiredReplicas` but pods cannot be scheduled:

- If nodes are fully packed and the Cloud Cluster Autoscaler / Karpenter is blocked by AWS EC2 quota limits or subnet IP exhaustion, pods remain stuck in `Pending`.

```bash
kubectl get pods -l app=<app-name> | grep Pending
kubectl describe pod <pending-pod> | grep -A 5 Events
# Look for: "0/12 nodes are available: 12 Insufficient cpu."
```

#### 🎯 Key Architectural Takeaway
> HPA scaling failures almost always boil down to three root causes: missing container CPU requests, metrics-server failure, or cluster capacity constraints blocking Pending pods.

#### ⏱️ 60-Second Elevator Pitch Summary

- HPA does not read Prometheus by default; it reads the Kubernetes Metrics API (metrics-server). First, I run 'kubectl describe hpa' to check the ScalingActive condition.
- If HPA shows ' / 80%', the most common cause is that the container specification lacks 'resources.requests.cpu', making percentage calculation mathematically undefined.
- Second, I check if metrics-server is healthy using 'kubectl get apiservice v1beta1.metrics.k8s.io' and 'kubectl top pods'.
- Third, I verify whether HPA has already hit 'maxReplicas', or if upscale stabilization windows are suppressing new events.
- Finally, if desired replicas increased but actual pods are stuck in Pending, I inspect Cluster Autoscaler / Karpenter logs for EC2 quota or subnet IP exhaustion.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-175-production-kubernetes-version-lifecycle-deprecation-audit-strategy"></a>
### 175. Production Kubernetes Version Lifecycle & Deprecation Audit Strategy

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Amazon EKS & Upgrades` | **Type:** `Production Scenario`

**Tags:** `Kubernetes` `Amazon EKS` `Version Management` `Cluster Upgrade` `API Deprecations`

> **Interview Question:**  
> *"What is the current version of Kubernetes you are using in your project, and how do you manage version lifecycle and deprecations?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
In my current project, we run Kubernetes v1.29.x in production on Amazon EKS and validate upgrades on v1.30.x in staging before rollout. We maintain strict control plane and node group version skew, track deprecations release-by-release, and run upgrade rehearsals with Helm chart compatibility checks.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Live Version Auditing & Worker Node Skew Policy

Demonstrate hands-on familiarity with live cluster versions and worker node alignment:

- **Cluster & Node Version Inspection:** Query both client and server versions to ensure API compatibility.
- **Version Skew Discipline:** Kubernetes supports up to 3 minor versions skew between kube-apiserver and kubelet, but in production we keep worker nodes within 1 minor version of the control plane.
- **Cloud Provider Specifics:** Query EKS/AKS managed control plane metadata directly via cloud CLI.

```bash
# Check cluster client and server versions
kubectl version --short

# Inspect node versions across the cluster
kubectl get nodes -o wide
kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.nodeInfo.kubeletVersion}{"\n"}{end}'

# Query Amazon EKS control plane version
aws eks describe-cluster --name prod-cluster --region ap-south-1 --query 'cluster.version' --output text
```

##### 2️⃣ Auditing Manifests & Helm Charts for Deprecated APIs

Proactively identify deprecated API versions (e.g. ingress, pdb, autoscaling) before cluster upgrades:

- **Inspect live resources:** Query active resource API groups and check chart template versions.
- **Pre-upgrade scanning:** Integrate tools like Pluto or Kube-no-trouble (kubent) into CI/CD pipelines to catch deprecated API calls before merge.
- **Canary Node Group Testing:** Spin up a canary node pool running the target version to test DaemonSets and CNI compatibility before wide rollout.

```yaml
# Check for deprecated API usage in live manifests
kubectl api-resources | grep -i ingress
helm list -A
kubectl get ingress -A -o yaml | grep 'apiVersion:' -n
```

#### 🎯 Key Architectural Takeaway
> Always state the exact minor version (e.g., v1.29.x moving to v1.30.x) and explain the upgrade validation workflow: API deprecation scans, staging rehearsals, and canary node groups.

#### ⏱️ 60-Second Elevator Pitch Summary

- State live production version (e.g., v1.29.x) and target staging version (v1.30.x) with strict 1-minor-version node group skew.
- Audit API deprecations with kubectl api-resources, Helm chart inspections, and automated Pluto/kubent scans.
- Rehearse upgrades in lower environments with canary node pools before upgrading production control plane and worker nodes.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-176-production-incident-walkthrough-bad-configmap-feature-flag-rapid-rollback"></a>
### 176. Production Incident Walkthrough: Bad ConfigMap Feature Flag & Rapid Rollback

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Troubleshooting & Debugging` | **Type:** `Production Incident`

**Tags:** `Kubernetes` `Production Incident` `Troubleshooting` `Rollback` `Helm`

> **Interview Question:**  
> *"What was the last production issue you faced and how did you resolve it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
One recent production issue was a sudden spike in 5xx errors from 0.2% to 8% immediately following an application release. While pods remained in Ready state, application logs revealed an invalid downstream service endpoint injected via a newly updated ConfigMap. I confirmed the blast radius, rolled back the Helm release in under 5 minutes, and then added automated config schema validation to prevent recurrence.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Immediate Blast Radius Assessment & Log Correlation

Triage latency and error rate spikes by inspecting edge ingress and container runtime logs:

- **Telemetry Verification:** Ingress metrics showed HTTP 500/502 errors spiking right after the last deployment.
- **Pod Health Paradox:** Pods passed liveness/readiness probes, but application logs threw unhandled downstream connection timeouts.
- **Diff Inspection:** Correlated the incident onset with Helm rollout history and ConfigMap revisions.

```bash
# Confirm pod status and fetch recent error logs
kubectl get pods -n payments
kubectl logs -n payments deploy/api --since=10m | tail -100
kubectl describe ingress -n payments public-ing

# Inspect recent release and rollout history
kubectl rollout history deploy/api -n payments
helm history api -n payments
```

##### 2️⃣ Executing Rollback & Restoring Traffic in Under 5 Minutes

Prioritize restoring the service SLO over debugging live production pods:

- **Atomic Rollback:** Execute an immediate Helm rollback or kubectl rollout undo to restore the last known stable replica set.
- **Rollout Verification:** Monitor deployment status and event streams until healthy pods are serving 100% of traffic.
- **Error Rate Stabilization:** Verify that error rates in Datadog/Prometheus return to the baseline < 0.2%.
- **Post-Mortem & Safeguards:** Added JSON schema validation for Helm values and mandatory pre-merge preview tests.

```bash
# Roll back immediately via kubectl or Helm
kubectl rollout undo deploy/api -n payments
# Or if deployed via Helm:
helm rollback api 12 -n payments

# Verify recovery and monitor cluster events
kubectl rollout status deploy/api -n payments --timeout=120s
kubectl get events -n payments --sort-by=.lastTimestamp | tail -20
```

#### 🎯 Key Architectural Takeaway
> Prioritize immediate rollback over deep live debugging to protect SLAs. Once restored, conduct a blameless post-mortem and enforce automated configuration validation in CI.

#### ⏱️ 60-Second Elevator Pitch Summary

- Identify blast radius immediately using Ingress telemetry and application container logs.
- Execute fast atomic rollback via Helm rollback / kubectl rollout undo in under 5 minutes to restore customer traffic.
- Implement permanent preventative controls: JSON schema linting for configs and canary deployment gates.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-177-intermittent-502-bad-gateway-via-ingress-under-high-traffic-systematic-triage"></a>
### 177. Intermittent 502 Bad Gateway via Ingress Under High Traffic — Systematic Triage

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Networking & Ingress` | **Type:** `Production Incident`

**Tags:** `Kubernetes` `Ingress` `NGINX Ingress` `HTTP 502` `HPA`

> **Interview Question:**  
> *"During high traffic, your app shows intermittent 502 errors through Ingress — how do you debug and fix it?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
I debug 502s from the edge inward: Ingress controller logs and metrics, upstream service endpoints, pod readiness, connection saturation, timeouts, and application logs. Under high traffic, common causes are insufficient replicas, slow upstreams, readiness flapping, keepalive/timeout mismatches, or node CPU throttling. I correlate timestamps across Ingress, service, and application telemetry before tuning.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Ingress Controller Logs & Service Endpoints Validation

Differentiate whether the 502 is generated by the Ingress controller or returned by the backend application:

- **Ingress Controller Error Logs:** Search NGINX Ingress controller logs for `upstream timed out (110: Connection timed out)` or `connect() failed (111: Connection refused)`.
- **Service Endpoints Check:** Verify whether active endpoints are dropping or flapping under load.
- **Pod Readiness Flapping:** Check if high CPU causes readiness probes to time out, removing pods from endpoints dynamically.

```bash
# Filter Ingress controller logs for 502 responses
kubectl logs -n ingress-nginx deploy/ingress-nginx-controller --since=15m | grep ' 502 '
kubectl describe ingress public-api -n app

# Check service endpoints and watch pod restarts
kubectl get svc,endpoints -n app api -o wide
kubectl get pods -n app -l app=api -w
kubectl describe pod -n app <pod-name> | egrep 'Readiness|Liveness|Restart'
```

##### 2️⃣ Tuning Resource Pressure, HPA, and Upstream Proxy Timeouts

Remediate upstream latency bottlenecks and adjust Ingress controller keepalive and timeout limits:

- **CPU Throttling & HPA:** Inspect `kubectl top pods` and HPA metrics; increase HPA minReplicas so capacity is pre-warmed for peaks.
- **Tune Proxy Timeouts:** If backend queries take longer during traffic spikes, annotate the Ingress to extend proxy read and send timeouts from default 60s to 120s.
- **Database & Query Optimization:** Resolve backend bottleneck (e.g. unindexed query or connection pool starvation) that triggered slow upstream processing.

```bash
# Inspect resource consumption and autoscaling
kubectl top pods -n app
kubectl top nodes
kubectl get hpa -n app
kubectl describe hpa api -n app

# Extend NGINX Ingress timeout annotations
kubectl annotate ingress public-api -n app nginx.ingress.kubernetes.io/proxy-read-timeout='120' --overwrite
kubectl annotate ingress public-api -n app nginx.ingress.kubernetes.io/proxy-send-timeout='120' --overwrite
```

#### 🎯 Key Architectural Takeaway
> 502 Bad Gateway means the Ingress controller failed to get a timely HTTP response from upstream pods. Trace from edge logs to service endpoints, verify readiness probe stability, and tune timeouts alongside HPA scaling.

#### ⏱️ 60-Second Elevator Pitch Summary

- Inspect NGINX Ingress controller logs to verify whether errors are upstream connection timeouts or dropped endpoints.
- Check pod CPU throttling and readiness probe failures that temporarily remove pods from Service endpoints during traffic spikes.
- Apply permanent fixes: increase HPA minReplicas, optimize upstream connection pools, and tune Ingress proxy-read-timeout annotations.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-178-preventing-bad-configurations-from-reaching-production-in-ci-cd-pipelines"></a>
### 178. Preventing Bad Configurations from Reaching Production in CI/CD Pipelines

**Level:** `Senior DevOps / SRE` | **Category:** `CI/CD` • `🔐 Supply Chain Security & Advanced CI/CD` | **Type:** `CI/CD Architecture`

**Tags:** `CI/CD` `Kubernetes` `Policy as Code` `Helm` `Kubeconform`

> **Interview Question:**  
> *"How do you prevent bad configs from reaching production in a CI/CD pipeline?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
I use layered controls across every stage of the pipeline: schema validation, linting, render checks, policy-as-code, environment-specific tests, and progressive delivery. For Kubernetes and Helm configs, I run helm lint, helm template, kubeconform with strict schemas, Conftest or Kyverno policy checks, secret scanning, and dry-run apply against a test API server before deployment.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Static Linting, Template Rendering & Schema Validation

Catch syntax, type mismatches, and deprecated Kubernetes schema errors early in pull requests:

- **Helm Lint & Template:** Run `helm lint` to detect chart errors and `helm template` against environment values to produce concrete manifests.
- **Kubeconform Strict Schema Checking:** Validate rendered YAML against official Kubernetes OpenAPI schemas with `-strict` to reject undocumented fields.
- **Server-Side Dry Run:** Execute `kubectl apply --dry-run=server` against an ephemeral or staging cluster to validate mutating webhooks and CRDs.

```bash
# Helm validation and rendering
helm lint charts/api
helm template api charts/api -f values-prod.yaml > rendered.yaml

# Kubernetes schema validation
kubeconform -strict -summary rendered.yaml
kubectl apply --dry-run=server -f rendered.yaml
```

##### 2️⃣ Policy-as-Code (OPA/Conftest) & Secret Scanning

Enforce organization security standards and prevent misconfigurations automatically:

- **OPA / Conftest Guardrails:** Block configs that violate security baselines (e.g., privileged containers, missing resource limits, insecure Ingress TLS, root user).
- **Secret Leak Prevention:** Run Gitleaks or Trufflehog in pre-commit and CI to ensure API keys and passwords never enter git.
- **Environment Promotion Gates:** Mandate PR reviews, protected branches, and successful deployment to staging before promoting to production.

```bash
# Policy checks with OPA Conftest
conftest test rendered.yaml --policy policy/

# Secret scanning and YAML linting
yamllint .
gitleaks detect --source .
```

#### 🎯 Key Architectural Takeaway
> Layer static linting (helm lint, kubeconform), policy-as-code (Conftest/OPA), secret scanning (Gitleaks), and server-side dry runs in CI so invalid configurations fail before touching production clusters.

#### ⏱️ 60-Second Elevator Pitch Summary

- Implement static verification in CI: helm lint, helm template, and kubeconform -strict against Kubernetes schemas.
- Enforce organizational security policies using OPA Conftest and scan for accidental secrets with Gitleaks.
- Validate against real Kubernetes admission webhooks with kubectl apply --dry-run=server in preview environments.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-179-helm-deployment-fails-due-to-insufficient-cluster-resources-sre-triage"></a>
### 179. Helm Deployment Fails Due to Insufficient Cluster Resources — SRE Triage

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Platform Engineering & Delivery` | **Type:** `Production Incident`

**Tags:** `Kubernetes` `Helm` `Resource Management` `Capacity Planning` `Quotas`

> **Interview Question:**  
> *"Helm deployment fails due to insufficient cluster resources — what is your approach?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
First I confirm whether the failure is scheduling-related (CPU/memory requests, PVCs, node selectors, taints) or quota-related (namespace ResourceQuota and LimitRange). I inspect events and pending pods, compare requests/limits against actual cluster allocatable capacity, then either right-size resources, scale node groups, or split the rollout. I avoid blindly lowering requests if it compromises application SLOs.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Differentiating Scheduling Starvation vs Namespace ResourceQuota

Inspect Helm release details and Kubernetes event streams to pinpoint the exact failure mechanism:

- **Dry-Run & Helm Debug:** Run `helm upgrade --dry-run --debug` to inspect the exact manifest and resource requests submitted.
- **Pending Pod Inspection:** Check `kubectl describe pod` to find scheduler messages: `0/12 nodes are available: 12 Insufficient memory` vs `exceeded quota: compute-resources`.
- **Quota & Allocatable Capacity:** Inspect `kubectl describe quota` and `kubectl describe nodes` to evaluate unreserved node capacity.

```bash
# Inspect Helm release status and run debug dry-run
helm upgrade --install api charts/api -n app -f values-prod.yaml --debug --dry-run
helm status api -n app

# Inspect scheduling and quota failures
kubectl get pods -n app
kubectl describe pod -n app <pending-pod>
kubectl get events -n app --sort-by=.lastTimestamp | tail -30
kubectl describe quota -n app

# Check node resource allocation
kubectl top nodes
kubectl describe nodes | egrep 'Allocated resources|cpu|memory' -A8
```

##### 2️⃣ Capacity Remediation, Node Scaling & Safe Atomic Release

Resolve the resource constraint and safely re-run the deployment:

- **Cluster Autoscaler / Karpenter:** If nodes are saturated, trigger node pool expansion or adjust Karpenter provisioner limits.
- **Namespace Quota Adjustment:** If namespace quota is capped, submit a quota adjustment PR after verifying overall cluster headroom.
- **Temporary Workload Right-Sizing:** Scale replica count temporarily if urgent, or tune oversized sidecar requests.
- **Atomic Rollout Retry:** Re-run `helm upgrade --atomic --timeout 10m` so that if resources stall, Helm cleanly rolls back without leaving dangling pods.

```bash
# Temporary right-size replicas if needed
kubectl scale deploy api -n app --replicas=3

# Re-run release with atomic rollback flag
helm upgrade api charts/api -n app -f values-prod.yaml --atomic --timeout=10m
```

#### 🎯 Key Architectural Takeaway
> Distinguish between node-level resource exhaustion (requires Cluster Autoscaler/Karpenter scaling or right-sizing) and namespace ResourceQuota exhaustion (requires quota tuning). Always use helm --atomic to avoid leaving deployments in failed states.

#### ⏱️ 60-Second Elevator Pitch Summary

- Examine pending pod events to distinguish node-level capacity starvation from namespace ResourceQuota breaches.
- Scale worker node groups via Cluster Autoscaler/Karpenter or adjust namespace ResourceQuota allocations based on actual telemetry.
- Execute Helm releases with --atomic and --timeout to ensure automatic rollback if resource provisioning stalls.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-180-enterprise-internal-helm-chart-distribution-using-oci-registries-ecr-harbor"></a>
### 180. Enterprise Internal Helm Chart Distribution Using OCI Registries (ECR/Harbor)

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Platform Engineering & Delivery` | **Type:** `CI/CD Architecture`

**Tags:** `Kubernetes` `Helm` `OCI Registry` `Harbor` `AWS ECR`

> **Interview Question:**  
> *"How do you share Helm charts internally across multiple engineering teams?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
I package charts and publish them to an internal OCI registry (such as AWS ECR, Harbor, GHCR, or Artifactory) using semantic versioning. Teams consume the charts in their CI/CD pipelines with pinned versions, and we maintain a central changelog and JSON values schema. OCI-based sharing eliminates legacy chart repository servers and leverages our existing container registry authentication and RBAC.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Packaging & Publishing Charts to Internal OCI Registries

Modern Helm 3 treats charts as standard OCI artifacts stored alongside container images:

- **Dependency & Lint Checks:** Run `helm dependency update` and `helm lint` to ensure dependencies and templates are validated.
- **Packaging:** Package chart into a versioned tarball (e.g. `base-app-1.4.2.tgz`).
- **OCI Push:** Log in to the internal registry and push directly using the `oci://` protocol.

```bash
# Package and push chart to OCI registry
helm dependency update charts/base-app
helm lint charts/base-app
helm package charts/base-app

# Authenticate and push
helm registry login harbor.internal.example.com
helm push base-app-1.4.2.tgz oci://harbor.internal.example.com/helm
```

##### 2️⃣ Team Consumption, Version Pinning & Governance

How consumer teams integrate shared base charts into their deployment pipelines:

- **Version Pinning:** Application pipelines consume charts by specifying explicit semantic versions (e.g., `--version 1.4.2`) to prevent unexpected breaking changes.
- **Values Schema Enforcement:** Include a `values.schema.json` file in the chart to validate team-provided values during client-side rendering.
- **Automated Release Pipelines:** Use GitHub Actions / GitLab CI with semantic-release to automatically build, test, and publish chart artifacts when PRs merge to main.

```bash
# Pull and inspect remote OCI chart
helm pull oci://harbor.internal.example.com/helm/base-app --version 1.4.2

# Deploy directly from OCI registry in CI/CD
helm upgrade --install myapp oci://harbor.internal.example.com/helm/base-app \
  --version 1.4.2 -n myns -f values.yaml --create-namespace
```

#### 🎯 Key Architectural Takeaway
> Adopt Helm OCI registries (ECR, Harbor, GHCR) over legacy ChartMuseum/HTTP servers. It unifies container and chart security, simplifies access control, and enables strict semantic versioning.

#### ⏱️ 60-Second Elevator Pitch Summary

- Publish versioned Helm charts as OCI artifacts directly to internal registries like Harbor or AWS ECR.
- Enforce schema validation with values.schema.json and semantic versioning to protect downstream teams from breaking changes.
- Integrate chart consumption directly into application CI/CD pipelines using pinned oci:// registry URIs.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-181-automated-helm-chart-testing-linting-unit-testing-ephemeral-kind-verification"></a>
### 181. Automated Helm Chart Testing: Linting, Unit Testing & Ephemeral Kind Verification

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Platform Engineering & Delivery` | **Type:** `Technical Deep-Dive`

**Tags:** `Kubernetes` `Helm` `Testing in CI` `Chart Testing` `Kind`

> **Interview Question:**  
> *"What is Helm chart testing and how is it done in a production CI/CD pipeline?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
Helm chart testing validates chart quality, syntax, and operational behavior before release. It consists of multiple tiers: static linting and template rendering, JSON schema validation for inputs, template unit tests for conditional logic, and integration tests by installing the chart into an ephemeral disposable cluster (kind/k3d). In CI, I use helm lint, chart-testing (ct), and the helm-unittest plugin to catch misconfigurations before merge.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Static Linting, Template Rendering & Unit Testing

Fast feedback stage running in CI runners without needing a live Kubernetes cluster:

- **Helm Lint & Template:** Verifies syntax, required fields, and renders YAML against different values fixtures.
- **Template Unit Testing:** Use the `helm-unittest` plugin to test complex Go template logic, if/else branches, and label injection in isolation.
- **Schema Validation:** Ensures team values conform strictly to `values.schema.json`.

```bash
# Static linting and dry-run rendering
helm lint charts/api
helm template api charts/api -f charts/api/ci-values.yaml > rendered.yaml

# Template unit testing with helm-unittest
helm plugin install https://github.com/helm-unittest/helm-unittest || true
helm unittest charts/api
```

##### 2️⃣ Integration Testing with chart-testing (ct) and Ephemeral Kind Clusters

Spin up a real disposable Kubernetes cluster in GitHub Actions to test actual installation and pod readiness:

- **Chart Testing Tool (ct):** The official CNCF `ct` tool detects changed charts, validates version bumps, and executes test suites.
- **Kind Cluster Integration:** Automatically bootstrap a lightweight Kubernetes-in-Docker (kind) cluster in CI.
- **Installation & Smoke Test:** Install the chart, wait for pods to reach `Ready` state, and run Helm test pods (e.g. `helm test api`) before tearing down the cluster.

```bash
# Chart testing static checks and installation test
ct lint --charts charts/api

# Spin up ephemeral kind cluster and test release
kind create cluster --name helm-ci
helm upgrade --install api charts/api -n test --create-namespace
kubectl rollout status deploy/api -n test --timeout=180s
kubectl get all -n test
kind delete cluster --name helm-ci
```

#### 🎯 Key Architectural Takeaway
> A complete Helm chart test strategy combines fast static checks (helm lint, helm-unittest) with realistic ephemeral cluster testing (chart-testing on Kind) to catch breaking template and API issues before release.

#### ⏱️ 60-Second Elevator Pitch Summary

- Implement multi-tiered testing: helm lint, template rendering, and schema validation on every pull request.
- Test Go template conditional logic and edge cases using the helm-unittest plugin.
- Run automated end-to-end install and readiness tests inside disposable Kind clusters using CNCF chart-testing (ct).

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-182-multi-cloud-docker-workload-architecture-build-once-deploy-portably"></a>
### 182. Multi-Cloud Docker Workload Architecture: Build Once, Deploy Portably

**Level:** `Senior DevOps / SRE` | **Category:** `Docker` • `Docker in CI/CD` | **Type:** `CI/CD Architecture`

**Tags:** `Docker` `Multi-Cloud` `Buildx` `EKS` `AKS`

> **Interview Question:**  
> *"How would you manage Docker workloads across multiple clouds (e.g., AWS and Azure)?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
I avoid managing raw Docker hosts manually across clouds. Instead, I standardize on immutable, multi-architecture images built once via Buildx, push them to a central registry strategy (such as GHCR or replicated ECR/ACR), and run workloads on managed Kubernetes orchestrators (EKS, AKS, GKE). Deployment is driven by Terraform and GitHub Actions with environment parity, shared Helm charts, and cloud-specific values overlays.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Immutable Multi-Architecture Builds & Registry Distribution

Ensure container images execute seamlessly across cloud providers and CPU architectures (AMD64/ARM64):

- **Docker Buildx:** Build multi-platform images (`linux/amd64`, `linux/arm64`) using Docker BuildKit to support diverse cloud VM instances.
- **Centralized vs Replicated Registry:** Store images in a global registry (GHCR/JFrog) or replicate automatically to regional cloud registries (AWS ECR / Azure ACR) to avoid cross-cloud egress costs and rate limits.
- **Strict Semantic Digest Tagging:** Deploy using immutable tags or SHA256 digests to guarantee binary parity across cloud environments.

```bash
# Create and use multi-architecture buildx builder
docker buildx create --use --name multi || true

# Build and push multi-arch image
docker buildx build --platform linux/amd64,linux/arm64 \
  -t ghcr.io/org/api:1.8.0 -t ghcr.io/org/api:latest --push .

# Replicate to cloud-specific registry if required
docker pull ghcr.io/org/api:1.8.0
docker tag ghcr.io/org/api:1.8.0 <aws_account>.dkr.ecr.ap-south-1.amazonaws.com/api:1.8.0
docker push <aws_account>.dkr.ecr.ap-south-1.amazonaws.com/api:1.8.0
```

##### 2️⃣ Unified Orchestration & Cloud Abstraction Layer

Decouple application code and container configuration from cloud-specific infrastructure services:

- **Standardized Kubernetes Orchestration:** Run workloads on EKS and AKS using identical core manifest definitions rather than raw VM Docker daemons.
- **Base Chart with Cloud Overlays:** Use a shared Helm chart for the microservice with cloud-specific `values-aws.yaml` and `values-azure.yaml` (e.g., storage classes, ingress annotations).
- **Terraform Infrastructure Modules:** Abstract cloud primitives (VPC, IAM, Managed DB) behind modular Terraform modules while keeping application deployment pipelines identical.

```bash
# Deploy identical chart with cloud-specific values overlay
# AWS deployment:
helm upgrade --install api charts/api -f values.yaml -f values-aws.yaml

# Azure deployment:
helm upgrade --install api charts/api -f values.yaml -f values-azure.yaml
```

#### 🎯 Key Architectural Takeaway
> Achieve multi-cloud container portability by building multi-arch images once in CI, using a unified orchestrator (Kubernetes on EKS/AKS), and isolating cloud differences into Terraform and Helm values overlays.

#### ⏱️ 60-Second Elevator Pitch Summary

- Build immutable multi-architecture container images once using Docker Buildx and distribute via central or replicated registries.
- Deploy across clouds using managed Kubernetes (EKS/AKS) to maintain API and runtime parity.
- Use shared Helm charts with cloud-specific values overlays and modular Terraform to abstract cloud infrastructure differences.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-183-integrating-jenkins-with-docker-kubernetes-and-aws-ecr-eks-for-cloud-native-ci-cd"></a>
### 183. Integrating Jenkins with Docker, Kubernetes, and AWS (ECR/EKS) for Cloud-Native CI/CD

**Level:** `Senior DevOps / SRE` | **Category:** `CI/CD` • `Jenkins & Pipeline Configuration` | **Type:** `CI/CD Architecture`

**Tags:** `CI/CD` `Jenkins` `Docker` `Kubernetes` `Amazon EKS`

> **Interview Question:**  
> *"How did you integrate Jenkins with Docker, Kubernetes, and AWS?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
I integrate Jenkins into the cloud-native ecosystem using three pillars: (1) Docker BuildKit/buildx for multi-architecture image compilation, (2) the Jenkins Kubernetes plugin to provision ephemeral container agents dynamically on EKS, and (3) AWS IAM role assumption via IRSA/OIDC for passwordless authentication to ECR and EKS. Artifacts are versioned by git commit SHA and promoted through environments using Helm.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Dynamic Kubernetes Agent Provisioning & Docker BuildKit

Configure Jenkins to scale build worker pods automatically in response to job queues:

- **Kubernetes Cloud Plugin:** Jenkins Master communicates with the internal K8s API server, spinning up multi-container agent pods with Kaniko or Docker-in-Docker sidecars on demand.
- **BuildKit Layer Caching:** Use Docker Buildx with remote inline cache or AWS ECR cache backends to avoid rebuilding unchanged dependencies.
- **Commit SHA Tagging:** Images are tagged with the immutable short git commit SHA (e.g., `app:abc1234`) rather than mutable tags like `latest`.

```yaml
// Declarative Jenkinsfile pipeline snippet
pipeline {
  agent {
    kubernetes {
      yaml '''
apiVersion: v1
kind: Pod
spec:
  serviceAccountName: jenkins-ecr-deployer
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug
    command: ['sleep', '9999999']
'''
    }
  }
  stages {
    stage('Build & Push') {
      steps {
        sh '/kaniko/executor --context=dir://. --destination=123456789012.dkr.ecr.ap-south-1.amazonaws.com/api:${GIT_COMMIT:0:7}'
      }
    }
  }
}
```

##### 2️⃣ Passwordless ECR/EKS Authentication (IRSA) & Helm Release

Eliminate static AWS keys and deploy declarative workloads to EKS:

- **AWS IRSA (IAM Roles for Service Accounts):** Bind the Jenkins agent ServiceAccount to an AWS IAM Role with strictly scoped permissions for `ecr:PutImage` and EKS access.
- **Staging Automated Deployment:** Automatically trigger `helm upgrade --install` against staging EKS using values overlays.
- **Production Promotion Gate:** Gated with a manual approval stage, canary traffic routing, and automated rollback if HTTP 5xx errors spike.

```bash
# Jenkins deploying to EKS via Helm
aws eks update-kubeconfig --name prod-cluster --region ap-south-1
helm upgrade --install payment-api charts/payment-api \
  -n payments \
  --set image.tag=${GIT_COMMIT:0:7} \
  -f values-prod.yaml \
  --atomic --timeout 5m
```

#### 🎯 Key Architectural Takeaway
> Integrate Jenkins with Kubernetes using dynamic agent pod scaling, build immutable images tagged by git SHA, authenticate to AWS without static keys using IRSA, and release via Helm with --atomic flags.

#### ⏱️ 60-Second Elevator Pitch Summary

- Use the Kubernetes plugin to dynamically schedule single-use ephemeral agent pods on EKS.
- Build immutable container images tagged with git commit SHAs using BuildKit/Kaniko for speed and security.
- Authenticate seamlessly to AWS ECR and EKS using IRSA and deploy versioned Helm charts with automated rollback gates.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-184-designing-high-availability-ha-resilient-autoscaling-in-production-kubernetes"></a>
### 184. Designing High Availability (HA) & Resilient Autoscaling in Production Kubernetes

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Autoscaling & Reliability` | **Type:** `Technical Deep-Dive`

**Tags:** `Kubernetes` `High Availability` `HPA` `Karpenter` `TopologySpreadConstraints`

> **Interview Question:**  
> *"How do you design High Availability and Autoscaling in Kubernetes?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
I design Kubernetes HA by systematically removing single points of failure across both the control plane and data plane: Multi-AZ node groups, multiple workload replicas, PodDisruptionBudgets (PDBs), TopologySpreadConstraints across availability zones, and pod anti-affinity. Autoscaling is designed in two complementary tiers: horizontal pod scaling via HPA based on CPU/memory and custom metrics, paired with node autoscaling via Karpenter or Cluster Autoscaler to provision compute capacity dynamically.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Multi-AZ Workload Distribution & Disruption Budgets

Ensure zero downtime during node failures, AZ outages, and cluster maintenance:

- **TopologySpreadConstraints:** Enforce even pod distribution across availability zones using `topologyKey: topology.kubernetes.io/zone` with `maxSkew: 1`.
- **Pod Anti-Affinity:** Ensure pods of the same deployment do not land on the same physical worker node to prevent a single node crash from killing multiple replicas.
- **PodDisruptionBudgets (PDB):** Define `minAvailable: 60%` or `maxUnavailable: 1` so node draining and upgrades never violate minimum application capacity.

```bash
# High-availability Deployment topology constraints
spec:
  replicas: 6
  template:
    spec:
      topologySpreadConstraints:
        - maxSkew: 1
          topologyKey: topology.kubernetes.io/zone
          whenUnsatisfiable: DoNotSchedule
          labelSelector:
            matchLabels:
              app: payment-service
      affinity:
        podAntiAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
            - weight: 100
              podAffinityTerm:
                labelSelector:
                  matchLabels:
                    app: payment-service
                topologyKey: kubernetes.io/hostname
```

##### 2️⃣ Two-Tier Autoscaling: HPA & Node Provisioning (Karpenter)

Coordinate application pod demand with physical cluster compute provisioning:

- **HorizontalPodAutoscaler (HPA):** Configure target CPU utilization (typically 70%) and custom business metrics (e.g. SQS queue depth or HTTP requests/sec via Prometheus Adapter).
- **Stabilization Windows:** Set scale-down stabilization windows (e.g., 300s) to prevent pod flapping/thrashing during erratic traffic bursts.
- **Karpenter / Cluster Autoscaler:** When HPA scales up pods and nodes run out of allocatable CPU/RAM, Karpenter detects the pending pods and launches right-sized EC2 nodes in under 45 seconds.

```yaml
# HPA with scale-down stabilization
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: payment-hpa
  namespace: prod
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: payment-service
  minReplicas: 3
  maxReplicas: 20
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
  behavior:
    scaleDown:
      stabilizationWindowSeconds: 300
```

#### 🎯 Key Architectural Takeaway
> Achieve true Kubernetes HA by combining TopologySpreadConstraints across zones, podAntiAffinity across nodes, PDBs to protect during maintenance, and dual-tier autoscaling (HPA for pods, Karpenter for worker nodes).

#### ⏱️ 60-Second Elevator Pitch Summary

- Distribute pod replicas across availability zones using TopologySpreadConstraints and prevent co-location with podAntiAffinity.
- Protect production capacity during node upgrades and drain events with PodDisruptionBudgets (PDB).
- Couple HPA for workload scaling with Karpenter for sub-minute node provisioning and cost-efficient bin-packing.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-185-kubernetes-pod-restart-mechanics-container-restarts-vs-pod-evictions-lifecycle-hooks"></a>
### 185. Kubernetes Pod Restart Mechanics: Container Restarts vs Pod Evictions & Lifecycle Hooks

**Level:** `Senior DevOps / SRE` | **Category:** `Kubernetes` • `Troubleshooting & Pod Lifecycle` | **Type:** `Technical Deep-Dive`

**Tags:** `Kubernetes` `Pod Lifecycle` `Kubelet` `CrashLoopBackOff` `SIGTERM`

> **Interview Question:**  
> *"What actually happens under the hood when a Kubernetes Pod restarts?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
In Kubernetes, people often say 'the pod restarted', but technically pods don't restart — containers inside the pod restart. When a container process exits or fails a liveness probe, the local Kubelet on that node detects the exit code and applies the pod's restartPolicy. If restartPolicy is Always or OnFailure, Kubelet restarts the container in-place using exponential backoff (CrashLoopBackOff), incrementing the container's restartCount while preserving the Pod's IP, UID, and ephemeral volume data. If the Pod is deleted, evicted, or rescheduled, the entire Pod is destroyed and a brand new Pod with a new UID and IP is created by the controller.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ In-Place Container Restarts & Exponential Backoff

How Kubelet handles container crashes without destroying the parent Pod sandbox:

- **Kubelet Reconciliation:** The Kubelet monitors container runtime cgroups. When PID 1 inside the container exits, Kubelet cleans up the container cgroup.
- **Preserved Pod Sandbox:** The network namespace (Pause container), Pod IP address, and mounted volumes (emptyDir, PVCs) remain intact across container restarts.
- **CrashLoopBackOff Delay:** Kubelet delays restarts with an exponential backoff (10s, 20s, 40s, 80s, 160s, capping at 300s / 5 minutes) to prevent thrashing node resources.

```bash
# Inspect container restart count and termination reason
kubectl get pod api-7b8f9c-xyz -n prod -o jsonpath='{range .status.containerStatuses[*]}{.name}{" | Restarts: "}{.restartCount}{" | ExitCode: "}{.lastState.terminated.exitCode}{" | Reason: "}{.lastState.terminated.reason}{"\n"}{end}'

# Check previous container logs before the restart
kubectl logs api-7b8f9c-xyz -n prod --previous --tail=50
```

##### 2️⃣ Pod Replacement, OOMKills & Graceful Termination

What happens when Kubernetes terminates or replaces a Pod entirely:

- **OOMKill (Exit Code 137):** When a container exceeds its memory limit, the Linux kernel OOM Killer immediately sends SIGKILL (9 + 128 = 137). Kubelet records `Reason: OOMKilled` and restarts the container.
- **Graceful Termination Sequence:** Kubelet removes pod from endpoints -> executes `preStop` hook -> sends `SIGTERM` -> waits `terminationGracePeriodSeconds` (default 30s) -> sends `SIGKILL`.
- **Controller Replacement:** If a Deployment rolling update occurs or a node fails, the ReplicaSet creates a new Pod object with a fresh UID, new IP address, and newly allocated emptyDirs.

```bash
# Stream recent Kubelet events for pod lifecycle and eviction signals
kubectl get events -n prod --field-selector involvedObject.name=api-7b8f9c-xyz --sort-by=.metadata.creationTimestamp

# Describe pod to review exit status and termination history
kubectl describe pod api-7b8f9c-xyz -n prod | grep -A 10 'Last State:'
```

#### 🎯 Key Architectural Takeaway
> Containers restart in-place inside the existing pod sandbox (preserving Pod IP and volumes) with Kubelet exponential backoff up to 300s. A Pod itself is only replaced when a controller (ReplicaSet/Karpenter) destroys the old Pod object and schedules a new one.

#### ⏱️ 60-Second Elevator Pitch Summary

- Distinguish container restarts (Kubelet restarts process in-place, keeping Pod IP and storage) from Pod replacement (controller creates new UID and IP).
- Understand CrashLoopBackOff as Kubelet exponential backoff (10s to 300s) protecting the host from thrashing loops.
- Diagnose container exit codes immediately: Exit 137 indicates kernel OOMKill, while Exit 1 or 143 reflects application errors and SIGTERM.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

<a id="scenario-186-why-deployments-succeed-at-the-orchestrator-level-yet-users-still-see-5xx-errors"></a>
### 186. Why Deployments Succeed at the Orchestrator Level Yet Users Still See 5xx Errors

**Level:** `Senior DevOps / SRE` | **Category:** `CI/CD` • `Deployment Strategies & Rollbacks` | **Type:** `Production Incident`

**Tags:** `CI/CD` `Release Engineering` `Kubernetes` `Readiness Probes` `CDN`

> **Interview Question:**  
> *"Why do Kubernetes deployments succeed with green rollouts while end-users still experience errors?"*

<details>
<summary><b>🔍 Click to expand Production Runbook & Senior Engineer Answer</b></summary>

#### 🎙️ Senior Engineer First-Person Context
A deployment can succeed 100% at the orchestrator layer while the user journey fails completely. Kubernetes reports rollout success simply when new pods pass their readiness checks and old pods terminate cleanly. However, users can still experience errors due to non-backward-compatible database migrations, stale CDN/browser caches, missing ConfigMap keys, shallow readiness probes that don't check downstream dependencies, or Ingress/Service endpoint synchronization latency. Rollout status measures container lifecycle, not business success.

#### 📋 Step-by-Step Diagnostic & Resolution Runbook

##### 1️⃣ Why Orchestrator Health Does Not Equal User Success

Common architectural disconnects between container readiness and real traffic:

- **Shallow Readiness Probes:** If `/healthz` merely checks that the HTTP server is listening rather than testing critical DB connections, pods report `Ready` and receive traffic before they can actually process requests.
- **Database Schema Incompatibilities:** The new application code expects a new column or table that was not migrated yet in that region, causing 500 errors despite healthy pods.
- **EndpointSlice Sync Delays:** When old pods terminate, there is a race condition where the Ingress controller sends traffic to terminating pods before iptables/IPVS rules update.

```bash
# Verify rollout status vs real endpoint availability
kubectl rollout status deploy/checkout -n prod
kubectl get endpointslice -l kubernetes.io/service-name=checkout -n prod

# Test critical user journey endpoint directly against ingress IP
curl -I -H 'Host: checkout.example.com' http://<ingress-controller-ip>/api/v1/health

# Check container environment variables for missing configs
kubectl exec -it deploy/checkout -n prod -- printenv | grep -E 'DB_|REDIS_|FEATURE_'
```

##### 2️⃣ Post-Release Verification & Progressive Delivery Guardrails

Establish real user-centric verification beyond green deployment statuses:

- **Monitor Golden Signals Immediately:** Track HTTP 5xx error rates, p95 latency, and conversion rates in Prometheus/Datadog for 15 minutes post-release.
- **Expand-Contract Database Migrations:** Ensure schema changes are strictly backward compatible so old and new application versions can run simultaneously.
- **Canary Analysis & Automated Rollback:** Use Argo Rollouts or Flagger with automated Prometheus metric analysis (e.g., error rate < 0.5%) to automatically abort releases before they affect all users.

```bash
# Prometheus query for post-deployment error rate verification
sum(rate(http_requests_total{job="checkout", status=~"5.."}[5m]))
  /
sum(rate(http_requests_total{job="checkout"}[5m])) * 100 > 0.5
```

#### 🎯 Key Architectural Takeaway
> Container readiness is not business readiness. Measure post-release user-facing Golden Signals (errors, latency), use expand-contract database migrations, and deploy via canary gates with automated rollbacks.

#### ⏱️ 60-Second Elevator Pitch Summary

- Differentiate orchestrator status from user experience: green pods can still fail due to schema mismatches or missing secrets.
- Harden readiness probes to validate critical downstream dependencies without creating cascading failure loops.
- Verify releases using user Golden Signals (error rate, p95 latency) and automate canaries via progressive delivery.

[⚡ Practice this question interactively on interview.naveedkumbhar.com](https://interview.naveedkumbhar.com/?cat=kubernetes)

</details>

---

## 🤝 Contributing & Community

Have an alternative battle-tested runbook or an edge-case to add? PRs and scenario submissions are warmly welcomed!

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/new-runbook`)
3. Commit your changes (`git commit -m 'Add production triage runbook'`)
4. Push to branch (`git push origin feature/new-runbook`)
5. Open a Pull Request

---

### 🔗 Connect with Naveed Ahmed
- 🌐 **Portfolio & Systems:** [naveedkumbhar.com](https://naveedkumbhar.com)
- ✍️ **Tech Blog:** [blog.naveedkumbhar.com](https://blog.naveedkumbhar.com)
- 💼 **LinkedIn:** [linkedin.com/in/naveedkumbhar](https://pk.linkedin.com/in/naveedkumbhar)
- 🐦 **X (Twitter):** [@naveedkumbhar](https://x.com/naveedkumbhar)
- 🧵 **Threads:** [@naveedkumbhar](https://threads.net/@naveedkumbhar)
- 📸 **Instagram:** [@naveedkumbhar](https://instagram.com/naveedkumbhar)
- 📘 **Facebook:** [KiLL3rMiNd](https://www.facebook.com/KiLL3rMiNd)
- 💬 **WhatsApp Direct:** [@naveedkumbhar](https://wa.me/naveedkumbhar)
- 🐙 **GitHub:** [github.com/naveedkumbhar](https://github.com/naveedkumbhar)


---

## 📜 License

This repository is open-source and released under the [MIT License](LICENSE).  

Copyright © 2026 [Naveed Ahmed](https://naveedkumbhar.com). All rights reserved.
