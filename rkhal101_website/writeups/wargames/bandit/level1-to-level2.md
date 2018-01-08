---
layout: page
title: OverTheWire Waregames Bandit Level 2 Writeup
permalink: /writeups/wargames/bandit/level2
---

# [Bandit Level 1 -> Level 2](http://overthewire.org/wargames/bandit/bandit2.html)

## Level Goal: 

> The password for the next level is stored in a file called - located in the home directory

## Write-up: 
First, verify that the file is located in the home directory:

```shell
ls
```

The output shows that a ```-``` file exists in the home directory.

Second, display the contents of the read me file. Inorder to do that we can't use the same command from the previous write-up because ```cat``` will view the filename ```-``` as a synonym for ```stdin```. Therefore, we have to change the string in such a way that the ```cat``` command will view it as a file. This can be done by prefexing the file name with a path.

```shell
cat ./-
```

The output will display the password to log into bandit2.

```shell
CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```

SSH into bandit2 using the discovered password to complete the next level.

```shell
ssh bandit2@bandit.labs.overthewire.org -p 2220
```

Proceed to the [next level write-up](/writeups/wargames/bandit/level3).
