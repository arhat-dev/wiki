---
title: Nix
description: Nix Package Manager
published: true
date: 2021-07-11T13:47:49.282Z
tags: package-manager, nix
editor: markdown
dateCreated: 2021-07-11T13:13:48.715Z
---

# Nix

Nix Package Manager

Resources:
- https://nixos.org/manual/nix/stable/
- https://nixos.wiki/wiki/Nix_to_Debian_phrasebook
- https://nixos.wiki/wiki/Cheatsheet

## Usage

### Manage Channels (package lists)

Ref:
- https://nixos.org/manual/nix/stable/#sec-nix-channel
- https://nixos.wiki/wiki/Nix_channels
- https://status.nixos.org/
- https://matrix.ai/blog/intro-to-nix-channels-and-reproducible-nixos-environment/
- https://channels.nixos.org/

File Storage:
- System Channels (requires root privilege): `/etc/nixos/configuration.nix`

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
- nixpkgs-unstable: `https://nixos.org/channels/nixpkgs-unstable`
- nixos-channels: `https://channels.nixos.org/nixos-${MAJOR}.${MINOR}-small`

### Install Packages

Search a package

```bash
nix search

# nix-env -qa
```

```bash
nix-env -iA
```