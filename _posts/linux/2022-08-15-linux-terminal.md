---
layout: single
title:  "Linux Terminal and Vim: An Integration Guide"
date:   2022-08-15 15:02:15 +0500
categories: linux
tags: linux
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Introduction
Productivity tools on Linux often include both a status line and a prompt. The function of a status line is to display important information relevant to the program’s current context, and a prompt identifies where a program is expecting some input from the user. Some good application examples that utilize these features include the Linux shell and Vim.

## Integration of ZSH, Oh My Zsh and Powerlevel10 with Linux terminal

### Installing ZSH shell

In this section, I will show you how to install the ZSH shell on Linux (pop-os/ubuntu) operating system and customise it with ohmyzsh framework and PowerLeve10K theme.

Search for zsh with your package manager, the below output is edited.

```bash
lab@pop-os:~$ apt search zsh
Sorting... Done
Full Text Search... Done
zsh/jammy,now 5.8.1-1 amd64 [installed]
  shell with lots of features

zsh-antigen/jammy,jammy,now 2.2.3-5 all [installed]
  manage your zsh plugins

zsh-autosuggestions/jammy,jammy,now 0.7.0-1 all [installed]
  Fish-like fast/unobtrusive autosuggestions for zsh

zsh-common/jammy,jammy,now 5.8.1-1 all [installed,automatic]
  architecture independent files for Zsh

zsh-dev/jammy 5.8.1-1 amd64
  shell with lots of features (development files)

zsh-doc/jammy,jammy 5.8.1-1 all
  zsh documentation - info/HTML format

zsh-static/jammy 5.8.1-1 amd64
  shell with lots of features (static link)

zsh-syntax-highlighting/jammy,jammy,now 0.7.1-2 all [installed]
  Fish shell like syntax highlighting for zsh

zsh-theme-powerlevel9k/jammy,jammy,now 0.6.7-2 all [installed]
  powerlevel9k is a theme for zsh which uses powerline fonts
```

Install zsh and some Plugins for autosuggestion and syntax highlighting.

```terminal
sudo apt install zsh zsh-syntax-highlighting zsh-autosuggestions zsh-antigen
```

Next, install Oh My Zsh.

### [Installing Oh My Zsh](https://ohmyz.sh/)

Oh My Zsh is a delightful, open source, community-driven framework for managing your Zsh configuration. It comes bundled with thousands of helpful functions, helpers, plugins, and themes.

Oh My Zsh is installed by running one of the following commands in your terminal. You can install this via the command-line with either curl or wget. When installed, it will auto configure the setup.

```console
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

or

```console
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

Download Plugins for autosuggestion and syntax highlighting.

```terminal
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH/plugins/zsh-autosuggestions
```

```console
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH/plugins/zsh-syntax-highlighting
```

Next, install PowerLevel10k theme

### Install [PowerLeve10K](https://github.com/romkatv/powerlevel10k#oh-my-zsh) theme

We will clone the repository into the default theme folder

```console
git clone https://github.com/romkatv/powerlevel10k.git $ZSH/themes/powerlevel10k
```

To download font, see [Manual font installation](https://github.com/romkatv/powerlevel10k#manual-font-installation). It’s the best and works everywhere. For Linux (Ubuntu) you will need this font, otherwise, your terminal may not render clean status lines and prompts in zsh.

Now edit your `~/.zshrc` file to use the PowerLeve10K theme, Awesome Patched font, Autocorrect, Autosuggestion and Syntax highlighting.

```console
vim ~/.zshrc
```

Find these settings and replace them with the below configuration.

```bash
# Find the ZSH_THME and replace it with
ZSH_THEME="powerlevel10k/powerlevel10k"
# If you want to enable auto correction,uncomment the line
ENABLE_CORRECTION="true"
# add plugins so scroll down a little till you find
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
# add red dot completion
COMPLETION_WAITING_DOTS="true"
# add path for theme
source ~/.oh-my-zsh/themes/powerlevel10k/powerlevel10k.zsh-theme
# To customize prompt, run `p10k configure` or edit ~/.p10k.zsh.
[[ ! -f ~/.p10k.zsh ]] || source ~/.p10k.zsh
source ~/.oh-my-zsh/themes/powerlevel10k/config
# color out put for ip cmd
alias ip='ip -c'
```

You will also have to go to the preferences of your terminal and change to the custom font which you installed.

### Now the last step

You will need to run `p10k configure` command to set up your terminal looks. Just follow the steps which you see on the screen.

For other operating systems see this [tutorial](https://medium.com/@shivam1/make-your-terminal-beautiful-and-fast-with-zsh-shell-and-powerlevel10k-6484461c6efb) to customize it with ohmyzsh framework and PowerLeve10K theme.

## Integration of [Powerline](https://github.com/powerline/powerline) with Vim

Powerline is a status line plugin for vim, and provides status lines and prompts for several other applications, including zsh, bash, fish, tmux, IPython, Awesome, i3 and Qtile.

Powerline is written in the Python programming language, which means that your system will need to have a recent version of Python and pip to run it.

### Installing Powerline

In this section, we will install a powerline on Linux along with its dependencies and then go through how to integrate the powerline with the Vim text editor.

```console
pip install powerline-status
```

Then confirm its install location on your file system using pip’s show command:

```console
pip show powerline-status# Output

# output
Location: /home/lab/.local/lib/python3.8/site-packages
```

Add your location directory to the PATH variable in ~/.zshrc:

```bash
vim ~/.zshrc
# add this line
export PATH="~/.local/bin:$PATH"
```

I recommend installing the i3ipc package even if you are not an i3 user because it might come in handy later. Invoke pip to Install these packages:

```console
pip install psutil i3ipc
```

### Using Powerline with Vim

Your version of Vim must have been compiled with Python in order for powerline to work. Run the following command to check the Python versions your Vim installation supports:

```console
vim — version | grep +python

# Output
+python/dyn +python3/dyn
```

You are good to go if you see a line containing either +python or +python3, meaning that Vim supports Python3.

At this point, all we need to do is add some code to [.vimrc](https://gitlab.com/sydasif/vim/-/blob/main/.vimrc) to enable powerline:

```bash
# to set status line
set laststatus=2
python3 from powerline.vim import setup as powerline_setup
python3 powerline_setup()
python3 del powerline_setup
```

No other code is necessary to get the powerline working inside of Vim.
