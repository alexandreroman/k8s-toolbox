# Deploying Nexus to Kubernetes

## Installing using Helm

First, you need to know on which endpoint this Nexus instance will be exposed:
```bash
$ export NEXUS_ENDPOINT=nexus.fqdn.com
```

Use this command to install Nexus:
```bash
$ kubectl create ns nexus
$ helm upgrade nexus stable/sonatype-nexus -n nexus -f nexus/values.yaml --set nexusProxy.env.nexusHttpHost=$NEXUS_ENDPOINT --version 1.22.0 --install
```

## Using Nexus

You can now access Nexus using your endpoint. Make sure you map your DNS
configuration to the load balancer IP address:
```bash
$ kubectl -n nexus get svc nexus-sonatype-nexus
NAME                   TYPE           CLUSTER-IP       EXTERNAL-IP                   PORT(S)        AGE
nexus-sonatype-nexus   LoadBalancer   10.100.200.188   10.197.47.130,100.64.112.31   80:30329/TCP   42s
```

Get the `admin` password using this command (using the Nexus pod id):
```bash
$ kubectl -n nexus exec -it nexus-sonatype-nexus-5b86d95977-766vx -- cat /nexus-data/admin.password
Defaulting container name to nexus.
Use 'kubectl describe pod/nexus-sonatype-nexus-5b86d95977-766vx -n nexus' to see all of the containers in this pod.
435dc320-ff87-4f2b-b28c-6c27b846f032%
```

When you first sign in to Nexus, you'll be asked to set up a new admin password.
