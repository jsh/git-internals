### Tags and Branches Are Both Commit-ishes

You've tagged all three, basic object types. 
All you'll ever see tagged in practice is commits.

Commit names are so important that there's a name for them: *commit-ish*,
and any tag you ever see, from now on, will be a commit-ish, just like "initial".

Time to introduce a pair of new tools: `git addfile` and `git lol`.
Neither is a standard part of git;
you installed them while going through your checklist for the workshop.

`git addfile` does the boring job of creating, adding, and committing a file.

```bash
cd; git scratch; cd $_
git addfile half-round
git addfile venona
git addfile X
for i in {1..5}; do
  git addfile $i
done
ls
cat venona
```

`git lol` shows you your commits and tags.
Mac laptops have Aqua-ized `gitX`. Linux laptops have the Gnome-based, `gitg`.
Almost any laptop has `gitk`, but I always think the Tcl/Tk GUIs look like MS-Windows from the 1990s.
Headless servers, which lack GUIs? `git lol` works on anything with a console.

```bash
git lol
git tag alog
git addfile
git tag guten
git tag -l # list the tags
git lol
```

Sweet, no?

So what's a branch?
As luck would have it, `git scratch` will take a `-b` flag that makes branches.

```bash
cd; git scratch -b; cd -
git branch -l # list the branches
git lol
tree .git/refs
tee .git/refs/heads/*
```

A branch is just another commit-ish, but branches are stored under `.git/refs/heads`
instead of `.git/refs/tags`.

They're both, effectively, little yellow stickies pasted on commit objects to name them.

```bash
git rev-parse master
git rev-parse davidian
git checkout davidian
ls; git show
git checkout master
ls; git show
```

How cheap is making a branch? Deleting a branch? Just like tags: it's instant and it's (almost) free.
It's a one-line file. No network traffic. No effect on anyone else. No nothing.

```bash
git branch water
git branch -l
git checkout water
git addfile bourbon
git addfile rocks
git lol
git checkout master
```

So, why two? [How are branches different from tags?](https://github.com/jsh/git-internals/blob/new-course/commitishes/tag-v-branch.md)
