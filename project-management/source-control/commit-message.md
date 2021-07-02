---
title: Commit Message
description: 
published: true
date: 2021-07-02T18:40:15.369Z
tags: git, commit, convension
editor: markdown
dateCreated: 2021-07-02T18:31:52.038Z
---

# Commit Message

Refs:
- origin: [angular.js Developer Guide](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#commits)
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

- `docs`: documentation only changes
- `refactor`: refactoring of the codebase
- `style`: formatting change (e.g. trim trailing whitespaces, change spaces to tabs)
- `chore`: all kinds of small tasks
- `nit`: short for nit pick, a small change that may not be very important, but is technically correct
	- source: https://en.wikipedia.org/wiki/Nitpicking
