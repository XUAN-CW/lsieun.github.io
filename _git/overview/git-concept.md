---
title: "git concept"
sequence: "101"
---

[UP](/git.html)


## Two primary data structures

Within a repository, Git maintains two primary data structures, **the object store** and **the index**.
All of this repository data is stored at the root of your working directory in a hidden subdirectory named `.git`.

```text
                                                                            ┌─── lightweight
                                                             ┌─── tag ──────┤
                                                             │              └─── annotated
                                                             │
                                         ┌─── Git Objects ───┼─── commit
                                         │                   │
                                         │                   ├─── tree
               ┌─── Repository (.git) ───┤                   │
               │                         │                   └─── blob
Git Concept ───┤                         │
               │                         └─── Index Area ────┼─── git ls-files -s
               │
               └─── Working Directory
```

**The object store** is designed to be efficiently copied during a clone operation
as part of the mechanism that supports a fully distributed VCS.
**The index** is transitory information, is private to a repository, and can be created or modified on demand as needed.

### Git Object Types

At the heart of Git's repository implementation is the **object store**.
It contains your original data files and all the log messages, author information, dates,
and other information required to rebuild any version or branch of the project.

**Git places only four types of objects in the object store: the blobs, trees, commits, and tags**.
These four atomic objects form the foundation of Git's higher level data structures.

**Blobs**: Each version of a file is represented as a blob.
Blob, a contraction of "binary large object," is a term
that's commonly used in computing to refer to some variable or file
that can contain any data and whose internal structure is ignored by the program.
A blob is treated as being opaque.
A blob holds a file's data but does not contain any metadata about the file or even its name.

**Trees**: A tree object represents one level of directory information.
It records blob identifiers, path names, and a bit of metadata for all the files in one directory.
It can also recursively reference other (sub)tree objects and thus build a complete hierarchy of files and subdirectories.

**Commits**: A commit object holds metadata for each change introduced into the repository,
including the author, committer, commit date, and log message.
Each commit points to a tree object that captures, in one complete snapshot,
the state of the repository at the time the commit was performed.
The initial commit, or root commit, has no parent.
Most commits have one commit parent, although later we explain how a commit can reference more than one parent.

**Tags**: A tag object assigns an arbitrary yet presumably human readable name to a specific object, usually a commit.
Although `9da581d910c9c4ac93557ca4859e767f5caf5169` refers to an exact and well-defined commit,
a more familiar tag name like `Ver-1.0-Alpha` might make more sense!

Over time, all the information in the object store changes and grows,
tracking and modeling your project edits, additions, and deletions.
To use disk space and network bandwidth efficiently,
Git compresses and stores the objects in **pack files**, which are also placed in the object store.

### Index

**The index** is a temporary and dynamic binary file that describes **the directory structure of the entire repository**.
More specifically, the index captures a version of the project's overall structure at some moment in time.
The project's state could be represented by a commit and a tree from any point in the project's history,
or it could be a future state toward which you are actively developing.

One of the key, distinguishing features of Git is that
it enables you to alter the contents of the index in methodical, well-defined steps.
**The index** allows a separation between incremental development steps and the committal of those changes.

Here's how it works. As the developer, you execute Git commands to stage changes in the index.
Changes usually add, delete, or edit some file or set of files.
The index records and retains those changes, keeping them safe until you are ready to commit them.
You can also remove or replace changes in the index.
Thus, the index allows a gradual transition, usually guided by you,
from one complex repository state to another, presumably better state.

The index plays an important role in **merges**,
allowing multiple versions of the same file to be managed, inspected, and manipulated simultaneously.

### Content-Addressable Names

The Git object store is organized and implemented as a content-addressable storage system.
Specifically, each object in the object store has a unique name produced
by applying SHA1 to the contents of the object, yielding an SHA1 hash value.
Because the complete contents of an object contribute to the hash value and
the hash value is believed to be effectively unique to that particular content,
the SHA1 hash is a sufficient index or name for that object in the object database.
Any tiny change to a file causes the SHA1 hash to change, causing the new version of the file to be indexed separately.

SHA1 values are 160-bit values that are usually represented as a 40-digit hexadecimal number,
such as `9da581d910c9c4ac93557ca4859e767f5caf5169`.
Sometimes, during display, SHA1 values are abbreviated to a smaller, unique prefix.
Git users speak of **SHA1**, **hash code**, and sometimes **object ID** interchangeably.

