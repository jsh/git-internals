### Branches: Like Tags, but Not

*Q: How are Dwight D. Eisenhower and Santa Claus alike?*
*A: They both have beards, except for Eisenhower.*

Encapsulate some routine operations with a function.

```bash
new-scratch() {
  cd
  git scratch $1 # for args
  cd scratch     # you know the drill
  git lol
}
```

Make a new, branched, scratch repo.

```bash
new-scratch -b
```

Now do some work

```bash
git checkout davidian
git rev-parse davidian
git addfile rockford
git rev-parse davidian
git addfile rankand
git rev-parse davidian
git lol
```

Every time you commit, the file `.git/refs/heads/davidian` changes. Try that with a tag.

```bash
git checkout initial
git rev-parse initial
git addfile gumbo
git rev-parse initial
git addfile VERY-IMPORTANT
git rev-parse initial
git lol
```

Tags don't move.
*What would you pay? But wait! There's less!*

```bash
git checkout master
git lol
```

All your work, gone.
The blobs for gumbo and VERY-IMPORTANT are even still in the object database, somewhere.
There's just no easy way to find them.

If you remember that last commit's SHA1, great.
You can use it to check the commit back out,
but you lack any easy-to-remember commit-ish for it.

Almost. Here's a cheap trick.

```bash
git checkout - # checkout the last commit you checked out, like 'cd -'
git lol
git branch almost-sawn-off
git checkout - # back to master
git lol # phew!
```

And now, you have a human-friendly name -- a commit-ish -- for that commit,
and all the commits that led up to it.

Let's look at it for a second.

```bash
git cat-file -p almost-sawn-off
git cat-file -p almost-sawn-off~ # the parent
git cat-file -p almost-sawn-off~2 # the grandparent
git rev-parse davidian~3
git lol
```

Notice:

- A commit object contains a pointer to its parent(s).
(Quick Quiz: How could a commit have more than one parent?)
- Strings like `master~2` are a new kind of commit-ish.
- When git tells you you're in a "detatched head state",
and even tells you what to do about it,
pay attention.
It's telling you that if you commit,
you're creating a commit that you won't be able to name.

Your Turn:

1. Make a scratch repo, make some commits to master, and tag the top-of-tree.
1. Next, check out the tag, and look at the message. Don't do any commits.
1. Finally, check out master again. Is there a message?

It's the same commit. One's headless, one's not. How does **git** know?

How can you figure out what's going on?
Do it.
