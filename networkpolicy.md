# NetworkPolicy Egress Rules

Create a policy that allows egress from the `internal` application only to the `payroll` and `mysql` pods, on their specified ports. The policy also allows DNS traffic over TCP and UDP port 53.

The source note includes ingress traffic in the policy to make testing the rules in the UI possible.

## Policy details

| Setting | Value |
| --- | --- |
| Policy name | `internal-policy` |
| Policy type | Egress and Ingress |
| Selected pod label | `name: internal` |
| Egress destination | `name: payroll`, TCP port `8080` |
| Egress destination | `name: mysql`, TCP port `3306` |
| DNS egress | TCP and UDP port `53` |

## Manifest

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: internal-policy
  namespace: default
spec:
  podSelector:
    matchLabels:
      name: internal
  policyTypes:
    - Egress
    - Ingress
  ingress:
    - {}
  egress:
    - to:
        - podSelector:
            matchLabels:
              name: mysql
      ports:
        - protocol: TCP
          port: 3306
    - to:
        - podSelector:
            matchLabels:
              name: payroll
      ports:
        - protocol: TCP
          port: 8080
    - ports:
        - port: 53
          protocol: UDP
        - port: 53
          protocol: TCP
```
