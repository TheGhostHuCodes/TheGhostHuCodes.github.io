---
layout: post
title: Building Unison
excerpt: "The one in which I build a version of Unison on Xubuntu to match the one in OSX."
modified: 2015-12-04
tags: [Unison, OSX, Xubuntu]
---

Having switched over to a Mac laptop brings with it some challenges when my
main desktop is still running Linux. Since I recently took the time to install
Xubuntu on my desktop machine, I thought I'd get everything setup again so that
I can seamlessly sync my data between my laptop and my desktop. To do this I
needed to build a copy of Unison that was the same version as the version
available in homebrew. In my case this was the 2.48.3 version of Unison.

First we'll need some prerequisites. Unison is written in OCaml.

{% highlight bash %}
sudo apt-get install ocaml liblablgtk2-ocaml-dev
{% endhighlight %}

Next, we'll set up a temporary directory and grab a copy of the version of
Unison that we need.

{% highlight bash %}
mkdir tempBuild
cd tempBuild
wget http://www.seas.upenn.edu/~bcpierce/unison//download/releases/stable/unison-2.48.3.tar.gz
tar xvfz unison-2.48.3.tar.gz
{% endhighlight %}

Finally, we'll go into that directory, build unison, and copy it over to a
directory in my path.

{% highlight bash %}
cd unison-2.48.3
make UISTYLE=text
make unison
mv unison /usr/local/bin/
{% endhighlight %}

Note, I chose to put unison in `/usr/local/bin/` because this path is searched
when I start a terminal in non-interactive mode. This is important because when
I execute the `unison` command on my laptop it executes on the remote machine
in non-interactive mode.
