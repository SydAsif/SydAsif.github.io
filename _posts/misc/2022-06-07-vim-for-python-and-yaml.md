---
layout: single
title:  "Vim setting for Python and YAML"
date:   2022-06-07 12:30:00 +0500
categories: misc
tag: vim
toc: true
toc_label: "On This Post"
toc_sticky: true
---

## Introduction
In this short blog, I'm showing you how to set up a vim editor for Python and YAML programming languages. In automation for networking, Python and YAML are used most frequently.

## Vim setting for .vimrc

Create a .vimrc file in home directory and use the below setting for both languages:

```console
" Global Default Setting 
syntax on             " Enable syntax highlighting
set number            " Enable line numbers

set expandtab         " On pressing tab, insert 4 spaces
set autoindent        " Enable auto indenting
set shiftwidth=4      " Indent by 4 spaces when auto-indenting
set softtabstop=4     " Indent by 4 spaces when hitting the tab
filetype indent on    " Enable indenting for files

set nobackup          " Disable backup files
set wildmenu          " Display command line's tab-complete options as a menu.
set noswapfile        " Disable swap file
set noundofile        " Disable undo file
colorscheme torte

" PYTHON SETTING 
autocmd FileType python setlocal ts=4 sts=4 sw=4 expandtab number autoindent

"YAML SETTING
autocmd FileType yaml setlocal ts=2 sts=2 sw=2 expandtab autoindent
```
