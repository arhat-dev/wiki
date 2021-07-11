---
title: Nix
description: Nix Package Manager
published: true
date: 2021-07-11T13:18:02.391Z
tags: package-manager, nix
editor: markdown
dateCreated: 2021-07-11T13:13:48.715Z
---

# Nix

Nix Package Manager

## Usage

### Manage Channels (package lists)

```bash
nix-channel --add <http-url> {optional-name}
```

Wellknown Channels:
- https://nixos.org/channels/nixpkgs-unstable
- 

### Install System Packages

```bash
nix-env -iA
```