---
layout: post
title:  "YADR in Terminator"
date:   2014-03-08 20:11:21
categories: yadr terminator debian jessie
---

I'm been using GNU/Linux for almost 10 years and helping friends install it on
their computers.  Recently I tried out Lubuntu for something lightweight.  The
stability hasn't been so good for me and, shock horror, it crashed a few times.
Seemed time to switch distros, I went for Debian Jessie.  When you switch
distros I find one of the most painful things is transferring your settings /
dot files.

yadr
====

I've been pairing with a friend on his Mac and he used yadr so I thought I
should try it out.  It is a collection of dot files that adds great
functionality to your terminal and vim (probably more things but I haven't
fully explored it all yet).  On Lubuntu it didn't work out of the box so I'm
mainly writing this to make the installation processes easier in future and
help any one else who has the same issues.

I use Terminator because of its split screen feature and it has all the
options I need.  Except... on my friends' iTerm if you command click on a file
link (in an rspec error message for example) you are taken to the file and 
line number in your editor of choice: vim!

After installing yadr

* the colours in vim are messed up so I went to Preferences -> Profiles -> Colors 
and set the scheme as "Solarized Dark" and the pallet as "Solarized"

* the powerline fonts seemd hard to get working.  I tried following the readme docs 
and installing the "for Powerline" fonts and patching fonts but the status bar still had 
little squares with numbers inside and not the nice powerline symbols.  Turns out I
didn't have the right fonts, I need to download:
`cd ~/.fonts/ && git clone https://github.com/scotu/ubuntu-mono-powerline.git && fc-cache -vf ~/.fonts`

* the default font in gvim was bad, really bad so in `~/.vimrc` I added:

```
if has('gui_running')
  set guifont=Monospace\ 10
endif
```

* setting gvim to save when focus is lost on a window (e.g. you click away) stops you 
having to type `:w` all the time so I also add:
`:au FocusLost * :wa`

* it is a bit annoying that the Sneak plugin remaps 'S' so I also deleted these lines (295-297) 
from ".yadr/vim/bundle/vim-sneak/plugin/sneak.vim"
```
if !hasmapto('<Plug>SneakBackward') && !hasmapto('<Plug>Sneak_S', 'n') && mapcheck(
  nmap S <Plug>Sneak_S
endif
```


On Debian I also wanted to remap the keyboard so CapsLock and Escape were switched which I'll add later...
