# How to undo git commits

There are several ways, for example:

1. `git revert`
2. `git reset`
3. `git rebase -i`

## 1. `git revert`

https://git-scm.com/docs/git-revert

> Given one or more existing commits, revert the changes that the related patches introduce, and record some new commits that record them. This requires your working tree to be clean (no modifications from the HEAD commit).

```shell
# Revert HEAD (the last commit)
git revert HEAD
```
