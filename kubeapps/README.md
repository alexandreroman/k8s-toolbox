# Deploying Kubeapps to Kubernetes

## Installing using Helm

First, you need to create a service account before deploying Kubeapps:
```bash
$ kubectl apply -f kubeapps/rbac-config.yaml
```

Retrieve the token: you'll need it when you want to log into the Kubeapps dashboard:
```bash
$ printf $(kubectl get secret $(kubectl get serviceaccount kubeapps-operator -o jsonpath='{.secrets[].name}') -o jsonpath='{.data.token}' | base64 --decode);echo
eyJhbGciOiJSUzI1NiIsImtpZCI6IiJ9.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJkZWZhdWx0Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZWNyZXQubmFtZSI6Imt1YmVhcHBzLW9wZXJhdG9yLXRva2VuLXRqNXY2Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQubmFtZSI6Imt1YmVhcHBzLW9wZXJhdG9yIiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9zZXJ2aWNlLWFjY291bnQudWlkIjoiZmM2OWUzMDUtYjkxMS0xMWU5LTllYTUtMDA1MDU2OGE5YjIzIiwic3ViIjoic3lzdGVtOnNlcnZpY2VhY2NvdW50OmRlZmF1bHQ6a3ViZWFwcHMtb3BlcmF0b3IifQ.aXlZRNUyMZTu8EvtJvYiiNwjWfc__8INtH_sIF_2f2m8Ao4HiZG4g6NknR0o47WzDlekve2xPvJMHMXgeKgptwk13ojI39FPD9rp-xsSFqHAeI0P2iKs664jLfkVEsbAWxk2lylPWH0xg0eZ9YoUBpTh-gmJwfKBR95TyzXkUq71jk_hL2T2DcfIIp_CrFTlNKx56fIYzLgPRsAxXZEdyAJLCN7opEAuPCeb_0FOfWdbE8CggKEKbCDxwBtSGsVR4qQTuZE7WsjJGY-0B66UbIlVwTws5n2OHnBEdpqDK50DN3MJbkw1JWktC34tPNT-E8rClM95xQ-b6f55etwQhw
```

Add the Bitnami chart repo:
```bash
$ helm repo add bitnami https://charts.bitnami.com/bitnami
$ helm repo update
```

Use this command to install Kubeapps:
```bash
$ kubectl create ns kubeapps
$ helm upgrade kubeapps bitnami/kubeapps -n kubeapps -f kubeapps/values.yaml --version 3.3.1 --install
```

## Using Kubeapps

Kubeapps dashboard is available under its own IP address:
```bash
$ kubectl -n kubeapps get svc kubeapps
NAME       TYPE           CLUSTER-IP       EXTERNAL-IP                   PORT(S)        AGE
kubeapps   LoadBalancer   10.100.200.224   10.197.47.135,100.64.112.31   80:31222/TCP   26m
```
