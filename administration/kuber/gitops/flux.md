# Flux

### Install

* Create git repo
* register ssh key
* export KUBECONFIG=/path/to/kubeconfig

```bash
flux bootstrap git --url=ssh://git@gitlab.example.com/flux-project.git --branch=main --private-key-file=/Users/cotsom/.ssh/id_rsa --path=clusters/my-cluster
```
