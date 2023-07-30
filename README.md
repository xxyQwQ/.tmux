.tmux
=====

Self-contained, pretty and versatile `.tmux.conf` configuration file.

Installation
------------

Requirements:

  - tmux **`>= 2.4`** running inside Linux, Mac, OpenBSD, Cygwin or WSL
  - awk, perl and sed
  - outside of tmux, `$TERM` must be set to `xterm-256color`

Installing in home directory:
```
$ cd
$ git clone https://github.com/xxyQwQ/.tmux
$ ln -s -f .tmux/.tmux.conf
$ cp .tmux/.tmux.conf.local .
```

You should never alter the main `.tmux.conf` or `tmux.conf` file. If you do,
you're on your own. Instead, every customization should happen in your
`.tmux.conf.local` or `tmux.conf.local` customization file copy.
