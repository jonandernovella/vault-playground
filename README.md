# Vault playground

This box contains an environment for running Vault using Consul as storage backend

## Deploy Consul and Vault

Using helm, please run:
```bash
helm upgrade --install -f /vagrant/vault-values.yaml vault-test vault-config/vault-chart/
helm upgrade --install -f /vagrant/consul-values.yaml consul-test consul-config/consul-chart
```

## Unseal Vault

Obtain the root token and unsealing keys by running:
```bash
kubectl exec -it vault-test-0 -- vault operator init
```

Unseal the vault by using three of the unsealing keys provided by the init command:
```bash
kubectl exec -it vault-test-0 -- vault operator unseal
```

Note that you need to run it three times, as the key threshold is 3. It is possible to generate new unseal keys, provided you have a quorum of existing unseal keys shares and using:

```bash
vault operator rekey
```

The Consul and Vault UI can be accessed at http://127.0.0.1:30393 and http:127.0.0.1:30394 respectively.
