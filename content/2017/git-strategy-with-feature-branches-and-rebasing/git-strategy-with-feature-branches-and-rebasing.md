---
title: Git Strategy with Feature Branches and Rebasing
date: 2017-02-21
redirect_from: /git-strategy-with-feature-branches-and-rebasing/
---
My personal favorite Git strategy is this: (there are many ways to do it)

Every feature starts from **master branch**
-------------------------------------------

```
git checkout master
git pull
git checkout -b feature/name-of-the-feature
```

Code!

After coding or during coding
-----------------------------

Commit all the changes in your branch and push the branch to remote.

You can commit all changes at once:

```
git add --all
git commit -m "Commit message"
```

Or you can specify the commits with more detail

```
git add name-of-the-file
git commit -m "Commit message"
```

Once you are done commiting and you have no changes or untracked files left, push your branch to remote.

```
git push origin feature/name-of-your-feature
```

Rebasing your branch
--------------------

Rebasing is a way to bring changes from the master branch which have been inserted there after you started your own feature branch.

In rebasing you pull the changes from the master (you can specify some other target too) and start adding your feature branch’s commits on top of it.

If there are a lot of changes in the master, especially things that are affecting your work, then I suggest you do a rebase everyday.

If there are no changes that affect your work, then there is no need to do it as often. But keep in mind that if you branch starts to fall a lot behind master it may become very difficult to do the rebase, because there might be so many conflicts.

**This is my routine** for rebasing when I’m developing and have made all the commits on my feature branch:

```
git checkout master
git pull
git checkout feature/name-of-the-feature
git rebase master (you can add -i to modify/rename the commits if you want)
```

Rebase and fix conflicts and once finished:

```
git push origin your-branch -f
```

Now you have succesfully rebased your branch and it’s in sync with master.

Multiple developers and rebasing
--------------------------------

If you have multiple developers working on the same branch then you have to communicate the rebasing so that all developers get the force pushed version to their machine. They can’t just pull the branch since its history has changed and doesn’t match anymore to their own branch.

You can also postpone the rebasing to a state where only one developer is working with the branch

### Multiple developer rebasing strategy

The problem with multiple developers working on the same branch can be solved by having one base branch and sub branches made from that base branch for each developer who works on the feature.

*   master
    *   base branch
        *   each developers own branch

Now actually no one is working directly on the base branch.

Own branches are merged with or without pull request to the base branch and once everything is done the base branch is merged into master. This is also good way to separate tasks to little branches and make the workflow better.

When we want to get the latest changes from master, some developer will checkout the base branch and do the rebase on master.

The sub branches are then rebased to the base branch.