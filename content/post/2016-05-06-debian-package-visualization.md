---
author: Alex Vanderpot
categories:
- Uncategorized
date: "2016-05-06T19:29:14Z"
guid: https://alex.vanderpot.com/wp/?p=1
id: 1
image: /wp-content/uploads/2016/06/packagegraph.png
title: Debian Package Visualization
url: /2016/05/debian-package-visualization/
---

Recently, a close friend sent me a link to [this blog post](https://tech-foo.blogspot.com/2013/01/visualising-ubuntu-package-repository.html). The blog post goes over some details about exporting package relationships for Ubuntu in a format that can be read by graph generating software. The blog post was made in early 2013, so I decided to try it myself and add a few things. I made some slight modifications to his code, which can be found below.

The original blog post only contained image renderings. I imported the data into Gephi and produced several SVG renderings of the graph. I then overlayed the vector graphics onto a blank map using the Google Maps API. There are a few renderings with different graph parameters to choose from. The big dot at the center of the graph is libc6, which makes vulnerabilities like [CVE-2015-7547](https://security.googleblog.com/2016/02/cve-2015-7547-glibc-getaddrinfo-stack.html) seem very scary.

Click the image below to load the map visualization. Be forewarned, the SVG file is 3mb and can slow down some browsers.

[![packagegraph](https://vanderpot.com/wp-content/uploads/2016/06/packagegraph.png)](https://vanderpot.com/packages/)

A note about this code: Apparently the approach used in this snippet only shows a subset of packages that are in the apt repos. Thomi Richards did a [follow up post](http://www.tech-foo.net/ubuntu-package-repository-visualisation-take-2.html) explaining this. I may redo the map with the updated dataset, but I belive that this is sufficient for now. Also, I don’t want to run Gephi’s placement algorithm for another 4 hours. Thomi’s original code, slightly edited and reformatted, is reposted below.

<div class="oembed-gist"><script src="https://gist.github.com/ajvpot/cdec7bdc5f1da6d82da65a0257f19db2.js"></script><noscript>View the code on [Gist](https://gist.github.com/ajvpot/cdec7bdc5f1da6d82da65a0257f19db2).</noscript></div>
