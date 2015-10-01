## Class Checklist for Students

Here's your checklist. If you want a discursive list, with explanations,
[it's here](https://docs.google.com/document/d/1eQr6fFiZPGYNc2DSWdA1s5fS0nU5midRgpaZBttD49E/edit?usp=sharing).


- The computer you'll bring

  + bring up a terminal window running bash/dash/zsh/ksh and type basic, shell commands

  + ```uname -a``` says you have Linux or some other Unix-flavored OS.

  + **tree(1)** is installed

  ```bash
  tree
  ```

  + use some, installed programming editor (vi, emacs, gedit, atom, ...) to write and run a simple shell script

  ```bash
  $ cat hello
  #!/bin/bash -eux
  echo hello, world
  $ ./hello
  hello, world
  ```

- git

  + ```git version``` shows >= 1.9.1

  + you have colorized git output

  ```bash
  git config --global ui.color auto
  git log
  ```

  + you have the alias ```git lol```

  ```bash
  git config --global alias.lol ’log --graph --decorate --oneline --all’
  ```

- GitHub

  + clone some repos


  ```bash
  git clone https://github.com/jsh/git-under-the-hood
  git clone https://github.com/jsh/git-scratch
  cd git-scratch
  make install
  ```

  + create a repo on GitHub

  + push to the repo from the machine you'll use

- Networking

  + ```~/.ssh/``` is set up so ***you are not prompted for a password*** for this

  ```bash
  ssh localhost
  ```
