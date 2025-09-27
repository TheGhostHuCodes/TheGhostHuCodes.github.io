+++
title = "Moving my ZFS Pool to Ubuntu 16.04 LTS"
description = "The one in which I remount my ZFS pool."
date = 2016-05-14

[taxonomies]
tags = ["zfs", "ubuntu-16.04"]
+++

So Ubuntu 16.04 LTS is finally out. Is it the LTS that I've been waiting for?
Ubuntu 15.10 was a fine operating system, but it promised out-of-the-box ZFS
support, and didn't really deliver on it. In the end I had to mess around with
systemd to get everything working and that was a bit of a pain.

You see, [years
ago](http://alteregocoding.blogspot.com/2014/04/setting-up-zfs-file-system-on-ubuntu.html)
I switched over to ZFS after one of my drives decided to give up the ghost.
Although I've been very happy with ZFS since then, it's always been kind of a
hassle to get things working again when I update my OS... that is, until now.
How hard is it to mount my ZFS pool in Ubuntu 16.04? 

```bash
$ sudo apt-get install zfsutils-linux
$ sudo zfs mount -vO -a
```

The `-vO` switch executes an overlay mount, which I need since I'm mounting my
ZFS `/home` over the existing `/home` directory on my SSD. After everything is
installed I can:

```bash
$ sudo zfs mount
tank                            /tank
tank/home                       /home
```

to make sure that the ZFS filesystem was mounted correctly.

To continue to mount the ZFS filesystem upon reboot we need to open up
`/etc/rc.local` and add the following line to the file:

```bash
zfs mount -vO -a
```

That's it? That's it. Log out, log back in and we're off to the races!