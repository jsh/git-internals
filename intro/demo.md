### A Simple Git Demo

Let's start with a simple demo. Begin by cloning a repository from GitHub.
Just for grins, check out the source code for **`git`** itself.

```bash
time git clone https://github.com/git/git.git
cd git
du -sh .
ls
```

It's about 100 megabytes, with over 2500 files,
so a reasonable-sized project.
The clone it takes under half a minute.
That seems fast enough.

But unlike earlier, Centralized Version Control Systems (CVCSs),
we didn't check out a version of the code, we cloned the entire repository.

To emphasize that, let's first turn off networking,
so we no longer have access to GitHub, where we cloned from.

```bash
sudo ifconfig en0 down # on a mac
ping -n github.com # no DNS
ping -n 4.2.2.2  # okay, it's down
```
Now let's try a few things. What's the history look like?

```bash
git log
git log | tail
```

That last one is the first version of git. Ever.
We can tag it.

```bash
git tag initial e83c5163316f89bfbde7d9ab23ca2e25604af290
git checkout initial
ls
```

Eleven files.

**`git`** was created by Linus Torvalds
to maintain the Linux kernel,
so the earliest version is quite easy to build
even a decade later, on modern Linuxes.

Here's what you need to change for Ubuntu 14.04

```bash
echo 'LIBS=-lcrypto -lz' >> Makefile
sudo apt-get install libssl-dev # in case it's not there
make
```

And, since it builds with that change, make a branch
and commit the change on that branch

```bash
git checkout -b devonian initial
git status
git commit -am'Port to Ubuntu 14.04'
```

All this is local.
You can checkout, paw through history, branch, tag, commit,
and anything else you'd want to do
with a version-control system,
all on an airplane, in a coffee shop,
or in your home while still in your pajamas.

#### *Note: For a short talk, the intro can probably stop here.*

We can look for a version a week later and tag it.

```bash
git rev-list master -n 1 $(git rev-parse --before=2005-04-14)
git tag week-1 $(git rev-list master -n 1 $(git rev-parse --before=2005-04-14))
git rev-list --count week-1 # about 10 commits a day
```

He's doing about 10 commits a day.
Over a decade later, that's still about the rate.

Merges? If we can do branches, we can do merges.
For fun, let's look at the very first merge commit.

```bash
git show $(git rev-list --merges master | tail -1)
git log --oneline --graph --decorate $(git rev-list --merges master | tail -1)
```

All this completely disconnected from the net. Fast. Local.
