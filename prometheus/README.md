# Deploying Prometheus to Kubernetes

## Installing using Helm

Add the stable Helm repository:
```bash
$ helm repo add stable https://kubernetes-charts.storage.googleapis.com
$ helm repo update
```

Use this command to install Prometheus:
```bash
$ kubectl create ns monitoring
$ helm upgrade prometheus stable/prometheus -n monitoring -f prometheus/values.yaml --version 10.3.1 --install
```

## Using Prometheus

Your Prometheus server is available as a `ClusterIP` service at `prometheus-server`:
```bash
$ kubectl -n monitoring get svc prometheus-server
```

Add these pod annotations in your app to scrape metrics:
```yaml
metadata:
  annotations:
    prometheus.io/scrape: "true"
    prometheus.io/path: /metrics
    prometheus.io/port: "8080"
```
