# Self-Hosted Sentry for CloudNativeDays

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [How to set up](#how-to-set-up)
  - [Sentry VM](#sentry-vm)
  - [Redis VM](#redis-vm)
  - [PostgreSQL VM](#postgresql-vm)
- [Reference](#reference)

<!-- /code_chunk_output -->

## How to set up

### Sentry VM

Clone the repo and run `./install.sh` in your local check-out.

```sh
./install.sh
```

Then, modify connection settings.

`relay/config.yml`

```diff
- redis: redis:redis:6379
+ redis: redis://192.168.0.201:6379
```

`sentry.conf.yml`

```diff
- SENTRY_OPTIONS["redis.clusters"] = {
-     "default": {
-         "hosts": {0: {"host": "redis", "password": "", "port": "6379", "db": "0"}}
-     }
- }
+ SENTRY_OPTIONS["redis.clusters"] = {
+     "default": {
+         "hosts": {0: {"host": "192.168.0.201", "password": "", "port": "6379", "db": "0"}}
+     }
+ }
```

Run `docker compose up -d` in your local check-out.

```sh
docker compsoe up -d
```

### Redis VM

Clone the repo and run `docker compose up -d` in your `redis/`.

```sh
cd redis; docker compose up -d
```

### PostgreSQL VM

TBD

## Reference

- [getsentry/self-hosted](https://github.com/getsentry/self-hosted)
