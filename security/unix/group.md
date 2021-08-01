---
title: Unix Group
description: 
published: true
date: 2021-08-01T10:23:34.639Z
tags: security, unix
editor: markdown
dateCreated: 2021-07-30T18:21:48.652Z
---

# Unix Group

## Lookup User GroupIDs

syscall `getgrouplist`
- linux: https://man7.org/linux/man-pages/man3/getgrouplist.3.html
- freebsd: https://www.freebsd.org/cgi/man.cgi?query=getgrouplist&sektion=3&apropos=0&manpath=freebsd
- openbsd: https://man.openbsd.org/getgrouplist

Refs:

- https://git.musl-libc.org/cgit/musl/tree/src/passwd/getgrouplist.c#n12
- https://git.musl-libc.org/cgit/musl/tree/src/passwd/nscd_query.c#n18
- https://git.musl-libc.org/cgit/musl/tree/src/passwd/getgrent_a.c#n11
