# NGINX Ingress Rewrite Target

Different Ingress controllers provide different customization options. This note covers the NGINX Ingress `rewrite-target` annotation.

## Why rewrite the path?

Suppose the watch and wear applications serve their pages at their service roots:

```text
http://<watch-service>:<port>/
http://<wear-service>:<port>/
```

Ingress paths can route requests to those services:

```text
http://<ingress-service>:<ingress-port>/watch -> http://<watch-service>:<port>/
http://<ingress-service>:<ingress-port>/wear  -> http://<wear-service>:<port>/
```

Without rewriting, the incoming path is forwarded to the backend:

```text
http://<ingress-service>:<ingress-port>/watch -> http://<watch-service>:<port>/watch
http://<ingress-service>:<ingress-port>/wear  -> http://<wear-service>:<port>/wear
```

If the backend applications do not serve `/watch` or `/wear`, these requests can return a 404. The `rewrite-target` annotation rewrites the path configured under `rules.http.paths.path` to the annotation's target. The source note describes this as a search-and-replace operation:

```text
replace(path, rewrite-target)
replace("/path", "/")
```

## Example: replace a path with `/`

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: test-ingress
  namespace: critical-space
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
    - http:
        paths:
          - path: /pay
            pathType: Prefix
            backend:
              service:
                name: pay-service
                port:
                  number: 8282
```

## Example: capture and preserve part of the path

The source note also gives this replacement:

```text
replace("/something(/|$)(.*)", "/$2")
```

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: rewrite
  namespace: default
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /$2
spec:
  rules:
    - host: rewrite.bar.com
      http:
        paths:
          - path: /something(/|$)(.*)
            pathType: Prefix
            backend:
              service:
                name: http-svc
                port:
                  number: 80
```
