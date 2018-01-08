---
layout: page
title: OverTheWire Waregames Bandit Level 0 Writeup
permalink: /writeups/wargames/bandit/level0
---



### Level Goal: 

> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

### Write-up: 
This is a simple challenge that requires you to ssh into the target machine with the credentials bandit0:bandit0. We use the following command to accomplish the task:

```shell
ssh bandit0@bandit.labs.overthewire.org -p 2220 
```

Proceed to the [next level write-up](/writeups/wargames/bandit/level1).
