# Deploying Harbor to Kubernetes

## Installing using Helm

Add the Harbor Helm repository:
```bash
$ helm repo add harbor https://helm.goharbor.io
$ helm repo update
```

Since Harbor will generate a TLS certificate, you need to specify the endpoint URL:
```bash
$ export HARBOR_ENDPOINT=harbor.fqdn.com
```

Use this command to install Harbor:
```bash
$ kubectl create ns harbor
$ helm upgrade harbor bitnami/harbor -n harbor -f harbor/values.yaml --set externalURL=https://$HARBOR_ENDPOINT --set service.tls.commonName=$HARBOR_ENDPOINT --version 3.1.3 --install
```

## Using Harbor

You can now access Harbor. Get the allocated IP address:
```bash
$ kubectl -n harbor get svc harbor
NAME     TYPE           CLUSTER-IP       EXTERNAL-IP                   PORT(S)                                     AGE
harbor   LoadBalancer   10.100.200.185   10.197.47.129,100.64.112.31   80:32276/TCP,443:30176/TCP,4443:31091/TCP   84m
```

Make sure you map this IP address to your Harbor endpoint
by updating your DNS configuration.

You can now use Harbor: use `admin` and `changeme` to log in.

Since the default configuration uses self-signed certificates, you will need
to update your configuration to trust these certificates.
[Read this page](https://tosbourn.com/getting-os-x-to-trust-self-signed-ssl-certificates/)
if you're using Mac OS X.
