### Togetherness

The most important thing about **git** is that it's simple.

The *next* most important thing? It's local.

Your repo is all yours. Your branches, your tags? Yours.
Other stuff we haven't even talked about,
but that you'll discover when you explore more?
Yours.

The "canonical" version of the repo? Doesn't exist.

Projects with more than one contributor? You need a way to share.
With a Centralized Version Control System (CVCS),
like Subversion or CVS,
you checkout a version of code from "the repository."

With a Distributed VCS (DVCS), each developer's clone of a repo is independent.
Any pair can be synchronized on request,
but getting 10 developers in synch requires 10*9 pairwise synchs.

A common way to cut this down is to agree, by convention, on a sync point,
such as "the clone up on GitHub."

This transforms a O(N^2) problem to a O(N) problem,
but keep in mind that GitHub isn't a "master" in the CVCS sense,
it's only a sync point.

Time to make a "central" repo,
so you can see how GitHub (or GitLab, or Gerrit, or ...) works.

```bash
git scratch
git clone --bare scratch
ls sc*
tree scratch.git
```

Synch points are "bare" repos, which means that they only have the objects,
not a working tree: they look like the .git directory,
which is why they're named *`reponame`*`.git`

Sidebar: Do `diff -r scratch/.git scratch.git`. Why are there differences?

You can pretend the "remote" is somewhere else on the web by putting it in `/tmp`,
and then cloning from it with `git clone ssh://localhost/tmp/scratch.git` .

By an amazing coincidence, `git scratch -r` does just that.

```bash
git scratch -r
tree /tmp/$LOGNAME/scratch.git
```

(It's in `/tmp/$LOGNAME/` in case you're on a shared server.)

Check to make sure the clone is what you'd expect.

```bash
tree -a scratch.clone
```

Oops. What are `.git/objects/pack/` and `.git/packed-refs`.
And the `.gitkeep` file is still there, but what happened to the objects?
Or to ``.git/refs/tags/initial`?

They're still there, and **git**'s commands can still see them.

```bash
cd scratch.clone
cat .git/packed-refs
git verify-pack -v .git/objects/pack/*.pack
git rev-parse master
git cat-file -t e69de
git checkout initial
```

It's just a performance hack.
If you have 1000 objects and 100 tags and branches in the synch point,
`git clone` packs up the objects into a single file, and the refs into a second,
so it can do 2 file transfers instead of 1100.

It also compresses the result, to speed transfer even more,
and you can see the packfile name contains a SHA1.

If you'd done this yesterday, you wouldn't have known where to start.

```bash
git clone https://github.com/jsh/git-internals.git
cd git-internals
tree .git
```

Now, you can see a lot of what's going on.

We could do many experiments to learn more,
but I'll leave that to you and move on to a final topic: [git commands, and how to add your own.](https://github.com/jsh/git-internals/blob/new-course/other-stuff/extending.md)
