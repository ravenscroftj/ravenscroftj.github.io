---
tags:
  - software
---

## Moving Submodules
	- Simply running `git mv oldname newname` should work and do all the plumbing for you ([source](https://stackoverflow.com/questions/4604486/how-do-i-move-an-existing-git-submodule-within-a-git-repository))
	-

## Alternatives to submodules
- https://gitmodules.com/
- https://blog.plover.com/2022/06/29/#tips

## Storing Credentials
- The best practice is always to use SSH keys for authentication.
- In some environments (e.g. overleaf), use of SSH keys is not possible and HTTP auth is required
- Your credentials can be stored on disk but they are unencrypted and thus pose a security risk
- Enter the directory you wish to store creds for and run:
	- `git config credential.helper store`