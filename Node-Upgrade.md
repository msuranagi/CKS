# Worker Node Kubernetes Version Upgrade

The commands in this note describe upgrading `node01` to Kubernetes v1.35.0.

## Connect to the node

Run the commands on `node01`. From the control-plane node, connect with:

```bash
ssh node01
```

## Update the package repository

Edit the Kubernetes apt repository file:

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

The source note gives `1.35.0-1.1` as the available package version for Kubernetes `1.35.0`:

```bash
apt-get install kubeadm=1.35.0-1.1
kubeadm upgrade node
```

## Upgrade kubelet

Install the kubelet version and refresh its systemd configuration:

```bash
apt-get install kubelet=1.35.0-1.1
systemctl daemon-reload
systemctl restart kubelet
```

Return to the control-plane node by running `exit` or `logout`, or pressing `Ctrl+D`.
