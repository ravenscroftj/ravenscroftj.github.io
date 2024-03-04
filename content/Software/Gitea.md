---
title: Gitea
date: 2024-03-03
tags:
  - software
public: true
---
Gitea is a lightweight version control hub that provides git hosting, project management, release management and packages. It's very powerful and very efficient (written in Go and uses minimal memory).

## Actions

Gitea have recently introduced a CI actions feature which is compatible with github's actions. I am compiling notes on this under #GiteaActions


## Python Packages

- Official docs: https://docs.gitea.com/usage/packages/pypi

Best strategy with PDM seems to be:

1. use `pdm build`
2. upload package with `twine`:
  
```shell
    twine upload \
       --repository-url https://gitea.example.org/api/packages/<username>/pypi \
       -u <username> \
       -p <password> \
       dist/something-0.1.0-py3-none-any.whl
```


