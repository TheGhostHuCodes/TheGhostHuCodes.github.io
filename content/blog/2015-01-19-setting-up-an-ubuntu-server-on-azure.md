+++
title = "Setting up an Ubuntu server in Azure"
description = "The one in which I use Microsoft hardware to Linux software."
date = 2015-01-19

[taxonomies]
tags = ["ubuntu", "azure"]
+++

For those of you who don't know, I work at a Microsoft shop. It's not as bad as
it initially sounds. Microsoft has changed a lot since the days when I was sure
that [they killed my
pappy](http://www.hanselman.com/blog/MicrosoftKilledMyPappy.aspx). By the way,
my favorite line from Scott Hanselman's post is how he describes Microsoft:
"*We're not nearly as organized as we'd need to be to be as evil as you might
think we are.*" I'll just leave it at that.

One of the perks of working at a Microsoft shop is my MSDN account,
and one of the perks of having an MSDN account is the free Azure benefits that
I get. What have I decided to do with my 100 Azure fun-bucks per month, you ask?
Of course, I'm going to set up an Ubuntu server! For the curious, 100 quatloos
a month on Azure can get you a D1 Linux VM (1 core, 3.5 GB RAM, 50 GB SSD), some
hard drive space, and leave enough left over to play around with some of the
other neat things that seem to be showing up on Azure (HDInsight / Machine
Learning, I'm looking at you).

Microsoft's "[Create a Virtual Machine Running
Linux](http://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-tutorial/)"
is surprisingly helpful, considering my usual subpar experience with Microsoft
documentation. If you're interested in doing things right, you should probably
also check out "[Introduction to Linux on
Azure](http://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-introduction/)"
I ended up just provisioning the VM with a password, and later I generated some
SSH keys like so:

```sh
ssh-keygen -t rsa -b 4096
ssh-copy-id -i id_rsa.pub <user>@<DNS name>
```

If you end up going my route, don't forget to disable password login to the
machine when you're all done. You can do that by editing your `sshd_config`
file.

```sh
sudo vi /etc/ssh/sshd_config
```

changing the line:

```sh
PasswordAuthentication yes
```

to read:

```sh
PasswordAuthentication no
```

Finally, you'll want to restart the VM so that your changes will take effect.