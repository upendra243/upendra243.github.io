---
layout: post
title : Route Web Traffic Securely Without a VPN Using a SOCKS Tunnel
description : Web Traffic Securely Without a VPN Using a SOCKS Tunnel, SSH Tunnel + SOCKS Proxy Forwarding = Secure Browsing
subtitle : "SSH Tunnel + SOCKS Proxy Forwarding = Secure Browsing"
date: 2018-01-02 16:41:10
author: "Upendra Pratap Kushwaha"
header-img: "img/posts/android-bg.jpg"
comments: true
tags: [CodeMonkey]
---

# Introduction

When you are at the coffee shop, or at a conference, and you are not sure that you want to send all your data over the wi-fi network in plain text, you want a secure tunnel to browse.You want to make sure no one in the middle is watching the traffic.

One solution is a VPN, but many VPNs require special client software on your machine, which you may not have rights to install.

If all you need to secure is your web browsing, there is a simple alternative: a SOCKS 5 proxy tunnel.

A SOCKS proxy is basically an SSH tunnel in which specific applications forward their traffic down the tunnel to the server, and then on the server end, the proxy forwards the traffic out to the general Internet.

We are going to setup a socks proxy and configured Firefox browser to route all traffic via new socks tunnel.

# Prerequisites
* A server to create socks tunnel with SSH access(example.com)
* A non-root user with `sudo` access(demo)
* Firefox web browser

# Step 1- Create a Tunnel (Linux)
You can use the “-D” flag of ssh to create a SOCKS proxy.
```
ssh -D 8088 -f -C -q -N demo@example.com
```
* D: To create SOCKS tunnel on the specified port number
* f: Forks the process to run in the background
* C: Compresses the data before sending it
* q: Uses quiet mode
* N: Tells SSH that no command will be sent once the tunnel is up

Verify that tunnel is created properly run following command-
```
upendra 31237 0.0 0.0 48040 5476 ? Ss Sep25 0:12 ssh -D 8088 -f -C -q -N demo@example.com
```
# Step 2- Setup Firefox to use SOCKS Tunnel as proxy
The socks tunnel is created and running on port 8088. This port is used to configure Firefox. Steps to configure proxy –

1. Go to Preferences section of browser settings.

![preference.png](/img/posts/preference.png)

2. Click on Advance setting option and click network tab as shown
![advance-768x468.png](/img/posts/advance-768x468.png)

3. Configure SOCKS PROXY as bellow image.
4. Select Radio Manual proxy configuration
5. Added SOCKS host = localhost
6. Added socks port = 8088(for this example)
7. Check the radio of SOCKS v5
![proxy_setup.png](/img/posts/proxy_setup-768x393.png)
