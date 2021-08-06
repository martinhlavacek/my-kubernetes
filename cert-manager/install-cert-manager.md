# Cert manager

1. Install
[Kubernetes | cert-manager](https://cert-manager.io/docs/installation/kubernetes/)

```bash
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.yaml
```

> overeni `kubectl get pods —namespace cert-manager`
> viz obrazek v url nahore

## test
vytvorit file
```
cat <<EOF > test-resources.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: cert-manager-test
---
apiVersion: cert-manager.io/v1
kind: Issuer
metadata:
  name: test-selfsigned
  namespace: cert-manager-test
spec:
  selfSigned: {}
---
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: selfsigned-cert
  namespace: cert-manager-test
spec:
  dnsNames:
    - example.com
  secretName: selfsigned-cert-tls
  issuerRef:
    name: test-selfsigned
EOF
```

a spustit 
```bash 
kubectl apply -f test-resources.yaml
```

## Delete test
```bash
kubectl delete -f test-resources.yaml
```