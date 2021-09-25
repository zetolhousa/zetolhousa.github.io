---
title: "My Dotfile Favorites"
date: 2021-09-25T15:58:55+05:30
draft: true
---

Dotfiles are used to customize your system. The “dotfiles” name is derived from the configuration files in Unix-like systems that start with a dot (e.g. `.bash_profile` and `.gitconfig`). In this post I will share some of my most used configurations for some common dotfiles.

## .zshrc

```shell
greph () {
    fc -ln 0 | grep --color=auto $1 | awk '!seen[$0]++' | sed -e 's/^/>> /'
}
```
I love this one. Probably my favorite in this dotfile. Usually I find myself having to type a very long CLI command to execute something. Then execute some other commands. If I have to repeat that same command, I'll have to press up arrow key to go back the entire command execution history and find the command or re-type it from stratch or copy it in a notepad and paste it back. With this I can simply `greph substring_of_command` and get every matching command that was recently executed.

---

```shell
grepr () {
    grep -nri $1 *
}
```
This one helps me find a text pattern in current location and all its sub-directories. Pretty useful when you know a term but can't remember the location. I have a folder where I store a bunch of notes in markdown files. Doing a quick `grepr text_i_want` gives me the results.

---

```shell
u () {
   set -A ud
   ud[1+${1-1}]=
   cd ${(j:../:)ud}
}
```
It's tedious having to `cd ..` all the way up a deeply nested folder. With this you can simply `u 10` to go 10 directories up.

---

```shell
alias gls="gls --color=auto --group-directories-first -X -1"
alias cls="clear"
alias cdu="cd .."
alias gitc='git commit -m'
alias gits='git status'
alias gitl='git log'
alias gita='git add -A'
alias gitd='git diff'
alias gitb='git branch'
alias gitp='git pull'
alias gitch='git checkout'
```
There are my goto aliases on a daily basis. `cls` is probably my most used, can't live without it. If on a remote host I still do `alias cls='clear'` and go about doing my work on that host 😂 that's how much I need it.

Some other zsh configurations I have:
+ powerlevel10K theme
+ ohMyZsh

## .tmux.conf
```shell
unbind-key C-a
set -g prefix `
bind-key ` send-prefix
```
This update the **prefix key** to the tilde character. I find it so much more convenient and easy to reach.

---

```shell
set -g base-index 1
```
Sets the window indexing from 1. Makes more sense because on your keyboard 0 is at the right end which is supposed to represent the first window.

---

```shell
set -g history-limit 100000
```
Sometimes when you have a long file printed out the tmux window history is limited by some default lines and you lose ability to scroll beyond that.

---

```shell
set -g default-terminal "xterm-256color"
```
If not colored already, this colors the terminal similar to syntax highlighting for code but in this case highlights prompt, folderes, executables, etc. in its own colors.

## .vimrc
```shell
set nu              # line numbering
set relativenumber  # google it
set cursorline      # adds an underline to where cursor currently is
set wildmenu        # google it
set autoindent      # intelligently indent different files when editing
syntax on           # syntax highlighting
colorscheme elflord # highlighting color scheme
set tabstop=4       # each tab will have 4 spaces instead of usual 8
set shiftwidth=4    # google it
set softtabstop=4   # google it
set expandtab       # makes space character for each tab
set nowrap          # vim editor will not wrap lines to go to next line
set sidescroll=2    # speed of sidescroll
set hlsearch        # each search will highlight the pattern
set ic              # ignores case when searching
```
