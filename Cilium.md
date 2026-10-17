# Cilium Network Encryption

## Reference

[Cilium network encryption documentation](https://docs.cilium.io/en/stable/security/network/encryption/)

## Install Cilium with encryption enabled

```bash
# Add the Cilium Helm repository
helm repo add cilium https://helm.cilium.io/

# Install Cilium with encryption enabled
helm install cilium cilium/cilium \
  --version 1.19.4 \
  --namespace kube-system \
  --set encryption.enabled=true \
  --set encryption.type=wireguard \
  --set operator.tolerations[0].operator=Exists
```

Verify that Cilium is running and encryption is enabled:

```bash
# Wait for the status of Cilium to be OK
cilium status

# Check the encryption status of the Cilium installation
cilium encryption status
```

## Deploy a client pod

Deploy a pod named `curlpod`, label it, then open a shell in it:

```bash
kubectl run curlpod --image=rapidfort/curl --command -- sleep 3600
kubectl label pod curlpod app=curlpod
sleep 5
kubectl exec -it curlpod -- sh
```
