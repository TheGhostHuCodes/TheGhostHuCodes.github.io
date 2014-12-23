---
layout: post
title: Building Potion
excerpt: "The one in which I build an esoteric programming language."
modified: 2014-22-06
tags: [potion, vimscript]
---

Part of working through "[Learning VimScript the Hard
Way](http://learnvimscriptthehardway.stevelosh.com/)" involves sitting down and
writing your own plugin for the [Potion](http://perl11.org/potion/) programming
language. But before doing that I wanted to play around with the language for a
little bit. For those not in the know, Potion is a small programming language
that was written by "\_Why the lucky stiff", before his mysterious
disappearance from the Internet.

Again, prerequisites seem to be the difference between a smooth build, and
searching all over the Internet for reasons why an esoteric programming
language won't build on your machine (Ubuntu 14.04 in my case). Let's make sure
we have all of the prerequisites:

{% highlight console %}
sudo apt-get install build-essential libtool autotools-dev automake
{% endhighlight %}

Then clone over a copy of potion, build it, and test the build:

{% highlight console %}
cd ~
git clone https://github.com/perl11/potion.git potion-lang
cd potion-lang
make
make test
{% endhighlight %}

... and we're off to the races!
