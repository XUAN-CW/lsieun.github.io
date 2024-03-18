---
title: "git update-index"
---

[UP](/git.html)


```bash
$ git update-index --add --cacheinfo 100644 \
 3b18e512dba79e4c8300dd08aeb37f8e728b8dad hello.txt
```

In this case, you're specifying a mode of `100644`, which means it's a normal file.
Other options are `100755`, which means it's an executable file;
and `120000`, which specifies a symbolic link.
The mode is taken from normal UNIX modes but is much less flexible
— these three modes are the only ones that are valid for files (blobs) in Git
(although other modes are used for directories and submodules).
