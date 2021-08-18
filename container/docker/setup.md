---
title: Docker Setup
description: Operations after docker installation
published: true
date: 2021-08-18T07:18:24.198Z
tags: docker
editor: markdown
dateCreated: 2021-06-28T10:38:40.413Z
---

# Docker Setup

## Setup usable multi-arch support

Ref:
- [https://github.com/docker/setup-qemu-action](https://github.com/docker/setup-qemu-action)
- [https://github.com/tonistiigi/binfmt](https://github.com/tonistiigi/binfmt)
- [https://github.com/docker/buildx/blob/master/docs/reference/buildx_bake.md](https://github.com/docker/buildx/blob/master/docs/reference/buildx_bake.md)
- [https://gist.github.com/nrjdalal/e70249bb5d2e9d844cc203fd11f74c55](https://gist.github.com/nrjdalal/e70249bb5d2e9d844cc203fd11f74c55)

## Useful command snippets

### Enter docker vm

Ref: https://github.com/justincormack/nsenter1

```bash
docker run -it --rm --privileged --pid=host justincormack/nsenter1
```
