---
layout: post
title: tmux
tags: [tmux, unix]
---

![tmux]({{ site.baseurl }}/img/vim-and-tmux/splash.png)

For people who like staying in the terminal, tmux will help you do exactly that.

<!--excerpt-->

## Basics

Tmux is a terminal multiplexer. In short, it is a program that can simulate an
arbitrary number of shell instances within a single process. You can have one
shell running a localhost right next to another one that's free to run git commands
and keep them both in a single terminal window.

Installation:

~~~ sh
$ brew install tmux
~~~

To use tmux, start a **session** ([what is a session?](#what-is-a-session-anyways))
by navigating to the primary directory you want to work in and running

~~~ sh
$ tmux
~~~

or

~~~ sh
$ tmux new -s session_name
~~~

![tmux]({{ site.baseurl }}/img/vim-and-tmux/basic.png)

The bottom of the terminal window now displays a the tmux **statusline**. Yours
will look different from mine, but I'll go through how to change that later.

Going from left to right, the first "0" is just the name of the session. If you
did not specify a session name, tmux will automatically assign an integer name,
which starts at zero. The `0: zsh` tab indicates that we are currently looking
at the zeroth **window** in our session, which is running a process, `zsh`.

## Windows

A *session* consists of one or more *windows*. To create another window, use the
keystroke <kbd>C-b c</kbd> (<kbd>ctrl+b</kbd> then <kbd>c</kbd>).

![tmux]({{ site.baseurl }}/img/vim-and-tmux/windows.png)

Now, you should see a second tab labeled `1: zsh` (or `bash`/whichever default
shell you use). We'll call this window 1 (window 0 was created when we started
the session).

To cycle between windows, you have the following options:

key              | action
--------         | ------
<kbd>C-b n</kbd> | next
<kbd>C-b p</kbd> | previous
<kbd>C-b k</kbd> | goto window `k`

## Prefix & tmux.conf

Now's a good time to decide whether or not you like the default prefix, <kbd>C-b</kbd>.
Personally, I prefer <kbd>C-a</kbd> since "a" is closer to the control key than b.

If you do want to change this, create a file named `.tmux.conf` in your home
directory, and add the following lines in (and replace `C-a` with your preferred
keystroke)

~~~ conf
# remap prefix from 'C-b' to 'C-a'
unbind C-b
set-option -g prefix C-a
bind C-a send-prefix
~~~

The `.tmux.conf` file is a configuration file for tmux, much like a `.zshrc` or
`.bashrc`. There will be a few convenient settings you may want to add as we go
through the rest of the tutorial, so you may want to create a `.tmux.conf` even
if you decided to keep the default prefix.

## Panes

If a session is a collection of windows, then a window must but a collection of
**panes**.

![tmux]({{ site.baseurl }}/img/vim-and-tmux/splits.png)

Use <kbd>prefix %</kbd> to create a vertical split and <kbd>prefix "</kbd> for a
horizontal split. (I'm using `prefix` instead of <kbd>C-b</kbd> or <kbd>C-a</kbd>
for the rest of the article.)

In my opinion, these keybindings make absolutely no sense. Perhaps keyboards were
a bit different when tmux was written. So lets remap them to something a little
easier to remember:

~~~ conf
# Sane splits
bind \ split-window -h
bind - split-window -v
unbind '"'
unbind %
~~~

On my keyboard, `\` shares a key with the pipe character, `|`, which looks like
a horizontal divider. And `-` is about as close as you can get to a vertical
divider, so those were the keys I chose.

You can close panes and windows with <kbd>prefix x</kbd>, by sending an EOF symbol
with <kbd>C-d</kbd>, or by typing `logout`.

## Sane Pane Navigation

The default way of moving between panes is using <kbd>prefix o</kbd> to cycle.
If you like vim keybindings, the following bindings will allow you to use
<kbd>prefix [hjkl]</kbd> to jump to the next pane in a given direction.

~~~ conf
# Navigate panes with hjkl
unbind j
bind j select-pane -D
unbind k
bind k select-pane -U
unbind h
bind h select-pane -L
unbind l
bind l select-pane -R
~~~

## Use your mouse (only if you want to)

Sometimes, it's just easier.

~~~ conf
# Mouse
set -g mode-mouse on
set -g mouse-resize-pane on
set -g mouse-select-pane on
set -g mouse-select-window on
~~~

## Detaching and reattaching

To **detach** from your current session, just run <kbd>prefix d</kbd>.
To reattach to an existing target session, run

~~~ sh
$ tmux attach -t target_name
~~~

## What is a session, anyways?

Tmux is based on a client-server model. The first time your run `tmux`, you start
a tmux server on your computer and create a session on that server. A tmux server
can host multiple sessions. A session is just a collection of tmux windows (and
windows are just collections of panes).

The client in this model is your terminal window. You are automatically connected
to sessions upon creation, and can connect to existing sessions using `tmux attach`.
Clients talk to the server using sockets, and detaching from a session is simply
disconnecting the client (your terminal) from the server (running on your compute
somewhere). That's why your windows and panes stay where you left them upon
reattaching.

To view existing sessions

~~~ sh
$ tmux ls
~~~

and to kill a target session

~~~ sh
$ tmux kill-session -t session_name
~~~

## What next?

Tmux is very flexible, which makes it quite powerful. I find it extremely useful
when ssh-ed into another machine. In the past, I would use multiple terminals
and ssh multiple times so I could have one window to edit text and another to
run commands. Now, I simply ssh once and create a tmux session. If the machine
you're ssh-ed into allows it, you can also detach from your tmux sessions and
reattach to them at an arbitrary time in the future.

That was a walkthrough of some of my most frequently used tmux commands. For visual
tweaks, check out my
[`.tmux.conf`](https://github.com/zhaorz/.dotfiles/blob/master/tmux.conf)
on Github. You may need powerline fonts for the decorators to show up.

For more information on tmux in general, `man tmux` is a great place to start.



