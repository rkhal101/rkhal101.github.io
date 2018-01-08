---
layout: page
title: OverTheWire Waregames Bandit Level 3 Writeup
permalink: /writeups/wargames/bandit/level3
---

# [Bandit Level2 -> Level 3](http://overthewire.org/wargames/bandit/bandit3.html)

## Level Goal: 

> The password for the next level is stored in a file called spaces in this filename located in the home directory

## Write-up: 
First, verify that the file is located in the home directory:

```shell
ls
```

The output shows that a ```spaces in this filename``` file exists in the home directory.

Second, display the contents of the file:

```
 cat spaces\ in\ this\ filename
```

The output will display the password to log into bandit3.

```shell
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```

SSH into bandit3 using the discovered password to complete the next level.

```shell
ssh bandit3@bandit.labs.overthewire.org -p 2220
```

Proceed to the [next level write-up](/writeups/wargames/bandit/level4).
