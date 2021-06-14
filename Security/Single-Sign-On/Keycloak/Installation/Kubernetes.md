---
title: Keycloak Installation on Kubernetes
description: Keycloak Installation on Kubernetes using helm
published: false
date: 2021-06-14T10:41:45.457Z
tags: security, keycloak, kubernetes, helm
editor: markdown
dateCreated: 2021-06-14T09:22:01.051Z
---

# Installation on Kubernetes

Install `keycloak` using helm

## Enable Features

Ref: https://www.keycloak.org/docs/latest/server_installation/index.html#profiles

- Add Script Authenticator for custom login flow

  ```bash
  JAVA_OPTS="${JAVA_OPTS} -Dkeycloak.profile.feature.scripts=enabled"
  ```
