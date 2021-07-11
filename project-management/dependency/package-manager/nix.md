---
title: Nix
description: Nix Package Manager
published: true
date: 2021-07-11T13:19:54.082Z
tags: package-manager, nix
editor: markdown
dateCreated: 2021-07-11T13:13:48.715Z
---

# Nix

Nix Package Manager

## Usage

### Manage Channels (package lists)

List existing channels

```bash
nix-channel --list
```

Add a channel

```bash
nix-channel --add <http-url> {optional-name}
```

Update channels

```bash
nix-channel --update {optional-space-separated-names}
```

Wellknown Channels:
- https://nixos.org/channels/nixpkgs-unstable
- 

### Install System Packages

```bash
nix-env -iA
```