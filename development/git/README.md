# git

'What the fuck is git?', you may ask. To explain it simply, a git, shorted for nothing, is a stupid content tracker, that's what the creator, the God, himself said.

Let's stop being a git for a second. A git is actually a fucking big graph. (It's directed acyclic graph, nerds.)

There are a few terminologies should be known.

## Terminologies

### Blob

**Blob** is the actual data (a picture, video, file, etc.)

### Tree

**Tree** is a pointer (or are pointers) to blobs related to the commit. So, if one commit contains changes in many files, the tree will point to many blobs (1:M relationship).

### Commit

**Commit** is a metadata of a tree. It contains data such as author, commit message, and, of course, a pointer to a tree.

With these tree words being known, we can roughly draw a simple diagram like:

```text
[blob_a] (foo.txt)    --\
[blob_b] (bar.js)     --->--- [tree] --- [commit]
[blob_c] (foobar.svg) --/
```

Now, let's move on to even higher levels.

There are another set of vocabulary that we should know.

### Tag, Branch, Remote, HEAD

Ok, let's group them together. Why? Because they are just simply pointers to a commit. A branch is a pointer to a commit chain. So is remote, tag, and HEAD.

For tags and branches, they allow naming a commit and contain some additional meta information.

