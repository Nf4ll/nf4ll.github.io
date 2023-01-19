---
title: Looking glass
author: nf4ll
date: 2022-12-11 12:21:00 +0000
categories: [Hack The Box, Challenge] 
tags: [Web, Remote Code Execution, Command Injection]
math: true
mermaid: true
image:
  path: /assets/img/posts/LookingGlass/web.PNG
  width: 1019
  height: 500
---
# Challenge: Looking Glass

Looking Glass challenge is a Web-challenge. It include the following description:
"We've built the most secure networking tool in the market, come and check it out!"

## Vulnerability

In this web page we can found a remote command execution vulnerability. If someone exploits this vulnerability, the attacker can gain access to a system. The attaker can access to a vulnerable system where he hasn't any perrmision. 
With this vulnerability the attacker can, for example, search files, gain acces with a shell or get confidential information.

## Explotation
1.  I go to the web page and I can run ping or traceroute like in the following image:
![Desktop View](/assets/img/posts/LookingGlass/page.PNG)
2. I try to concatenate a command to run this after running the ping. It can be concatenate by different ways:
```bash
| #This symbol concatenate two commands but we only see the output of the second command.
; #This symbol is to finish the command, so we can run another command.
```
![Desktop View](/assets/img/posts/LookingGlass/codeInj.PNG)
3. Now I know that I can run commands, so I search the file in the root directory with the next command:
![Desktop View](/assets/img/posts/LookingGlass/directoryList.PNG)
4. Finally I want to display the flags with `cat` command:
![Desktop View](/assets/img/posts/LookingGlass/flag.PNG)

