---
title: How to reset GIT commits of a branch
date: 2016-08-25
redirect_from: /how-to-reset-git-commits-of-a-branch/
---
I assume that you are in branch and you’d like to forget about your commits.

If you want to reset the whole branch and make it look like its master, and lose all the changes use this command:

```
git reset --hard master
```

If you want to reset the previous commit but not lose the changes use this:

```
git reset HEAD^
```

If you want to continue working but have the changes included in the same commit then you can use this:

```
git commit --amend
```