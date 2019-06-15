---
layout: posts
title: Easy way to automate Redis cache flush remotely in Powershell
excerpt: "How to easily clear your Redis cache remotely from a Windows machine with Powershell"
modified: 2019-05-01
date: 2019-05-01
tags: [powershell, Redis, continuous integration, continuous delivery]
header: 
  overlay_image: /images/taylor-kiser-373472-unsplash.jpg
  caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
comments: true
published: true
---

<section id="table-of-contents" class="toc">
  <header>
    <h3>Overview</h3>
  </header>
  <div id="drawer" markdown="1">
  *  Auto generated table of contents
  {:toc}
  </div>
</section>

## Synopsis
- clearing your Redis Cache involves logging in to a server containing your Redis instance and running a few Redis commands to flush the cache
- it doesn't matter if you have your own server with a Redis cache installation, or hosted in the Cloud like in [AWS Elasticache](https://aws.amazon.com/elasticache/) or [Azure Cache for Redis](https://azure.microsoft.com/en-gb/services/cache/), you can login just the same
- there is a tool [redis-cli](https://redis.io/topics/rediscli) available, but what if you don't want to build it yourself, or you simply can't, also this tool is only available in Linux, in this situation, we want to be able to do it from a Windows machine
- there is a Linux networking utility called [Netcat](http://netcat.sourceforge.net/) that can easily remotely connect to servers. There is also a port of this for [Windows](https://joncraton.org/blog/46/netcat-for-windows/) which we use in this post
- so first you connect to your Redis cache with:
  ```
  nc <ipaddress of redis server> <port of redis server>
  // once connected, run the following Redis commands
  SELECT 0 // specify your Redis index here
  +OK      // Redis reply 
  FLUSHDB  // now flush that DB index
  +OK      // Redis reply
  QUIT     // and then disconnect
  +OK      // Redis reply
  ```
  Now that's nice, however it is not clear what you need to do if you do this operation remotely from a Windows machine and plug it into your CI/CD system.
- Powershell to the rescue!

## Here is the Powershell script
It is surprisingly simple and can be done in a couple of lines of Powershell. 

```powershell
  $redisCommands = "SELECT $redisDBIndex`r`nFLUSHDB`r`nQUIT`r`n"
  $redisCommands | .\nc $redisServer 6379
```
In the first line, we are setting up the 3 Redis commands, but separating them in it's own line (crlf). Because we are in Powershell we have the pipe (|) operator to make things easy. We simply pipe the commands to nc.

As simple as that. 

  
