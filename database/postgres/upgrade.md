---
title: Upgrade Postgres
description: 
published: true
date: 2021-07-19T10:03:44.811Z
tags: maintenance, database
editor: markdown
dateCreated: 2021-07-19T09:44:54.526Z
---

# Upgrade Postgres

__NOTE:__ This wiki is mainly for [`patroni`](https://github.com/zalando/patroni) managed postgres clusters, inside [`spilo`](https://github.com/zalando/spilo) container, and spilo containers are managed by [`postgres-operator`](https://github.com/zalando/postgres-operator)

## Upgrade using `postgres-operator`

Ref:

- https://github.com/zalando/postgres-operator/blob/master/docs/administrator.md#in-place-major-version-upgrade

## Upgrade Manually with `pg_upgrade`

1. Check current version of postgres, both environment variable `${PGVERSION}` and file `${PGROOT}/data/PG_VERSION`, only the value stored in file `${PGROOT}/data/PG_VERSION` is respected by patroni

2. Depending on which version you want to upgrade to, have a look at `https://www.postgresql.org/docs/${TARGET_PGVERSION}/pgupgrade.html`

3. Do the upgrade (in place)

Ref:

- https://wiki.postgresql.org/wiki/In-place_upgrade
- https://stackoverflow.com/questions/35682315/postgresql-inplace-database-upgrade

```bash
/usr/lib/postgresql/${TARGET_PGVERSION}/bin/pg_upgrade --check --link \
  --old-datadir=/home/postgres/pgdata/pgroot/data \
  --new-datadir=/home/postgres/pgdata/pgroot/data \
  --old-bindir=/usr/lib/postgresql/${OLD_PGVERSION}/bin \
  --new-bindir=/usr/lib/postgresql/${TARGET_PGVERSION}/bin \
  --old-options '-c config_file=/home/postgres/pgdata/pgroot/data/postgresql.conf' \
  --new-options '-c config_file=/home/postgres/pgdata/pgroot/data/postgresql.conf'
```