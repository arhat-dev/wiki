---
title: Docker Setup
description: Operations after docker installation
published: true
date: 2021-09-01T15:15:10.934Z
tags: docker
editor: markdown
dateCreated: 2021-06-28T10:38:40.413Z
---

# Docker Setup

## Use [`lima`](https://github.com/lima-vm/lima)

### Compile qemu for mac m1 with `hvf` support

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
- [https://github.com/dbhi/qus](https://github.com/dbhi/qus)

1. Register qemu-user binaries in `/qus/bin`

```bash
$ sudo nerdctl run --rm --privileged -e QEMU_BIN_DIR=/qus -it aptman/qus -s -- -p
```

2. Copy qemu-user binaries

- Option 1: From aptman/qus image (recommended)

```bash
$ sudo nerdctl run --rm -it -v /qus:/host-qus aptman/qus -i sh
# in container
$ mv /qus/bin /host-qus/bin
```

- Option 2: Find them installed by system package manger

```bash
# for debian based distro
$ apt-get update && apt-get install -y qemu-user-static

$ mkdir -p /qus/bin
$ cp /usr/bin/qemu-*-static /qus/bin/.
```

- Option 3: Download them from release assets of https://github.com/multiarch/qemu-user-static (x86_64 host only) or https://github.com/dbhi/qus (`qemu-xxx-static_${HOST}.tgz` for HOST arch)

3. (For arm64 host users) You may need to enable `arm` emulation explicitly due to `qemu-binfmt-conf.sh` assuming your cpu supports aarch32 and will not register `/proc/sys/fs/binfmt_misc/qemu-arm` for arm binaries. To do this, run the script with environment variable `HOST_ARCH=x86_64` and set `TARGET_ARCH` to `arm`

```bash
$ sudo nerdctl run --rm --privileged -e HOST_ARCH=x86_64 aptman/qus -s -- -p arm
```

## Useful command snippets

### Enter docker vm

Ref: https://github.com/justincormack/nsenter1

```bash
docker run -it --rm --privileged --pid=host justincormack/nsenter1
```
