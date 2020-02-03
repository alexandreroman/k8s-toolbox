# Deploying Prometheus to Kubernetes

## Installing using Helm

Add the stable Helm repository:
```bash
$ helm repo add stable https://kubernetes-charts.storage.googleapis.com
$ helm repo update
```

Use this command to install Grafana:
```bash
$ kubectl create ns monitoring
$ helm upgrade grafana stable/grafana -n monitoring -f grafana/values.yaml --install
```

This instance will automatically be connected to a Prometheus instance running at
`prometheus-server`.

Get the `admin` generated password:
```bash
$ printf $(kubectl -n monitoring get secret grafana -o jsonpath="{.data.admin-password}" | base64 --decode); echo
ot98n1lh0d0jbgRGsKaqy6kCtjwzHiPPYv5E43da
```

## Using Grafana

You can now access Grafana. Get the allocated IP address:
```bash
$ kubectl -n monitoring get svc grafana
NAME      TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)        AGE
grafana   LoadBalancer   10.100.200.211   146.148.12.149   80:31729/TCP   6m24s
```

Using your browser, hit the Grafana endpoint.
