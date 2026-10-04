# CNCF CKS Notes

---

## Create a Role

```bash
kubectl create role developer --namespace=default --verb=list,create,delete --resource=pods
```

## Create a RoleBinding

```bash
kubectl create rolebinding dev-user-binding --namespace=default --role=developer --user=dev-user
```

## Namespace vs Cluster Scoped Resources

```bash
kubectl api-resources --namespaced=true   # resources scoped at namespace level
kubectl api-resources --namespaced=false  # resources scoped at cluster level
```

## kubectl Proxy and Port Forwarding

```bash
kubectl proxy   # opens proxy port to the API server
kubectl proxy & # by default enables kubectl proxy on port 8001
kubectl proxy --port 8002 &
```

### Port Forward Examples

```bash
kubectl port-forward pods/{POD_NAME} 8005:80 &
kubectl port-forward deployment/{DEPLOYMENT_NAME} 8005:80 &
kubectl port-forward service/{SERVICE_NAME} 8005:80 &
kubectl port-forward replicaset/{REPLICASET_NAME} 8005:80 &
```

> 8005 is the localhost port and 80 is the internal port of the pod/service.

### Exec into a Pod

```bash
kubectl exec app -- curl -s http://<IP>:9999
```

## ClusterRole and ClusterRoleBinding

```bash
kubectl create clusterrole node-viewer --verb=get --verb=list --verb=watch --resource=nodes
kubectl create clusterrolebinding node-viewer-binding --clusterrole=node-viewer --serviceaccount=default:node-viewer-service
```

---

## Kube Bench

```bash
curl -L https://github.com/aquasecurity/kube-bench/releases/download/v0.4.0/kube-bench_0.4.0_linux_amd64.tar.gz -o kube-bench_0.4.0_linux_amd64.tar.gz
tar -xvf kube-bench_0.4.0_linux_amd64.tar.gz
```

Run kube-bench in the control plane:

```bash
./kube-bench --config-dir pwd/cfg --config pwd/cfg/config.yaml
```

### Example Output

```text
[PASS] 1.2.17 Ensure that the admission control plugin NodeRestriction is set (Automated)
[PASS] 1.2.18 Ensure that the --insecure-bind-address argument is not set (Automated)
[FAIL] 1.2.19 Ensure that the --insecure-port argument is set to 0 (Automated)
```

### Fix

Issue: insecure port enabled

Add the following to `/etc/kubernetes/manifests/kube-apiserver.yaml`:

```yaml
--insecure-port=0
```
