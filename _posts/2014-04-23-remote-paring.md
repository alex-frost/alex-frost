---
layout: post
title: "Remote Pairing"
tags: [paring, zsh, git]
comments: true
---

When paring it is nice to make sure the commits are assigned to the correct names.
In fact, when you go back over the git log (or use blame) then seeing an accurate portrait can
be really important.

I’ve been working remotely for a few weeks and thought I’d note down my set-up. Firstly, I made a
file '~/.ssh/config' with:

```
Host nameForRemote
  HostName your_host_ip
  ForwardAgent yes
```

This means I can log onto the remote with `ssh nameForRemote` and commit using my local ssh key on the remote server.

Next I made a few alias to simplify pairing (and unparing) following this post on [git paring](http://thepugautomatic.com/2013/11/git-pairing/).
I use [YADR](https://github.com/skwp/dotfiles) and this comes with a great prompt but I wanted to add the initials of the pair.
The default prompt 'skwp' uses `git-info` and I changed line 412 to

```sh
git_info[$info_format]="$REPLY`git config user.pair`"
```

Note: this is a simplest thing I could do, you might want to do something a bit more comprehensive.

Finally, on the remote server in tmux in vim (phew!) the colours were all messed up.  I love having
clear colours for quick scanning of code so I had to force tmux to use colours properly.  
The `-2` option is meant to do this but tmux is very very picky about what `$TERM` is
set as, this alias worked for me:

```sh
tmux='TERM=screen-256color-bce tmux -2'
```

I'm on Debain, the other devs are on Macs and the server is on Ubuntu - and everyone is happy!

{% include JB/setup %}
