# Deploying Vault to Kubernetes

## Installing using Helm

As of now, Hashicorp does not provide a Chart repository for Vault.
You need to [clone the Git repository](https://github.com/hashicorp/vault-helm/):
```bash
$ git clone https://github.com/hashicorp/vault-helm.git
```

Use this command to install Vault:
```bash
$ helm upgrade vault vault-helm -f vault/values.yaml --install
```

## Using Vault

This Vault instance is running in `dev` mode: all credentials are stored
in memory, and the vault instance is unsealed by default on start.

You should access Vault from your apps using an internal cluster service.

Vault UI is available under an external IP address:
```bash
kubectl get svc vault-ui
NAME       TYPE           CLUSTER-IP       EXTERNAL-IP                   PORT(S)        AGE
vault-ui   LoadBalancer   10.100.200.254   10.197.47.134,100.64.112.31   80:31514/TCP   65s
```

Use this token to sign in: `root`.
