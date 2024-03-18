---
title: ".gitignore"
---

[UP](/git.html)


## Ignoring files: .gitignore

```text
git add .gitignore
```

You wish to ignore all files with the extension `.tmp` in a Git repository.

```text
*.tmp
```

忽略所有以 `.` 开头的文件，但是 `.gitignore` 例外：

```text
.*
!.gitignore
target/
```

Each line of a `.gitignore` file matches files with a pattern.
For example, you can add comments by starting a line with a `#` character or negate patterns by starting a line with a `!` character.
Read more about the pattern syntax in `git help gitignore`.

A good and widely held principle for version control systems is to avoid committing output files to a version control repository.
Output files are those that are created from input files that are stored in the version control repository.

GitHub also provides a useful collection of gitignore files at [https://github.com/github/gitignore](https://github.com/github/gitignore).

## Deleting ignored files

When files have been successfully ignored by the addition of a `.gitignore` file,
you'll sometimes want to delete them all.
For example, you may have a project in a Git repository
that compiles input files (such as `.c` files) into output files (in this example, `.o` files)
and wish to remove all these output files from the working directory to perform a new build from scratch.

You wish to delete all ignored files from a Git working directory:

```text
git clean --force -X
```

The `-X` argument specifies that `git clean` should remove only **ignored files** from the working directory.
If you wish to remove **ignored files** and all the **untracked files** (as `git clean --force` would do),
you can instead use `git clean -x` (note that the `-x` is lowercase rather than uppercase).

The specified arguments can be combined with the others.
For example, `git clean -xdf` removes all untracked or ignored files (`-x`) and directories (`-d`) from a working directory.
This removes all files and directories for a Git repository that weren't previously committed.
Take care when running this; there will be no prompt, and all the files will be quickly deleted.

Often `git clean -xdf` is run after `git reset --hard`;
this means you'll have to reset all files to their last-committed state and remove all uncommitted files.
This gets you a clean working directory: no added files or changes to any of those files.

此处，我想到文件的三种状态：

- tracked file: `git reset --hard`
- untracked file
- ignored file
