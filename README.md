# Kubernetes Toolbox

This repository contains a collection of useful tools for your Kubernetes clusters.

All these tools are installed using [Helm](https://helm.sh) Charts.
Make sure you [deploy Helm into your cluster](https://helm.sh/docs/using_helm/#installing-helm)
first.

**Disclaimer**: these tools are not production-ready! Use this repository to easily
get hands on fancy tools for your Kubernetes cluster, but don't trust any of these
scripts to run your production workloads ;)

Make sure you first [deploy Helm 3 to your cluster](https://helm.sh/docs/intro/install/).

So far, here are the tools you can deploy:
 - [Kubeapps](kubeapps) ([Helm dashboard by Bitnami](https://kubeapps.com))
 - Monitoring
    - [Prometheus](prometheus)
    - [Grafana](grafana)
 - Continuous Integration tools
    - [Concourse](concourse)
    - [Jenkins](jenkins)
    - [GitLab](gitlab)
 - Content repositories:
    - [Artifactory](artifactory)
    - [Harbor](harbor)
    - [Nexus](nexus)
 - Credentials managers
    - [Vault](vault)

## Contribute

Contributions are always welcome!

Feel free to open issues & send PR.

## License

Copyright &copy; 2020 [VMware Software, Inc](https://vmware.com).

This project is licensed under the [Apache Software License version 2.0](https://www.apache.org/licenses/LICENSE-2.0).
