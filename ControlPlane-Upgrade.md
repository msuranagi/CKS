# Control Plane Kubernetes Version Upgrade

The commands in this note describe changing the Kubernetes package repository and upgrading the control-plane node to v1.35.0.

## Update the package repository

On the control-plane node, edit the Kubernetes apt repository file:

```bash
vim /etc/apt/sources.list.d/kubernetes.list
```

Update the version in the repository URL to `v1.35`:

```text
deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.35/deb/ /
```

Save the file, then update apt and inspect available kubeadm versions:

```bash
apt update
apt-cache madison kubeadm
```

## Upgrade kubeadm and the cluster

The source note gives `1.35.0-1.1` as an available package version for Kubernetes `1.35.0`:

```bash
apt-get install kubeadm=1.35.0-1.1
kubeadm upgrade plan v1.35.0
kubeadm upgrade apply v1.35.0
```

The cluster upgrade can take a few minutes.

## Upgrade kubelet

Install the kubelet version and refresh its systemd configuration:

```bash
apt-get install kubelet=1.35.0-1.1
systemctl daemon-reload
systemctl restart kubelet
```

The original note also says to mark the control-plane node as schedulable.
