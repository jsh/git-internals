### Nothing

Let's make another scratch repo, right up through the ```git add```
```bash
cd /tmp
rm -rf scratch
git init scratch
cd $_
touch README
git add .
git commit -m'initial'
tree .git/objects
```

(The command ```git init <directoryname>``` is a shorthand
that both makes the directory and does the ```git init``` inside it)

Wait.
You have a computer.
Space is cheap.
Be generous!
Make half a dozen scratch repos.

```bash
cd
for i in {1..6}; do
  git init scratch.$i
  pushd scratch.$i
  cp /dev/null $LOGNAME
  git add $LOGNAME
  popd
done
ls -l scratch.$i/$LOGNAME
```

Empty files, every one.
What's in the objects directory for all of them?

```bash
for i in {1..6}; do
  tree $LOGNAME.$i/.git/objects
done
```

They all have the same thing. That must be git's "empty file."

```bash
cmp {/tmp/scratch/,*.1}/.git/objects/e6/9*
```

They're the same as the ```e6/9de29...91``` under ```/tmp/scratch```,
which was made out of a file called ```README``` instead of your login name,
so it must not contain the filename.

You're working on a different machine, in a different home directory, at a different time, and have a different login name.
You've made empty files three different ways (```> filename```, ```touch filename```, and ```cp /dev/null filename```),
but you got ```e6/9de29``` every time, just like I did. That object must just *be* an empty file:
no history of how it was created, no machine name, no username, no filesystem location, no datestamp, no extra stuff, no nothin'. Right?

```bash
cat /tmp/scratch/.git/objects/e6/9*
```

Wrong. Oh well.

(If you have a more modern shell,
you can use its **globstar** option
to save yourself some typing.

```bash
shopt -s globstar # set the globstar option
cat /tmp/scratch/**/9* # or maybe even cat /tmp/**/9*
```

)

It looks like garbage because it *does* add a couple of pieces of metadata, the filesize and the object type (which we'll get to in a minute), and it's zlib-compressed.

To show the contents, **git** gives us a tool: **git**'s Swiss-army knife, ```git cat-file```.

```bash
cd /tmp/scratch
git cat-file -s e69de29 # show the object's size
git cat-file -t e69de29 # show the object's type
git cat-file -p e69de29 # pretty-print the object's contents
```

Pause here, add a couple of non-empty files to one of your scratch repos, and use ```git cat-file``` to look at the objects you added.

And what happens if you try to add a few more *empty* files, by other names?

Notice that though the object is in ```.git/objects/e6/9de29...91```,
**git** is letting us name the object with the directory name, ```e6```, stuck on to the first few characters of the filename, ```9de```.

By the time you're done, I predict you'll recognize ```e69de``` as "the empty file."

For now, though, let's move on to do a commit, and use ```git cat-file``` and
[look at those other two objects.](https://github.com/jsh/git-internals/blob/new-course/repos/two-new-object-types.md)
