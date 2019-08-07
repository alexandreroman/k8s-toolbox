# Deploying Artifactory to Kubernetes

## Installing using Helm

Add the JFrog Helm repository:
```bash
$ helm repo add jfrog https://charts.jfrog.io
$ helm repo update
```

Use this command to install Artifactory:
```bash
$ helm upgrade artifactory jfrog/artifactory -f artifactory/values.yaml --install
```

## Using Artifactory

You can now access Artifactory. Get the allocated IP address:
```bash
$ kubectl get svc artifactory-artifactory-nginx
NAME                            TYPE           CLUSTER-IP       EXTERNAL-IP                   PORT(S)                      AGE
artifactory-artifactory-nginx   LoadBalancer   10.100.200.199   10.197.47.128,100.64.112.31   80:31911/TCP,443:31753/TCP   39
```

In this example, hit `10.197.47.128` to reach Artifactory.
Use `admin` and `password` to log in.
