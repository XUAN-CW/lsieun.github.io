---
title: "git HEAD"
sequence: "105"
---

[UP](/git.html)

HEAD answers the question: **Where am I right now in the repository?**
It is a pointer to the currently checked-out branch or commit,
which in turn contains an immutable snapshot of your entire code base at a given time.

```text
HEAD 可以指向 branch，也可以指向 commit
另外，branch 本身也是指向 commit
```

## What is "HEAD" in Git?

When working with Git, only one branch can be checked out at a time - and this is what's called the **"HEAD" branch**.
Often, this is also referred to as the "active" or "current" branch.

```text
笔记：HEAD 是表示当前分支
```

Git makes note of this current branch in a file located inside the Git repository, in `.git/HEAD`.
(This is an internal file, so it should not be manually manipulated!)

```text
笔记：HEAD 这个抽象概念，具体表现形式是一个 .git/HEAD 文件
```

```text
$ cat .git/HEAD
ref: refs/heads/master
```

```text
$ git branch
* dev
  main

$ cat .git/HEAD
ref: refs/heads/dev

$ git checkout main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.

$ git branch
  dev
* main

$ cat .git/HEAD
ref: refs/heads/main
```

## Attached & detached state

First, it's essential to know that the `HEAD` pointer can be in either of two states: **attached** or **detached**.

The default state is **attached**,
where any manipulation of the history is automatically recorded to the branch `HEAD` is currently referencing.

In a **detached** state, experimental changes can be made without impacting any existing branch,
as `HEAD` is referencing the underlying commit directly and is not "attached" to a particular branch.

## Detached HEAD

In rare cases, the HEAD file does NOT contain a branch reference, but a SHA-1 value of a specific revision.
This happens when you checkout a specific commit, tag, or remote branch.
Your repository is then in a state called **Detached HEAD**.

要将 `HEAD` 指向某个 commit，可以使用以下命令：

```shell
git checkout <commit-id>
```

这个命令会将 `HEAD` 移动到指定的 `<commit-id>` 所表示的提交上，从而进入 detached HEAD 状态。在这种状态下，你可以查看特定提交的内容，进行测试或其他操作。

如果想要在 `HEAD` 指向某一 commit 后创建一个新分支，可以在命令中指定一个新分支名称：

```shell
git checkout -b <new-branch-name> <commit-id>
```

这将会创建一个新分支，并将 `HEAD` 指向指定的 commit，使得新分支从该 commit 开始。

## HEAD ref

- HEAD caret: `HEAD^`
- HEAD tilde: `HEAD~`

{:refdef: style="text-align: center;"}
![](/assets/images/git/head/git-head-relative-refs.jpg)
{:refdef}

- `HEAD`: The current reference point in a git log.
- `HEAD~`: shorthand for `HEAD~1`. It means reference HEAD's first parent.
- `HEAD~2`: means reference HEAD's grandparent, or first parent's parent.
- `HEAD~3`: means reference HEAD's great-grandparent, or first parent's parent's parent. So you see the pattern… 👍
- `HEAD^`: shorthand for `HEAD^1`. It means reference HEAD's first parent.
- `HEAD^2`: means reference HEAD's second parent. This scenario comes during merging of a branch.

Now we can combine `~` and `^` for scenarios
where a commit has more than one parent.
For example, `HEAD~2^2` gives us second grandparent of the `HEAD` reference commit.

Use case:

- `~` is used to go number of generation back and is generally linear in appearance.
- `^` is used on merge commits where a commit can have more than 1 parent.
  Hence, looks like forks in a road.

## @ 符号

在 Git `1.8.4` 版本之后，可以使用 `@` 符号代替 `HEAD`，这样书写起来会比较方便。

例如，下面两条批令是相同的效果：

```text
$ git show HEAD --oneline
$ git show @ --oneline
```


## Reference

- [What is HEAD in Git?](https://blog.git-init.com/what-is-head-in-git/)
- [How HEAD works in git](https://jvns.ca/blog/2024/03/08/how-head-works-in-git/)