An important characteristic of the SHA1 hash computation is that it always computes the same ID for identical content,
regardless of where that content is.
In other words, the same file content in different directories and even on different machines
yields the exact same SHA1 hash ID.
Thus, the SHA1 hash ID of a file is an effective globally unique identifier.

A powerful corollary is that files or blobs of arbitrary size can be compared for equality across the Internet
by merely comparing their SHA1 identifiers.

> corollary 必然的结果（或结论）a situation, an argument or a fact that is the natural and direct result of another one

### Git Tracks Content

It's important to see Git as something more than a VCS: **Git is a content tracking system**.
This distinction, however subtle, guides much of the design of Git and is perhaps the key reason
it can perform internal data manipulations with relative ease.
Yet, this is also perhaps one of the most difficult concepts for new users of Git to grasp,
so some exposition is worthwhile.

**Git's content tracking** is manifested in two critical ways
that differ fundamentally from almost all other revision control systems.

**First, Git's object store is based on the hashed computation of the contents of its objects**,
not on the file or directory names from the user's original file layout.
Thus, when Git places a file into the object store,
it does so based on the hash of the data and not on the name of the file.
In fact, Git does not track file or directory names, which are associated with files in secondary ways.
Again, Git tracks content instead of files.

If two separate files have exactly the same content, whether in the same or different directories,
Git stores a single copy of that content as a blob within the object store.
Git computes the hash code of each file according solely to its content,
determines that the files have the same SHA1 values and thus the same content,
and places the blob object in the object store indexed by that SHA1 value.
Both files in the project, regardless of where they are located in the user's directory structure,
use that same object for content.

If one of those files changes, Git computes a new SHA1 for it,
determines that it is now a different blob object, and adds the new blob to the object store.
The original blob remains in the object store for the unchanged file to use.

**Second, Git's internal database efficiently stores every version of every file**
— not their differences — as files go from one revision to the next.
Because Git uses the hash of a file's complete content as the name for that file,
it must operate on each complete copy of the file.
It cannot base its work or its object store entries on only part of the file's content
nor on the differences between two revisions of that file.

The typical user view of a file
— that it has revisions and appears to progress from one revision to another revision
— is simply an artifact.
Git computes this history as a set of changes between different blobs with varying hashes,
rather than storing a file name and set of differences directly.
It may seem odd, but this feature allows Git to perform certain tasks with ease.

### Pathname Versus Content

Git's physical data layout isn't modeled after the user's file directory structure.
Instead, it has a completely different structure that can, nonetheless, reproduce the user's original layout.
Git's internal structure is a more efficient data structure for its own internal operations and storage considerations.

When Git needs to create a working directory, it says to the filesystem:
"Hey! I have this big blob of data that is supposed to be placed at pathname path/to/directory/file. Does that make sense to you?"
The filesystem is responsible for saying
"Ah, yes, I recognize that string as a set of subdirectory names, and I know where to place your blob of data! Thanks!"

### Pack Files

An astute reader may have formed a lingering question about Git's data model and its storage of individual files:
Isn't it incredibly inefficient to store the complete content of every version of every file directly?
Even if it is compressed, isn't it inefficient to have the complete content of different versions of the same file?
What if you only add, say, one line to a file, doesn't Git store the complete content of both versions?

Luckily, the answer is "No, not really!"

Instead, Git uses a more efficient storage mechanism called a **pack file**.
To create a packed file, Git first locates files whose content is very similar and
stores the complete content for one of them.
It then computes the differences, or deltas, between similar files and stores just the differences.
For example, if you were to just change or add one line to a file,
Git might store the complete, newer version and then take note of the one line change as a delta and store that in the pack too.

Storing a complete version of a file and the deltas needed to construct other versions of similar files is not a new trick.
It is essentially the same mechanism that other VCSs such as RCS have used for decades.

Git does the file packing very cleverly, though.
Since Git is driven by content it doesn't really care if the deltas it computes
between two files actually pertain to two versions of the same file or not.
That is, Git can take any two files from anywhere within the repository and compute deltas between them
if it thinks they might be similar enough to yield good data compression.
Thus, Git has a fairly elaborate algorithm to locate and
match up potential delta candidates globally within a repository.
Furthermore, Git is able to construct a series of deltas from one version of a file to a second, to a third, etc.

Git also maintains the knowledge of the original blob SHA1 for each complete file
(either the complete content or as a reconstruction after deltas are applied) within the packed representation.
This provides the basis for an index mechanism to locate objects within a pack.

