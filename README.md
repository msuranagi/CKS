# CKS Exam Preparation Notes

Notes compiled to prepare for the Certified Kubernetes Security Specialist (CKS) exam. This repository keeps each topic in its own note; use this page as the index.

The links below are grouped by the topics already covered in the repository. They are not a complete exam syllabus or a prescribed study order.

## Exam approach and general references

- [Strategies for navigating documentation during the exam](CKS-Exam-Strategies.md)
- [Kubernetes admin commands and security scanning](Kubernetes-Admin-Commands-and-Scanning.md)
- [Quick references, admission control, SBOMs, and eBPF](CKS-Quick-References.md)
- [CKS exam requirements and testing resources](CKS-Exam-Requirements-and-Testing.md)

## Identity and access control

- [Service accounts](ServiceAccounts.md)
- [Create a test pod with a service account](TestPod-with-SA.md)
- [Create a ClusterRole for node access](newuser-clusterrole.md)
- [Create a ClusterRole for storage access](newuser-clusterrole-extended-permissions.md)

## Network traffic and ingress

- [NetworkPolicy egress rules](networkpolicy.md)
- [Cilium network encryption](Cilium.md)
- [NGINX Ingress rewrite target](Ingress-Annotation-and-rewrite-target.md)

## Runtime isolation and cluster checks

- [RuntimeClass examples for gVisor and Kata](Sandboxing.md)
- [Kube-bench usage and a sample finding](Kubebench.md)

## Cluster maintenance

- [Control plane Kubernetes version upgrade](ControlPlane-Upgrade.md)
- [Worker node Kubernetes version upgrade](Node-Upgrade.md)

## Using these notes

Examples and version numbers are preserved from the individual notes. Check the relevant Kubernetes or tool documentation and confirm the target cluster's versions and configuration before using commands or manifests.

The general notes and the dedicated Kube-bench note contain overlapping material; both files are kept separate.
