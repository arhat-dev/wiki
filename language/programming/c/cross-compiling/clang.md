---
title: Cross Compiling Using Clang Toolchain
description: 
published: true
date: 2021-08-21T04:33:03.929Z
tags: language, c, cross-compile, corss
editor: markdown
dateCreated: 2021-08-17T21:44:10.751Z
---

# Clang Cross Compiling

Refs:
- [https://mcilloni.ovh/2021/02/09/cxx-cross-clang/](https://mcilloni.ovh/2021/02/09/cxx-cross-clang/)

## Available Targets

See [https://github.com/llvm/llvm-project/blob/llvmorg-11.0.0/llvm/include/llvm/ADT/Triple.h](https://github.com/llvm/llvm-project/blob/llvmorg-11.0.0/llvm/include/llvm/ADT/Triple.h) (replace `11.0.0` according to your clang version)

## In Container

For a different OS

- `ghcr.io/arhat-dev/freebsd`
- `ghcr.io/arhat-dev/openbsd`
