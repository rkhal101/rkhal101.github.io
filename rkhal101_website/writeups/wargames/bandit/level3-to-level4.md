---
layout: page
title: OverTheWire Waregames Bandit Level 4 Writeup
permalink: /writeups/wargames/bandit/level4
---

# [Bandit Level 3 -> Level 4](http://overthewire.org/wargames/bandit/bandit4.html)

## Level Goal: 

> The password for the next level is stored in a hidden file in the inhere directory.

## Write-up: 
First, verify that the file is located in the ```inhere``` directory:

```shell
cd inhere
ls -a
```

The output shows that a ```.hidden``` file exists in the ```inhere``` directory.

Second, display the contents of the file. 

```shell
cat .hidden 
```

The output will display the password to log into bandit4.

```shell
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

SSH into bandit4 using the discovered password to complete the next level.

```shell
ssh bandit4@bandit.labs.overthewire.org -p 2220
```

Proceed to the [next level write-up](/writeups/wargames/bandit/level5).
