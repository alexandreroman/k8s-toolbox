# Deploying Vault to Kubernetes

## Installing using Helm

As of now, Hashicorp does not provide a Chart repository for Vault.
You need to [clone the Git repository](https://github.com/hashicorp/vault-helm/):
```bash
$ git clone https://github.com/hashicorp/vault-helm.git
```

You may want to select a tagged release:
```bash
$ cd vault-helm && git checkout v0.3.3 && cd -
```

Use this command to install Vault:
```bash
$ kubectl create ns vault
$ helm upgrade vault vault-helm -n vault -f vault/values.yaml --install
```

## Using Vault

This Vault instance is running in `dev` mode: all credentials are stored
in memory, and the vault instance is unsealed by default on start.

You should access Vault from your apps using an internal cluster service.

Check Vault is running using these commands:
```bash
$ kubectl -n vault port-forward vault-0 8200
$ export VAULT_ADDR=http://127.0.0.1:8200
$ vault status
```

Use token `root` to login:
```bash
$ vault login
Token (will be hidden): root
Success! You are now authenticated. The token information displayed below
is already stored in the token helper. You do NOT need to run "vault login"
again. Future Vault requests will automatically use this token.

Key                  Value
---                  -----
token                root
token_accessor       8pOjQwkoInyYtOQU34sPWHsJ
token_duration       ∞
token_renewable      false
token_policies       ["root"]
identity_policies    []
policies             ["root"]
```
