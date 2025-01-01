# Cheatsheet

- Un-stage staged file

```sh
git restore --stage <file_name>
```

- Get git log diff of two branches

```sh
git log main..release/2.0 --oneline
```

- Merge latest version from remote branch (when local branch is not up to date)
You can just fetch the remote branch and directly update the current branch
from the remote branch instead of updating the local branch from the remote
and merge the local branch

```sh
git fetch origin develop
git checkout release/1.0
git merge origin/develop
```
