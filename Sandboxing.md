# RuntimeClass Sandboxing

gVisor and Kata Containers are two container runtimes that provide additional isolation features compared with traditional runtimes such as Docker or containerd.

## RuntimeClass examples

### gVisor

```yaml
apiVersion: node.k8s.io/v1
handler: runsc
kind: RuntimeClass
metadata:
  name: gvisor
```

### Kata Containers

```yaml
apiVersion: node.k8s.io/v1
handler: kata-runtime
kind: RuntimeClass
metadata:
  name: kata-containers
```

## Assign a RuntimeClass to a pod

Set `runtimeClassName` in the pod spec to select a RuntimeClass:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-1
  labels:
    name: simple-webapp
spec:
  runtimeClassName: secure-runtime
  containers:
    - name: simple-webapp
      image: kodekloud/webapp-delayed-start
      ports:
        - containerPort: 8080
```
