---
title: Keycloak Installation on Kubernetes
description: Keycloak Installation on Kubernetes using helm
published: true
date: 2021-06-14T11:59:30.927Z
tags: security, keycloak, kubernetes, helm
editor: markdown
dateCreated: 2021-06-14T09:22:01.051Z
---

# Installation on Kubernetes

Install `keycloak` using helm chart

## Environment

- `kubernetes` cluster v1.20.7
- helm v3
- [`keycloak` chart from bitnami](https://artifacthub.io/packages/helm/bitnami/keycloak)

## Monitoring

### Enable `keycloak` Metrics

Ref:

- https://github.com/bitnami/bitnami-docker-keycloak#enabling-statistics
- https://github.com/codecentric/helm-charts/blob/master/charts/keycloak/README.md#prometheus-metrics-support

```
extraEnvVars:
- name: KEYCLOAK_ENABLE_STATISTICS
  value: "true"
- name: KEYCLOAK_STATISTICS
  value: all
```

## Customization

### Custom Login URL

Ref: https://www.keycloak.org/docs/latest/server_installation/index.html#default-provider

By default, you keycloak will serve login page at `/auth`, while you may want to separate public user from applications, this can be done with `frontendUrl` proterty

```yaml
extraEnvVars:
- name: JAVA_OPTS
  # other values are omitted
  value: |-
    -Dkeycloak.frontendUrl=<custom url>
```

### Enable/Disable Features

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

Ref: 

### Disable Public Acceess to Metrics

If you enabled metrics, they will be exposed at `/auth/realms/<realm-name>/metrics` without any protection, you may want to deny requests to these metrics endpoints from public domain.

For nginx ingress, you can do this by adding an annotation as following:

```yaml
ingress:
  annotations:
    nginx.ingress.kubernetes.io/server-snippet: |-
      location ~* /auth/realms/[^/]+/metrics {
          return 403;
      }
```

### Hide Admin Console from Public Domain

Firstly, you have to set a fixed adminUrl as noted in [Hostname #default-provider](https://www.keycloak.org/docs/latest/server_installation/index.html#default-provider)

```yaml
extraEnvVars:
- name: JAVA_OPTS
  # other values are omitted
  value: |-
    -Dkeycloak.adminUrl=<custom url>
```

Then, forbid public users from accessing `/auth/admin`:

```yaml
ingress:
  annotations:
    nginx.ingress.kubernetes.io/server-snippet: |-
      location ^~ /auth/admin
          return 403;
      }
```
