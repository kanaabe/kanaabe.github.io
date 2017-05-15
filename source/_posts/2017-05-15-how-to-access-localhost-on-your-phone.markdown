---
layout: post
title: "How to access localhost on your phone"
date: 2017-05-15 12:36:42 +0200
comments: true
categories: development, testing, mobile
---

This post explains how to make localhost work on your mobile device.

<!-- more -->

Find the IP of your desktop machine. You can use `ifconfig` on mac to pull your public IP. Look for it in the `en0` section of the result:

```
> ifconfig
en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
  ether ---
  inet6 ---
  inet 1111.00.11.1 netmask 0xffffff00 broadcast 1111.00.11.2
  nd6 ---
  media: autoselect
  status: active
```

Make sure localhost is running, and that both your phone and browser are connected to the same network. Then, simply go to the IP address on your phone along with the port number. For example, if my IP is `1111.00.11.1` and my localhost is opening port 5000, go to `1111.00.11.1:5000` on your phone.