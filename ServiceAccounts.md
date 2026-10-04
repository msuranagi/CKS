# Service Accounts

---

## Get the service account used by a pod

```bash
kubectl get pod <pod-name> -o jsonpath='{.spec.serviceAccountName}'
```

## Create a token for a service account

```bash
kubectl create token <sa-name> -n <namespace>
```

## Check permissions as a service account

```bash
kubectl auth can-i <verb> <resource> --as=system:serviceaccount:<namespace>:<sa-name>
```

---

## Allow a pod using custom-sa to read pods

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: pod-reader-binding
  namespace: default
subjects:
- kind: ServiceAccount
  name: custom-sa
  namespace: default
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## Restrict pod egress to the API server only

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all-except-api
  namespace: default
spec:
  podSelector:
    matchLabels:
      run: restricted-pod
  policyTypes:
  - Egress
  egress:
  - to:
    - ipBlock:
        cidr: 10.0.0.1/32  # API Server IP
    ports:
    - protocol: TCP
      port: 443
```

This policy restricts pod egress traffic and only allows access to the API server.

---

## Disable auto-mounting of service account tokens

### At the ServiceAccount level

```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: no-token-sa
  namespace: default
automountServiceAccountToken: false
```

### At the Pod level

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secure-pod
  namespace: default
spec:
  serviceAccountName: default
  automountServiceAccountToken: false
  containers:
  - name: nginx
    image: nginx
```
