### On the Surface

First, define a little, reporting function
to list the contents of the current directory
and run ```git status```.

```bash
function state() { echo; ls -l; printf '\n===\n\n'; git status; }
```
It will save you some typing.

Next, use it to watch what's happening,
as you create a little, scratch project
and put it under **git**.

```bash
mkdir /tmp/scratch
cd $_
state
git init
state
> README
state
git add hello
state
git commit
state
```

*Something* is changing. How does **git** know?
