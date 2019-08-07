# Deploying Jenkins to Kubernetes

## Installing using Helm

Use this command to install Jenkins:
```bash
$ helm upgrade jenkins stable/jenkins -f jenkins/values.yaml --install
```

When everything is ready, get the generated admin password:
```bash
$ printf $(kubectl get secret --namespace default jenkins -o jsonpath="{.data.jenkins-admin-password}" | base64 --decode);echo
7li4SwKEnO
```

## Using Jenkins

You can now access Jenkins. Get the allocated IP address:
```bash
$ kubectl get svc jenkins
NAME      TYPE           CLUSTER-IP      EXTERNAL-IP                   PORT(S)        AGE
jenkins   LoadBalancer   10.100.200.12   10.197.47.129,100.64.112.31   80:30985/TCP   5m35s
```

In this example, hit `10.197.47.129` to reach Jenkins.
Use `admin` and your generated password to log in.
