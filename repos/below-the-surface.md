### How Do it Know?

Let's start afresh, but watch more carefully.


```bash
rm -rf /tmp/scratch; mkdir /tmp/scratch
cd $_
ls -al
git init
ls -al
```

Aha! ```git init``` created a **.git/** directory.
What's in it?

```bash
tree .git
```

Quite a bit. Let's modify our reporting function to watch it.

```bash
function state() { echo; tree .git; printf '\n===\n\n'; git status; }
```

```bash
> README
state
```

No obvious change.
**git** simply sees that there's a ```README``` file
that it doesn't know anything else about.

Let's continue to follow **git**'s advice.

```bash
git add README
state
```

Aha! Now there are changes.
And **git** *does* know something about the file.
Keep your eye on that file under ```objects/e6/```.

What's left? The commit.

```bash
git commit -m'initial'
state
```

We've added two more objects.

Are all the things **git** knows about under ```.git/```?
Let's find out.

```bash
git show
rm -rf .git
state
git show
```

We're back to where we started.
````.git/```` is, in fact, your entire git repository.
It's all there is.
It's where **git** stores everything it knows about.
Understand what's in it and you understand **git**.

And what were the three objects?
We'll see momentarily,
but first, try doing this yourself:

make a ```state()``` reporting function,
create a ```/tmp/scratch``` directory,
initialize the repo with ```.git init```,
add an empty ```README``` file (name in all caps),
add it, and commit it,
watching each step with your ```state``` function.

Don't just watch and nod.

Now you see what each step's doing,
and what each message is telling you.

This is going to be our approach:

- make disposable, scratch, toy repos

- do tiny experiment-lets in them

- watch carefully what changes at each step

What will you get from it?

- an ability to hear what **git** is telling you

- a deep understanding of **git**'s design

- a way that works to understand the things we don't cover

Let's start to that to understand what's that ```.git/``` repo contains by
[looking at that simple repo again.](https://github.com/jsh/git-internals/blob/new-course/repos/the-empty-file.md)
