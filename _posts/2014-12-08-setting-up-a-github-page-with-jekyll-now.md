---
layout: post
title: Setting up a GitHub Page with Jekyll Now
excerpt: "The one in which I document the process of setting up a GitHub Page."
modified: 2014-12-08
tags: [githubpages, jekyll]
---

Barry Clark, the guy whose GitHub Page theme I forked, has already given the
rundown on how to set up a [Jekyll Now](http://www.jekyllnow.com/) GitHub Page
[here](http://www.smashingmagazine.com/2014/08/01/build-blog-jekyll-github-pages/).
If you're interested in going this route, I'd suggest that you check out his
post first. This won't be a rehash of his guide. Everything worked pretty much
as advertised until I got to the point where I wanted to build my website
locally. See I have this issue where I don't like testing in production. I
haven't worked with ruby gems very much, and as it turns out I had some
[prerequisites](http://michaelchelen.net/81fa/install-jekyll-2-ubuntu-14-04/)
to install on my Ubuntu 14.04 machine:

{% highlight console %}
sudo apt-get install ruby ruby-dev make gcc nodejs
{% endhighlight %}

after that things went more smoothly:

{% highlight console %}
sudo gem install github-pages
cd <repo directory>
jekyll serve --watch
{% endhighlight %}

and your locally built website should be served up at:

{% highlight console %}
http://0.0.0.0:4000
{% endhighlight %}
