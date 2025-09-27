+++
title = "Switching git profiles"
description = "The one in which I pop back and forth between my work and home git profiles."
date = 2016-10-15

[taxonomies]
tags = ["git"]
+++

I use git at work, which is great, but I also still work on personal side
projects for fun at home. I like to use my legal name and personal email when
working on my own projects, but I prefer to use my nickname and am required to
use my work email when committing to work related projects. That means I'm
always trying to remember which `user.name` and `user.email` is set to a
particular git repository, and dealing with setting that up correctly can be a
real pain.

If all I wanted to do was set my `user.email` then I could write a simple git
alias as described
[here](http://www.codeography.com/2011/08/05/project-specific-git-author.html),
but what I'd really like to do is set both my `user.name` and `user.email` in a
single git alias. Unfortunately you can't easily do that in a single git alias.
However, what you can do, as I learned from this blog post on [advanced git
aliases](http://blogs.atlassian.com/2014/10/advanced-git-aliases/), is shell out
to bash and from there the world is your oyster! For example, I added the
following to my `~/.gitconfig` file:

```bash
[alias]
  athome = "!f() { \
    git config user.name \"Yung-Jin (Joey) Hu\"; \
    git config user.email \"yungjinhu@gmail.com\"; \
    }; f"
  atwork = "!f() { \
    git config user.name \"Joey Hu\"; \
    git config user.email \"myemail@work.com\"; \
    }; f"
  whoami = "!f() { \
    git config user.name ; \
    git config user.email ; \
    }; f"
```

Now I've got these awesome git aliases that let me check my current profile (`git whoami`) and
switch user profiles easily (`git athome` and `git atwork`) within a git repo:

```bash
$ git whoami
Joey Hu
myemail@work.com
$ git athome
$ git whoami
Yung-Jin (Joey) Hu
yungjinhu@gmail.com
$ git atwork
$ git whoami
Joey Hu
myemail@work.com
```