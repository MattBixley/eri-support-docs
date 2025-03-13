---
created_at: '2025-03-13T00:34:14Z'
tags:
- ssh
- howto
- bashrc
description: How to setup your bashrc file so that is loads correctly on connectioneRI cluster.
---


## Preamble

When bash is invoked as an interactive login shell, or as a non-interactive shell with the `--login` option, it first reads and executes commands from the file `/etc/profile`, if that exists.  After reading that file, it looks
for `~/.bash_profile`, `~/.bash_login`, and `~/.profile`, in that order, and reads and executes commands from the first one that exists and is readable.  The `--noprofile` option may be used when the shell is started to inhibit this behavior.

When an interactive login shell exits, or a non-interactive login shell executes the exit builtin command, bash reads and executes commands from the file `~/.bash_logout`, if it exists.

When an interactive shell that is not a login shell is started, bash reads and executes commands from `~/.bashrc`, if that file exists.  This may be inhibited by using the `--norc option`.  The `--rcfile` file option will  force  bash to read and execute commands from file instead of `~/.bashrc`.

## Setup
To ensure that your `.bashrc` is sourced correctly you need to add the following to `~/.bash_profile`

```
# include .profile if it exists
[[ -f ~/.profile ]] && . ~/.profile

# include .bashrc if it exists
[[ -f ~/.bashrc ]] && . ~/.bashrc
```

## Usage

Assuming you have followed the setup above you will be able to connect to the clusters directly using;

```sh
ssh eri
```

And if you have a prompt and other commands set they should now be visible.
