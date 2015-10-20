### Tag, You're It

Study this list for a few seconds, close your eyes and say back as many as you can:

[vegetable, sausage, present, burnout, morning, address, produce](http://4pics1word.ws/7-letter-words/)

Now, do the same with this list:

e83c516, 8bc9a0c, e497ea2, bf0c6e8, 19b2860, 24778e3, 2ade934

They're both lists of seven-character strings.
**`git`** loves hex constants. You? Not so much.

You need a better way to name these constants; **`git`** gives you lots of ways.

Start with the most straightforward: *tags*.

```bash
cd
git scratch
cd $_
git cat-file -t e69de29
git tag empty e69de29
git cat-file -t empty
git cat-file -p empty
git cat-file -s empty
git rev-parse empty
tree .git/refs
cat .git/refs/tags/empty
```

  I tag my first commits, "initial",
  so I can check out 0-day versions of my own repos
  without having to think about SHA1s.
  I tweaked `git-scratch` to remember to do that for me.

```bash
cat .git/refs/tags/initial
git show
```

(The "initial" in my comment isn't connected with the name of the tag.
I use the same word for each
because it's easier for me to remember one word than two.)

Tags are just one-line files in `.git/refs/tags/`.
Really. What could be simpler?
You can tag objects until the cows come home.

```bash
git tag bupkis e69de
git tag nothing bupkis
cp .git/refs/tags/nothing .git/refs/tags/nada
cat .git/refs/tags/nada
tree .git/refs/tags
git cat-file -t nada
```

They're just files. No magic. What could be simpler? Or faster?

Simple, fast.

Want to delete the tag? Delete the file.
`git tag -d`*`tagname`* does the trick, too.

Whenever a git command expects a SHA1,
it runs through a checklist:

- Did he give me a 40-digit hex number?
Look for an object by that name.
- Did he give me a smaller hex number?
Look for object with that number as the first few digits.
- Did he give me the name of a file in .git/refs/tags?
Read the file, use that SHA1.

it deletes the tag `.git/refs/tags/empty`,
instead of the object it points at.

True.

`git tag -d` doesn't expect a SHA1, it expects a tagname.

----
#### *A tag is a human-friendly name for a SHA1.*
#### *It's implemented as a one-line file.*
----

From tags, it's [an easy step to branches.](https://github.com/jsh/git-internals/blob/new-course/commitishes/on-to-branches.md)

Okay. Your turn.

Make a scratch repo, tag commits, trees, blobs, whatever.
Look at the tags, delete the tags, copy the tags, hand-craft tags. Do things that don't work and watch git whine.

Run free.

Whenever you get confused, or mess something up hopelessly,
just `cd; git scratch; cd -` and start afresh.
