+++
title = "Writing a Jekyll blog using a Docker container"
description = "The one in which I use docker to compile Jekyll sites."
date = 2017-05-30

[taxonomies]
tags = ["jekyll", "docker", "containers"]
+++

Lately I have been really getting into the workflow of containerizing
dependencies, and using those containers to get work done. It's also been a
while since I regularly wrote a blog post, so I was pleasantly surprised today
to find that [Jekyll](https://hub.docker.com/r/jekyll/jekyll/) has been
containerized. The workflow where I simply start a container to compile my
Jekyll site is vastly superior to what I use to do, which involved installing
Ruby, and a bunch of bundles on my system.

Honestly, I don't really know Ruby, and although I do like learning new
languages, Ruby and its packaging/dependency system isn't very high up on my
list right now. I would much rather start up an application, and have it run in
the background, compiling my static site for my blogging pleasure. That's where
Docker comes in.

We'll start by getting the latest Jekyll container:

```sh
docker pull jekyll/jekyll
```

If you're using Native Docker, you can then start the container from the
directory where your Jekyll site repository is, using the command: 

```sh
docker run --rm --label=jekyll --volume=$(pwd):/srv/jekyll \
  -it -p 127.0.0.1:4000:4000 jekyll/jekyll jekyll serve
```

and now you should be able to visit your compiled site at `0.0.0.0:4000` from
your browser of choice.

However, that `docker run` command is a bit difficult to remember, so here's a
`docker-compose.yml` file that does the same thing:

```yaml
version: '3'
services:
    local-jekyll:
        container_name: local-jekyll
        image:
            jekyll/jekyll
        ports:
            - "4000:4000"
        volumes:
            - .:/srv/jekyll
        command: jekyll serve
```

check that file into your site repository directory and from there run:

```sh
docker-compose up
```

and you're ready to blog!
