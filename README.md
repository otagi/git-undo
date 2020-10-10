# How to undo git commits

There are several ways, for example:

1. `git revert`
2. `git reset`
3. `git rebase --interactive`
4. Bug 1, oops!

## 1. `git revert`

https://git-scm.com/docs/git-revert

> Given one or more existing commits, revert the changes that the related patches introduce, and record some new commits that record them. This requires your working tree to be clean (no modifications from the HEAD commit).

```shell
# Revert HEAD (the last commit)
git revert HEAD
```

## 2. `git reset`

https://git-scm.com/docs/git-reset

> Reset current HEAD to the specified state.

```shell
# Reset history to 1 commit before HEAD, and keep the changes.
git reset HEAD~1

# Reset history to 1 commit before HEAD, and delete the changes.
git reset --hard HEAD~1
```

## 3. `git rebase --interactive`

https://git-scm.com/docs/git-rebase

> Make a list of the commits which are about to be rebased. Let the user edit that list before rebasing. This mode can also be used to split commits.

Standard rebase, but with the possibility to drop some commits.

```shell
git rebase master --interactive
```

Your editor opens with this text file:

```ini
pick 8eaee66 Add git-revert section
pick c939a9c Add git-reset section
pick 0bca4bd Add git-rebase section

# Rebase 0d0e164..0bca4bd onto 0d0e164 (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

If you want to drop commit `c939a9c`:

```ini
pick 8eaee66 Add git-revert section
drop c939a9c Add git-reset section
pick 0bca4bd Add git-rebase section
```

Save the file, and close it. The `git rebase` will continue on the CLI.
