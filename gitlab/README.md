# Deploying GitLab to Kubernetes

## Installing using Helm

Add the GitLab Helm repository:
```bash
$ helm repo add gitlab https://charts.gitlab.io
$ helm repo update
```

Use this command to install GitLab:
```bash
$ helm upgrade gitlab gitlab/gitlab -f gitlab/values.yaml --set global.hosts.domain=mydomain.com --timeout 600 --install
```

Your GitLab instance will be available under `gitlab.mydomain.com`.
You will need to update your DNS configuration in order to access this instance.

When everything is ready, get the generated `root` password:
```bash
$ kubectl get secret gitlab-gitlab-initial-root-password -ojsonpath='{.data.password}' | base64 --decode ; echo
Th398U10qH7nNA6IVkdkumVaX44q7xwyE1MJsgtn70o8PhtUWAhZnIikMJgL0GBO
```

## Using GitLab

You can now access GitLab. Get the allocated IP address:
```bash
$ kubectl get svc gitlab-nginx-ingress-controller
NAME                              TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                                   AGE
gitlab-nginx-ingress-controller   LoadBalancer   10.100.200.171   34.76.160.42   80:30520/TCP,443:30044/TCP,22:32655/TCP   33m
```

Make sure you map this IP address to your GitLab endpoint
by updating your DNS configuration (for example: `gitlab.mydomain.com`).

You can now use GitLab using user `root` and its generated password.
