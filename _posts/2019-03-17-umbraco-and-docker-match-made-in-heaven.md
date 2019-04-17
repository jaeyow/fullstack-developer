---
layout: posts
title: Umbraco and Docker, Match made in heaven
excerpt: "How to create a local development environment with Umbraco and Docker, plus 3 exclusive tips indside."
modified: 2019-03-17
date: 2019-03-17
tags: [docker, development environment, umbraco, gotchas]
header: 
  overlay_image: /images/daniel-cheung-554579-unsplash.jpg
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

## Gotchas
- Do a Ctrl+F5 to do a Run without debugging as debugging does not work with Docker for now. 
- To enable Virtualization to work on a Bootcamp Windows 10, you have to go back to Mac, and in Startup disk choose the Windows Bootcamp partition, then choose Restart. The restart button is importatnt, that is the only way to switch virtualization ON.
- In the docker run commnd, I did `
docker run -d -p 1433:1433 -e sa_password=StrongP@ssw0rd! -e ACCEPT_EULA=Y microsoft/mssql-server-windows-developer -v C:\ProgramData\Docker\volumes:C:\umbraco-volume` however this is wrong and will result in an error like so: `> docker run -d -p 1433:1433 -e sa_password=StrongP@ssw0rd! -e ACCEPT_EULA=Y microsoft/mssql-server-windows-developer -v C:\ProgramData\Docker\volumes:C:\umbraco-volume
02f2dd5042d3ce921dcdcb553d625c4c6874e3189603555db5af6a6aa013d449
C:\Program Files\Docker\Docker\Resources\bin\docker.exe: Error response from daemon: container 02f2dd5042d3ce921dcdcb553d625c4c6874e3189603555db5af6a6aa013d449 encountered an error during CreateProcess: failure in a Windows system call: The system cannot find the file specified. (0x2)
[Event Detail:  Provider: 00000000-0000-0000-0000-000000000000] extra info: {"CommandLine":"-v C:\\ProgramData\\Docker\\volumes:C:\\umbraco-volume","WorkingDirectory":"C:\\","Environment":{"ACCEPT_EULA":"Y","attach_dbs":"[]","sa_password":"StrongP@ssw0rd!","sa_password_path":"C:\\ProgramData\\Docker\\secrets\\sa-password"},"CreateStdInPipe":true,"CreateStdOutPipe":true,"CreateStdErrPipe":true,"ConsoleSize":[0,0]}`
  
