# Configuration

```hcl
component "grafana" {
  namespace = "grafana"

  # Params default values

  publicURL = "" # required, the full URL to reach the Grafana instance, e.g. https://dashboard.company.com

  secret = {
    # override this section only if you are not using the default store from the external-secrets component
    store = {
      name = "default"
      kind = "ClusterSecretStore"
    }
    key = "" # required, should be the store-specific key to the secret, e.g. the Vault or AWS Secrets Manager key
  }


  dex = {
    issuer = "" # required, Dex OIDC issuer URL

    # override this section only if you are using
    # a different Dex instance than the default one
    name = "dex"
    namespace = "dex"
  }
}
```

## Secrets

Secrets referenced by the configuration must be provisioned in the backend service of your choice before installing Grafana.

Unless you changed the configuration of the External Secret component or manually provisioned a custom `SecretStore` resource, you don't need to override the `store` section of each secret reference.
