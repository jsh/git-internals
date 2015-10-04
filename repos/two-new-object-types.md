### Blobs, Trees, and Commits

You've created a repository with `git init```
and added an empty file with `git add```.
Now what?

A commit, with `git commit```.

Clean up the array of scratch directories you've made
and start afresh.

```bash
cd && rm -rf $LOGNAME.*
git init scratch # make a project
cd $_ # go into it
touch README # make a file
git add $_ # add it
tree # this is looking familiar
```

Next, commit:

```bash
git commit -am'initial'
```

I like to use a stereotyped, initial commit message.
As with using common names, like, `README` and `LICENSE```,
putting a trash-can under the sink,
or doing laundry on Washday,
conventions offer familiarity and consistency.

Notice what **git**'s telling you:
there's a commit, and it has an identifier.

Look what's changed:
```bash
tree .git/objects
```

See the blob that corresponds to that identifier?
That identifier is your most recent commit,
or `HEAD```.

You don't have to memorize that identifier.
You can see it in lots of ways:
```bash
git show
git rev-parse HEAD
```

```HEAD` always names the most recent commit on your current branch --
whatever you're looking at right now.

What's in it?

```bash
git cat-file -t $(git rev-parse HEAD)
git cat-file -p $_ # what's it look like?
```

And there's the other object!

```bash
git cat-file -p 543b9
git cat-file -t $_
```

- "blob" is **git** for "file"
- "tree" is **git** for "directory"
- "commit" is **git** for ... uh ... "commit"

Time to make some more repositories and commits.
Please do it yourself a few times, with in a few different places and ways.

First, convince yourself that

- you're *completely* comfy with all the steps of creating a repo,
adding a file, making a commit,
and understanding what git's telling you along the way.
- you understand all the objects in a simple, scratch repo
with an empty `README` file.
- you can use `git cat-file` to look at objects
- it doesn't make you nervous to throw away repos

Next, add and commit more files, and use tools
you now have --
tree, git show, git cat-file, git rev-parse --
to confirm you really know what you're doing.

Last, here's a test. What's going on, under the hood,
at each step?

```bash
rm -rf scratch
git init scratch; cd $_
mkdir origami
touch origami/README
git add .
git commit -m'initial'
touch DO_NOT_README
git add .
git commit -m'truth in advertising'
```

Now that you're becoming an expert,
let's pause to [improve your intuition about objects.](https://github.com/jsh/git-internals/blob/new-course/repos/object-intuition.md)
