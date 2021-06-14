---
title: Keycloak Installation on Kubernetes
description: Keycloak Installation on Kubernetes using helm
published: false
date: 2021-06-14T11:00:19.518Z
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

Useful features:
- `script` - The script authenticator, which allows you defining your custom login flow using JavaScript,
  - see https://www.keycloak.org/docs/latest/server_development/#_script_providers
- `docker`
- `client_policies`
