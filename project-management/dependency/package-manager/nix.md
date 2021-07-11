---
title: Nix
description: Nix Package Manager
published: true
date: 2021-07-11T13:23:21.124Z
tags: package-manager, nix
editor: markdown
dateCreated: 2021-07-11T13:13:48.715Z
---

# Nix

Nix Package Manager

## Usage

### Manage Channels (package lists)

Ref: https://nixos.org/manual/nix/stable/#sec-nix-channel

File Storage:
- System Channels (requires root privilege): /etc/nixos/configuration.nix

List subscribed channels

```bash
nix-channel --list
```

Subscribe a channel (add a package list)

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