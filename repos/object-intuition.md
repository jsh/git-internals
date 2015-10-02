### What's in a Name?

*What’s in a name? that which we call a rose*

*By any other name would smell as sweet;*

-- William Shakespeare

If you're as lazy as I am,
you'll want to write a script to do the routine work
to create a scratch repo.

If you're lazier, you can use the one I wrote, in ../git-scratch.
If you followed the checklist you got before class, the code should already be installed,
as ```/usr/local/bin/git-scratch```.

Try it:

```bash
cd
PATH+=:/usr/local/bin
git-scratch
cd scratch
tree -a scratch
ls -a
```

Instead of an empty ```README``` file, I use an empty ```.gitkeep``` file,
so no one will be tempted to read it.
Still, the blob is the familiar ```e69de``` blob of the empty file.

Add a dozen files.

```bash
for i in {0..11}; do echo file $i > $i; done # make every file different
tree .git/objects
```

And half a dozen new blobs. But how do they get their names?

Start simply:

```bash
cd; git scratch # start again
```

You can invoke ```git-scratch``` without the hyphen,
which makes it possible to ```cd``` into "it."

```bash
cd $_; tree .git # every call wipes out the old scratch/
```

Make and add a new file

```bash
echo 'echo hello, world' > hello
chmod +x hello; ./hello # the canonical program
```

Look to see what its name will be, with git hash-object:

```bash
git hash-object hello
git add hello
tree .git
```

Here's how git hash-object works:

- It tacks together the object type, a blank, the size, a NUL byte, and the file.
- It hashes the result with the **sha1(1)** command.

Watch:

```bash
printf 'blob 18\000echo hello, world\n' | sha1sum
git hash-object hello
```

That name is a 40-digit, hex number.
There are lots of objects in most ```git/``` repos,
so **git** carves off the first two characters of the name
for a directory: 16^2 = 256 directories under ```.git/objects/```
so each directory can have fewer objects.

The objects? ```git add``` takes these three items -- type, size, and contents --
tacked together as shown above, calculates the hash, uses zlib to compress the triple,
then stores the compressed object under in the place named by the SHA1.

```git cat-file``` looks inside the compressed object, extracts the type, size, or contents,
(-t, -s, or -p), and displays them for you.

You could do this by hand

```bash
perl -MCompress::Zlib -e 'undef $/; print uncompress(<>)' .git/objects/e6/9de*
```

but ```git cat-file``` is ever-so-much more convenient.

A trio of exercises to hammer this home:

1. Try what you've seen: make files, add them,
and convince yourself you know why the resulting objects have the names they do.
1. Make objects that don't correspond to their names:
move them to different names, or change their contents.
Try some **git** commands with the mangled repos
to see what **git** does.








```



