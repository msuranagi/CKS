# Test Pod with a Service Account

Deploy a test pod and assign it the `node-viewer-service` service account:

```bash
kubectl apply -f - <<'EOF'
apiVersion: v1
kind: Pod
metadata:
  name: api-test-pod
  namespace: default
spec:
  containers:
    - name: api-test
      image: nginx
      command: ["sleep"]
      args: ["infinity"]
  serviceAccountName: node-viewer-service
  restartPolicy: Never
EOF
```
