---
title: Upgrade Postgres
description: 
published: true
date: 2021-07-19T09:44:54.526Z
tags: maintenance, database
editor: markdown
dateCreated: 2021-07-19T09:44:54.526Z
---

# Upgrade Postgres

__NOTE:__ This wiki is mainly for [`patroni`](https://github.com/zalando/patroni) managed postgres clusters, inside [`spilo`](https://github.com/zalando/spilo) container, and spilo containers are managed by [`postgres-operator`](https://github.com/zalando/postgres-operator)

1. Check current version of postgres, both environment variable `${PGVERSION}` and file `${PGROOT}/data/PG_VERSION`, only the value stored in file `${PGROOT}/data/PG_VERSION` is respected by patroni

2. Depending on which version you want to upgrade to, have a look at `https://www.postgresql.org/docs/${TARGET_PGVERSION}/pgupgrade.html`