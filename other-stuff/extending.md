### Extending

*
פרייהייט? דאס איז יאַנג דינען וואָרט.
*

Time to circle back to things you've seen earlier.

You know that your git repo is inside `.git/` .
Does git keep things anywhere else? You know that, too: Yes.

For example, the git command isn't inside your git repo.

```bash
type git
```

What else is outside `.git/`? Both "lots" and "almost nothing."

First, "lots"

```bash
locate git-core
ls /usr/lib/git-core # or wherever your distro installs it
ls /usr/lib/git-core | wc -l
```

This is where bash keeps its sub-commands.
When you type `git pull`, **git** sees the subcommand `git pull`,
slaps in a hyphen and looks for a command called `/usr/lib/git-core/git-pull`,
which it finds and executes.

Just as you can add a new command by putting it in `/usr/bin/`,
you can add a new git sub-command by putting it in `/usr/lib/git-core/`,
and naming it `git-`*`my-new-subcommand-name`*.

People do that all the time, which is why there are so many git subcommands.
People do that all the time with Linux, too,
which is why there are so many commands.

```bash
ls /bin /usr/bin | sort -u | wc -l
```

Want more? Add a package or two.

```bash
apt-get install pstree # or however you add packages
ls -l /usr/bin/pstree
```

Ditto for git

```bash
apt-get install git-flow
ls -l /usr/lib/git-core/git-flow*
```

There is no package? You can download it yourself,
or pull something down from GitHub, or make your own command and install it.
The beauty of open source.

You don't have permission to install in `/usr/lib/git-core/`,
or you don't want to risk installing it there, or it's still in flux?
If you put `git-`*`my-new-subcommand-name`* anywhere in your path,
git will find it.

```bash
echo 'echo hello, git' > ~/bin/git-hello
chmod +x ~/bin/git-hello
git hello
```

That's why you don't have to put a hyphen in `git addfile` or `git scratch` .

**git** keeps commands into `/usr/lib/git-core/`, plus anywhere in your path.
Where else does it keep things?

```bash
cat ~/.gitconfig
vi ~/.gitconfig +/lol # or git config -e and search for 'lol'
```

This INI-format file keeps your config info,
including aliases, which are another way to extend git.
That's how `git lol` works.

Aliases can be anything.

```bash
git config --global flanagan.son robert
git config --global flanagan.daughter brigid
cat ~/.gitconfig
git config flanagan.son
```

When you write a command,
you can configure it with your own `~/.gitconfig` variables.
`git help config` will tell you config variables that **git** knows about,
out of the box. There are lots.

If it's a good command, you can install it into `/usr/local/bin/` for general use.
If you think I could use it, too, put it on GitHub, and send me email,
so I can clone it and install it.
Like `git-scratch`, if you love it, set it free.

Where else is outside `.git/`? Just commands in `/usr/lib/git-core/` and config info in `~/.gitconfig`?
Pretty much. So "almost nothing."

[Time to wrap up, for now](https://github.com/jsh/git-internals/blob/new-course/other-stuff/finis.md),
so I can set you free.

" 'Freedom'? That is Yang worship word."
