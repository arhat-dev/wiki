---
title: Keycloak Installation on Kubernetes
description: Keycloak Installation on Kubernetes using helm
published: true
date: 2021-06-14T11:29:51.286Z
tags: security, keycloak, kubernetes, helm
editor: markdown
dateCreated: 2021-06-14T09:22:01.051Z
---

# Installation on Kubernetes

Install `keycloak` using helm

## Enable/Disable Features

Ref: https://www.keycloak.org/docs/latest/server_installation/index.html#profiles

To enable/disable a feature in helm values, we can use the environment variable JAVA_OPTS

```yaml
extraEnvVars:
- name: JAVA_OPTS
  # other values are omitted
  value: |-
    -Dkeycloak.profile.feature.<feature name>=<enabled | disabled>
```

Useful features not enabled by default:
- `script` - The script authenticator, which allows you defining your custom login flow using JavaScript,
  - see https://www.keycloak.org/docs/latest/server_development/#_script_providers
- `docker`
- `client_policies`

## Hardening

To protect the installed `keycloak` instance, there are extra work to do.

### Disable Public Acceess to Metrics

If you enabled metrics, they will be exposed at `/auth/realms/<realm-name>/metrics` without any protection, you may want to deny requests to these metrics endpoints from public domain, and for nginx ingress, add a annotation as following:

```yaml
ingress:
  annotations:
    nginx.ingress.kubernetes.io/server-snippet: |-
      location ~* /auth/realms/[^/]+/metrics {
          return 403;
      }
```

### Hide Admin Console from Public Domain

Firstly, you have to set a fixed adminUrl

```yaml
extraEnvVars:
- name: JAVA_OPTS
  # other values are omitted
  value: |-
    -Dkeycloak.adminUrl=<custom url>
```

Then, forbid user from accessing `/auth/admin`

```yaml
ingress:
  ## Set to true to enable ingress record generation
  ##
  enabled: true

  ## Set this to true in order to add the corresponding annotations for cert-manager
  ##
  certManager: true

  ## When the ingress is enabled, a host pointing to this will be created
  ##
  hostname: auth.arhat.dev

  ## Override API Version (automatically detected if not set)
  ##
  apiVersion:

  ## Ingress Path
  ##
  path: /

  ## Ingress Path type
  ##
  pathType: Prefix

  ## Ingress annotations done as key:value pairs
  ## For a full list of possible ingress annotations, please see
  ## ref: https://github.com/kubernetes/ingress-nginx/blob/master/docs/user-guide/nginx-configuration/annotations.md
  ##
  ## If certManager is set to true, annotation kubernetes.io/tls-acme: "true" will automatically be set
  ##
  annotations:
```