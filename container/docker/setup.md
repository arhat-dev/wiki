---
title: Docker Setup
description: Operations after docker installation
published: true
date: 2021-08-18T08:57:12.763Z
tags: docker
editor: markdown
dateCreated: 2021-06-28T10:38:40.413Z
---

# Docker Setup

## Use [`lima`](https://github.com/lima-vm/lima)

Refs:
- [https://gist.github.com/nrjdalal/e70249bb5d2e9d844cc203fd11f74c55](https://gist.github.com/nrjdalal/e70249bb5d2e9d844cc203fd11f74c55)

```bash
temp_build_dir="$(mktemp -d)"
cd "${temp_build_dir}"
# python3.8 may not work for cpu detection in meson build
# see: https://gist.github.com/nrjdalal/e70249bb5d2e9d844cc203fd11f74c55#gistcomment-3808885
pipenv --python 3.9
pipenv shell

# Install necessary packages for building
brew install libffi gettext glib pkg-config autoconf automake pixman ninja

# Build qemu with aarch64 hvf support
git clone --branch hvf-arm-v8 --depth 1 https://github.com/agraf/qemu.git
cd qemu

mkdir build && cd build
../configure --target-list=aarch64-softmmu --enable-hvf
make -j8

# Install qemu
sudo make install

# Clean up
cd ../../ && sudo rm -rf qemu
```

## Setup usable multi-arch support

Ref:
- [https://github.com/docker/setup-qemu-action](https://github.com/docker/setup-qemu-action)
- [https://github.com/tonistiigi/binfmt](https://github.com/tonistiigi/binfmt)
- [https://github.com/docker/buildx/blob/master/docs/reference/buildx_bake.md](https://github.com/docker/buildx/blob/master/docs/reference/buildx_bake.md)

## Useful command snippets

### Enter docker vm

Ref: https://github.com/justincormack/nsenter1

```bash
docker run -it --rm --privileged --pid=host justincormack/nsenter1
```
