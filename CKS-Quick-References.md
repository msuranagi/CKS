# CKS Quick References

This note collects additional commands and concepts.

## Kubernetes commands

### Create a TLS secret from a certificate and key

```bash
kubectl -n webhook-demo create secret tls webhook-server-tls \
  --cert="/root/keys/webhook-server-tls.crt" \
  --key="/root/keys/webhook-server-tls.key"
```

### Test whether a pod can reach an external website

```bash
kubectl exec -it busybox-pod -n namespace-worker -- wget -qO- http://google.com
```

This runs `wget` from inside the pod and prints the response body if the request succeeds.

## Admission control

Pod Security Admission is an admission controller. Authentication identifies the requester, and authorization determines whether the requester may perform an operation. Admission controllers can apply additional policies to API requests, such as pod security restrictions and image-related policy.

The source note uses this command to inspect the API server's admission-plugin flag help:

```bash
kubectl exec -n kube-system kube-apiserver-controlplane -it -- \
  kube-apiserver -h | grep enable-admission-plugins
```

This displays help for the `--enable-admission-plugins` option; it does not necessarily show which admission plugins are enabled in the running cluster.

## SBOM formats

- **SPDX** is commonly used for software component and license information, including legal-compliance use cases.
- **CycloneDX** is commonly used for security-focused software bills of materials, including vulnerability and supply-chain risk management.

These are general areas of emphasis, not exclusive format capabilities.

## Cilium and eBPF

Cilium uses eBPF to implement networking and other datapath features, with the goal of high performance and low overhead.
