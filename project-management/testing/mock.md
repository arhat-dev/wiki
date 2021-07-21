---
title: Mock Test
description: 
published: true
date: 2021-07-21T07:20:59.906Z
tags: testing, mock
editor: markdown
dateCreated: 2021-07-21T07:20:59.906Z
---

# Mock Test

Refs:

- https://stackoverflow.com/questions/2665812/what-is-mocking
- https://stackoverflow.com/questions/38181/when-should-i-mock

## Major Usecase

- Remove need of unstable/flaky/unimplemented dependencies to minimize false positive test result
	- If the dependencies are stable enough, and contain complex logic, do integration test instead
- Check whether method called, and how many times it being called