Packed files are stored in the object store alongside the other objects.
They are also used for efficient data transfer of repositories across a network.

## workflow

The typical workflow is that you'll change the contents of files in a repository, review the **diffs**,
add them to the **index**,
create a new **commit** from the contents of the **index**,
and repeat this cycle.

{:refdef: style="text-align: center;"}
![typical workflow](/assets/images/git/git-typical-workflow.png)
{:refdef}

## index staging area

Git doesn't add anything to the index without your instruction.
As a result, the first thing you have to do with a file you want to include in a Git repository is request that
Git add it to the index.

When a file is added to the index, a file named `.git/index` is created
(if it doesn't already exist). The added file contents and metadata are then added to the index file.

You've requested two things of Git here:

- Git should track the contents of the file as it changes (this isn't done without an explicit `git add`).
- The contents of the file when `git add` was run should be added to the **index**, ready to create the next commit.

## commit

Creating a **commit** stores the changes to one or more files.

Each commit contains
- a message entered by the author,
- details of the commit author,
- a unique commit reference (in Git, **SHA-1 hashes** such as `86bb0d659a39c98808439fadb8dbd594bec0004d`)
- a pointer to the preceding commit (known as the **parent commit**),
- the date the commit was created, and
- a pointer to the contents of files when the commit was made.

The file contents are typically displayed as the **diff**
(the differences between the files before and the files after the commit).

{:refdef: style="text-align: center;"}
![](/assets/images/git/commit-parts.png)
{:refdef}

## Object store

Git is a version control system built on top of an **object store**.
Git creates and stores a collection of objects when you commit.
The **object store** is stored inside the **Git repository**. 

the main Git objects we're concerned with: **commits**, **blobs**, and **trees**.
There's also a **tag** object, but don't worry about tags until they're introduced.
Figure 1.2 showed an example of a commit object and how it stores metadata and referenced file contents.
The file-contents reference is actually a reference to **a tree object**.
**A tree object** stores a reference to all the **blob objects** at a particular point in time
and **other tree objects** if there are any subdirectories.
**A blob object** stores the contents of a particular version of a particular single file in the Git repository.

{:refdef: style="text-align: center;"}
![](/assets/images/git/commit-blob-tree-objects.png)
{:refdef}

## Refs

In Git, `refs` are the possible ways of addressing individual commits.
They're an easier way to refer to a specific **commit** or **branch** when specifying an argument to a Git command.

### branch name

**The first ref** you've already seen is a branch
(which is `master` or `main` by default if you haven't created any other branches).
**Branches are pointers to specific commits**.
Referencing the branch name `master` is the same as referencing the SHA-1 of the commit at the top of the `master` branch,
such as the short SHA-1 `6b437c7` in the last example.
Whenever you might type `6b437c7` in a command, you can instead type `master`, and vice versa.
**Using branch names is quicker and easier** to remember for referencing commits than always using SHA-1s.

**Refs can also have modifiers appended**.
Suffixing a ref with `~1` is the same as saying “one commit before that ref.”
For example, `master~1` is the penultimate commit on the master branch: the short SHA-1 `6576b68` in the last example.
Another equivalent syntax is `master^`, which is the same as `master~1` (and `master^^` is equivalent to `master~2`).

### HEAD

**The second ref** is the string `HEAD`.
`HEAD` always points to the top of whatever you currently have checked out,
so it's almost always **the top commit** of **the current branch** you're on.
If you have the `master` branch checked out, then `master` and `HEAD` (and `6b437c7`) are equivalent.
See the `master/HEAD` pointers demonstrated in the following figure.



{:refdef: style="text-align: center;"}
![](/assets/images/git/refs-master-head.png)
{:refdef}

These `git diff` invocations are all equivalent:

- `git diff master~1 master`
- `git diff master~1..master`
- `git diff master~1..`
- `git diff master^ master`
- `git diff master~1 HEAD`
- `git diff 6576b68 6b437c7`

### rev-parse

You can also use the tool `git rev-parse` if you want to see what SHA-1 a given ref expands to.

```text
$ git rev-parse master
030e4624ad709a606374d827961187a6146b03a6

$ git rev-parse HEAD
030e4624ad709a606374d827961187a6146b03a6

$ git rev-parse 030e46
030e4624ad709a606374d827961187a6146b03a6
```
