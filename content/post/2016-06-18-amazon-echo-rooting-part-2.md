---
author: Alex Vanderpot
categories:
- Uncategorized
date: "2016-06-18T15:53:37Z"
guid: https://alex.vanderpot.com/wp/?p=41
id: 41
image: /wp-content/uploads/2016/06/echoboardsmall.png
tags:
- Amazon Echo
title: 'Amazon Echo Rooting: Part 2'
url: /2016/06/amazon-echo-rooting-part-2/
---

# Filesystem Information

While searching through the partial filesystem I extracted from the package updates, I found /etc/dev.tar which appears to be a skeleton of the dev filesystem. We can infer several things about the partition layout on the internal MMC with this information.

<div class="oembed-gist"><script src="https://gist.github.com/ajvpot/ec10e2116fb8a97aa43e9495ea1dbd17.js"></script><noscript>View the code on [Gist](https://gist.github.com/ajvpot/ec10e2116fb8a97aa43e9495ea1dbd17).</noscript></div>We now know that the internal MMC has 8 partitions and we know the names of all of those partitions. Next, in the open source code released by Amazon as required by the GPL, we can find the uBoot options that load the operating system.

<div class="oembed-gist"><script src="https://gist.github.com/ajvpot/7a7acdaa648b09a431a608231a912111.js"></script><noscript>View the code on [Gist](https://gist.github.com/ajvpot/7a7acdaa648b09a431a608231a912111).</noscript></div>The environment variable ${root} is set in u-boot/board/ti/lab126/evm.c.

<div class="oembed-gist"><script src="https://gist.github.com/ajvpot/3977c1eff2a8035e55f42b87816d9d0a.js"></script><noscript>View the code on [Gist](https://gist.github.com/ajvpot/3977c1eff2a8035e55f42b87816d9d0a).</noscript></div>This will set ${root} to /dev/mmcblk1p%d where %d is the index of a partition labeled main-A. The bootloader will try to load this filesystem as ext3.

# Building the SD Card

## Partitioning the SD Card

![Create Partitions](https://vanderpot.com/wp-content/uploads/2016/06/1createpartitions.png)

It appears that uBoot will only attempt to use the partition named main-A as the root filesystem. I created a small partition named \_ because there is a bug with get\_partition\_num that will cause it to occasionally be unable to find the first partition on the disk.

## Installing the TI SDK

We’ll need the files from the TI SDK to supplement what isn’t available in the Amazon packages. We will extract the filesystem provided by TI for this CPU, then extract the Amazon provided files over it.

![SDK Setup](https://vanderpot.com/wp-content/uploads/2016/06/2dvsdk-Setup.png)

<div class="oembed-gist"><script src="https://gist.github.com/ajvpot/9292009ab8642dd7f0186e495ada13e6.js"></script><noscript>View the code on [Gist](https://gist.github.com/ajvpot/9292009ab8642dd7f0186e495ada13e6).</noscript></div>More information on this subject can be found on the [Wiki](https://github.com/echohacking/wiki/wiki). A prebuilt Debian SD card image is available for use.