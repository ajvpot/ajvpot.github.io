---
author: Alex Vanderpot
categories:
- Uncategorized
date: "2016-06-18T16:38:55Z"
guid: https://vanderpot.com/?p=59
id: 59
image: /wp-content/uploads/2016/06/nginx-logo-square.png
title: Securing NGINX with CloudFlare
url: /2016/06/configuring-nginx-to-work-with-cloudflare/
---

A determined hacker can expose the origin IP address of a website behind a reverse proxy service using many methods. One of the methods I have seen used against me is scanning the entire IPv4 address space and making an HTTP request to every IP address with the Host header set to my domain. If the origin server responds to this request with the same page that is served over CloudFlare, the attacker will know that they have found the correct origin server.

I wrote this script to generate an NGINX configuration file that will only allow access to a website from CloudFlare IP addresses. Although using the configuration that this script generates will make it harder to find your site’s origin IP address, attackers can still use methods like e-mail origin headers, WordPress pingbacks, and social engineering to find it. This script should not be the only method you are using to protect your website.

<div class="oembed-gist"><script src="https://gist.github.com/ajvpot/971fc97e2ae3033f0b6357f4924fe447.js"></script><noscript>View the code on [Gist](https://gist.github.com/ajvpot/971fc97e2ae3033f0b6357f4924fe447).</noscript></div>