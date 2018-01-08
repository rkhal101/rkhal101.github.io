---
layout: page
title: OverTheWire Waregames Bandit Level 1 Writeup
categories: [overTheWire-waregames-writeup]
permalink: /writeups/wargames/bandit/level1
---

# [Bandit Level 0 -> Level 1](http://overthewire.org/wargames/bandit/bandit1.html)

## Level Goal: 

> The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.


## Write-up: 
First, you display the contents of the directory using the following command:

```shell
ls
```

The output shows that a ```readme``` file exists in the home directory.

Second, display the contents of the read me file:

```shell
cat readme
```

The output will display the password to log into bandit1.

```shell
boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```

SSH into bandit1 using the discovered password to complete the next level.

```shell
ssh bandit1@bandit.labs.overthewire.org -p 2220
```

Proceed to the [next level write-up](/writeups/wargames/bandit/level2).
