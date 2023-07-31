# Quickly Build Linux Terminal Development Environment

a guide powered by [zsh](https://www.zsh.org/) + [oh-my-zsh](https://ohmyz.sh/) + [tmux](https://github.com/tmux/tmux) + [oh-my-tmux](https://github.com/gpakosz/.tmux)

## Requirements

- Linux platform (e.g. Ubuntu 20.04)
- `root` or `sudo` privilege
- basic tools such as `curl` and `git`
- **purely available** network environment

## Installation

### zsh

Install `zsh` via `apt`.

```bash
$ sudo apt install zsh
```

Check whether `zsh` is available.

```bash
$ cat /etc/shells
# /etc/shells: valid login shells
/usr/bin/zsh
```

### oh-my-zsh

Install `oh-my-zsh` via `curl`. You can also use `wget` referred to [oh-my-zsh](https://ohmyz.sh/). Note that proxy may be needed.

```bash
$ cd
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

Change login shell into `zsh` and then re-login.

```bash
$ chsh -s /bin/zsh
```

Check whether `zsh` is login shell now.

```bash
$ echo $SHELL
/bin/zsh
```

If you are using `vscode` remote development, you should

- kill `vscode-server` in command panel
- modify `default terminal` in remote settings

These operations are necessary to make `zsh` the default shell.

`agnoster` theme is recommended.

```bash
$ vim ~/.zshrc
ZSH_THEME="agnoster"
```

Install `zsh-autosuggestions` and `zsh-syntax-highlighting` plugins and enable them.

```bash
$ git clone https://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
$ vim ~/.zshrc
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

### tmux

Install `tmux` via `apt`.

```bash
$ sudo apt install tmux
```

If `tmux` is already installed, restart it.

```bash
$ tmux kill-server
```

### oh-my-tmux

Install `oh-my-tmux` from `github`. My customized fork is used here. You can also start from [oh-my-tmux](https://github.com/gpakosz/.tmux) instead.

```bash
$ cd
$ git clone https://github.com/xxyQwQ/.tmux
$ ln -sf .tmux/.tmux.conf
$ cp .tmux/.tmux.conf.local .
```

## Optional

### migration

If you already have some customized settings in `.bashrc`, copy and append them to `.zshrc`. This promises your previous configurations are still available.

```bash
$ vim ~/.zshrc
# proxy setting
if [ -f /etc/profile.d/clash.sh ]; then
    . /etc/profile.d/clash.sh
fi
```

### anaconda

When you install `anaconda`, auto activation is recommended to be disabled. Otherwise, `PATH` could be switched incorrectly when you enter `tmux`.

```bash
$ vim ~/.condarc
auto_activate_base: false
```

### appearance

Hostname can be too long and meaningless. Hack the configurations to improve it.

For `oh-my-zsh`, modify `agnoster.zsh-theme`.

```bash
$ vim ~/.oh-my-zsh/themes/agnoster.zsh-theme
prompt_context() {
  if [[ "$USERNAME" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
    prompt_segment black default "%(!.%{%F{yellow}%}.)%n"
  fi
}
```

For `oh-my-tmux`, modify `~/.tmux.conf.local`.

```bash
$ vim ~/.tmux.conf.local
tmux_conf_theme_status_right=" #{prefix}#{mouse}#{pairing}#{synchronized}#{?battery_status,#{battery_status},}#{?battery_bar, #{battery_bar},}#{?battery_percentage, #{battery_percentage},} , %R , %d %b | #{username}#{root} "
```