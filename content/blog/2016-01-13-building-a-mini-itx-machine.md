+++
title = "Building a mini-ITX machine"
description = "The one in which I build the smallest computer I ever built."
date = 2016-01-13

[taxonomies]
tags = ["hardware", "mini-itx", "skylake"]
+++

It's been a while since the last time I built a computer from scratch. I think
it was in 2005. I say that because I remember a buddy of mine wanted me to play
World of Warcraft with him and I needed a new rig to do that. Since then I've
gradually upgraded some components (RAM, GPU, HDDs), but other than that It's
the same build as it was 10+ years ago.

Time for a refresh. Here's a list of components that I bought for my new rig:

- Gigabyte Z170N-Gaming5 Motherboard
- Intel i5-6500 LGA 1151 3.2 GHz Skylake CPU
- Fractal Design Node 304 Case
- Seasonic G-Series 550 W PSU
- 2x Corsair Vengeance LPX 8 GB 2666 MHz DDR4 

And here are some parts that I scavenged from my old build to cut down on cost:

- MSi N630GT-MD1GD3 (NVIDIA GeForce GT630) GPU
- 256 GB Samsung 840 EVO SSD
- 2x 2 TB WD 7200 RPM HDDs

The SSD is used for my OS and SWAP partitions, while the two HDDs are set up as
a mirrored ZFS pool and mounted as my `/home` directory.

I chose to go with a mini-ITX build because I had never built one before, but I
use to live with housemates who had these awesome shoebox sized rigs that fit
on their desktop. They were actually mini-DTX builds, but close enough. Also, I
thought it was finally time to get rid of my optical drive, and I really wanted
to have USB3 ports as well.

It being so long since I had built a computer from scratch, I did run into some
issues. The first thing I did was mount my CPU on the motherboard and pop on
the stock CPU fan that came with the processor. I then put the stand-offs into
my new case and installed the motherboard. Next I installed my GPU, SSD, and
RAM. I only added the OS drive to check to see that everything was working
properly. Finally, I added in the PSU and wired the whole thing up.

Installing the PSU into the Node 304 case was kind of annoying, so for the time
being I left it sitting sideways in the case. If I had to do it all over again,
I would recommend
[breadboarding](http://www.tomshardware.com/forum/262730-31-breadboarding) your
build before putting it in the case. I had issues initially with putting
everything on the motherboard all at once. After plugging everything in I turned
on the power, and nothing happened. Turns out my issue was #6 on this listing
of [things to do when your new build has post boot video
problems](http://www.tomshardware.com/forum/261145-31-perform-steps-posting-post-boot-video-problems).

I ended up disconnecting everything from the motherboard, putting in only one
stick of RAM, and plugging in the DVI-D cable into the integrated graphics on
the motherboard. This solved my initial problems. From there I was able to set
an XMP profile, which was able to detect the correct RAM frequency properly in
the BIOS. Then I was able to put in the second stick of RAM. From there I
plugged in the GPU and switched my monitor over to that. At this point the
whole build was still spread over most of my desk.

When I tried to start putting things in their place, I noticed that the
clearance between the PSU and the SATA-III ports were about 5 mm. There was no
way that I was going to get a normal SATA cable to bend in that space. It's
certainly something to think about when putting the Z170N-Gaming5 motherboard
in the Node 304 case. It turns out, what I needed was either [left-angle SATA
cables](http://www.amazon.com/gp/product/B005S0X2OI?psc=1&redirect=true&ref_=oh_aui_detailpage_o03_s00)
or [mini SATA
cables](http://www.amazon.com/gp/product/B0068Q59O2?psc=1&redirect=true&ref_=oh_aui_detailpage_o03_s00).
I bought two of each, and plugged them all in, even though I only need 3,
because I don't want to have to remove the hard drives and PSU just to plug in
a single SATA cable. For anyone considering a build with this motherboard and
case combination, I recommend the mini SATA cables. They have sufficient bend
in so that you can plug them into the SATA port without too much trouble.

After all was said and done, I dropped Ubuntu 15.10 on it and ran Geekbench. My
Geekbench 3 score came out at slightly over 3800 for single core performance.
Not too bad. I'll take it!