# Deploying Helm to Kubernetes

Deploy the Tiller configuration to your Kubernetes cluster:
```bash
$ kubectl apply -f helm/rbac-config.yaml
```

Now you can deploy the Tiller service:
```bash
$ helm init --service-account tiller
```

Check everything is working fine (nothing will be displayed):
```bash
$ helm ls
```
