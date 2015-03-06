---
layout: post
title: Adding Swap space to an Ubuntu server in Azure
excerpt: "The one in which I add some swap space to my Azure VM."
modified: 2015-01-30
tags: [Ubuntu, Azure]
---

So a few weeks ago, I was working on building LLVM/Clang from source (a story
for another time) and in the process I kept getting these errors:

{% highlight bash %}
Linking CXX executable ../../../../bin/clang
collect2: error: ld terminated with signal 9 [Killed]
make[2]: *** [bin/clang-3.5] Error 1
make[1]: *** [tools/clang/tools/driver/CMakeFiles/clang.dir/all] Error 2
make: *** [all] Error 2
{% endhighlight %}

Obviously, something bad was happening, so I Googled around and it seems that
the error often occurs when linking and not having enough memory. But wait, I'm
sure I have plenty of memory in my Azure VM, 3.5 GB of RAM and some extra Swap
space to boot.

{% highlight bash %}
$ free -h
             total       used       free     shared    buffers     cached
Mem:          3.4G       871M       2.5G       416K        78M       600M
-/+ buffers/cache:       192M       3.2G
Swap:           0B         0B         0B
{% endhighlight %}

OH...

.. and then I found [this blog
post](http://blogs.msdn.com/b/piyushranjan/archive/2013/05/31/swap-space-in-linux-vm-s-on-windows-azure-part-1.aspx). 

Really, Microsoft? No Swap space? Not even a little?

Let's go ahead and use the good 'ol estimate of ~2x my physical RAM for the
Swap space.

{% highlight bash %}
$ sudo fallocate -l 7g /mnt/swap7gb
$ sudo chmod 600 /mnt/swap7gb
$ sudo mkswap /mnt/swap7gb
$ sudo swapon /mnt/swap7gb
{% endhighlight %}

And now I have Swap space!

{% highlight bash %}
$ free -h
             total       used       free     shared    buffers     cached
Mem:          3.4G       871M       2.5G       416K        78M       600M
-/+ buffers/cache:       192M       3.2G
Swap:         7.0G         0B       7.0G
{% endhighlight %}

That's much better.
