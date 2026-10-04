# Kubebench

## Download Kubebench
curl -L https://github.com/aquasecurity/kube-bench/releases/download/v0.16.0/kube-bench_0.16.0_linux_amd64.tar.gz -o kube-bench_0.16.0_linux_amd64.tar.gz
tar -xvf kube-bench_0.16.0_linux_amd64.tar.gz

## How to Run - Run this in Control Plane
Run kube Bench in control plane
./kube-bench --config-dir `pwd`/cfg --config `pwd`  /cfg/config.yaml 

## Example output from kube Bench

[PASS] 1.2.17 Ensure that the admission control plugin NodeRestriction is set (Automated)
[PASS] 1.2.18 Ensure that the --insecure-bind-address argument is not set (Automated)
[FAIL] 1.2.19 Ensure that the --insecure-port argument is set to 0 (Automated)

## Sample of how to fix
Issue: Insecure port enabled
Fix: Add to /etc/kubernetes/manifests/kube-apiserver.yaml
--insecure-port=0
