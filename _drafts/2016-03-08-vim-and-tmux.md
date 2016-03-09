---
layout: post
title: vim & tmux
tags: [vim, tmux, tips]
---

For people who like staying in the terminal, a vim and tmux workflow is
flexible enough to perform most tasks. Here are a few tips on how to get started.

<!--excerpt-->

## 1. Basics

Vim is a popular modal text editor&mdash;modal in the sense that it operates in
a number of distinct editing modes such as insert, visual, and normal. Much can
be said about choosing a text editor, but this post is not about that.

Tmux is a terminal multiplexer. In short, it is a program that can simulate an
arbitrary number of shell instances within a single process. You can have one
shell running a localhost right next to another one that's free to run git commands
and keep them both in a single terminal window.

To use tmux, start a **session**

