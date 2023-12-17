# Jupyterhub

This is a Jupyterhub deployment for the kind-win cluster, this is using GitOps through FluxCD.

## secret.yaml

Secret manifest for the jupyterhub configuration

```yaml
hub:
  config:
    cookieSecret: secret
    GenericOAuthenticator:
      client_id: client
      client_secret: secret
      oauth_callback_url: http://localhost:8080/hub/oauth_callback
      authorize_url: https://keycloak.local/realms/default/protocol/openid-connect/auth
      token_url: https://keycloak.local/realms/default/protocol/openid-connect/token
      userdata_url: https://keycloak.local/realms/default/protocol/openid-connect/userinfo
      logout_redirect_url: http://keycloak.local/realms/default/protocol/openid-connect/logout
  db:
    type: postgres
    url: postgresql://{user}:{password}@databases.postgres.svc.cluster.local:5432/jupyterhub
```
