---
title: Commit Message
description: 
published: true
date: 2021-07-07T15:52:22.435Z
tags: git, commit, convension
editor: markdown
dateCreated: 2021-07-02T18:31:52.038Z
---

# Commit Message

Refs:
- origin: [angular.js Developer Guide #commits](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits)
- https://www.conventionalcommits.org/en/v1.0.0/
- https://github.com/conventional-changelog/conventional-changelog
- https://www.v2ex.com/t/652309

## Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

## Commit Types

Final production related

- `feat`: new feature
- `fix`: bug fix
- `perf`: performance improvement
- `test`: update/fix/change test cases/code

Repo maintenance related

- `docs`: documentation only changes, should not touch any code
- `refactor`: refactoring of the codebase
- `style`: formatting change
  - e.g. trim trailing whitespaces, change spaces to tabs
- [`chore`](https://www.merriam-webster.com/dictionary/chore): all kinds of small/trivial tasks and daily routine
- `nit` [(short for nit pick)](https://en.wikipedia.org/wiki/Nitpicking): a small change that may not be very important, but is technically correct

## Tools

- https://github.com/talos-systems/conform
