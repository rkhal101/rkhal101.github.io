---
layout: page
title: OverTheWire Waregames Bandit Level 5 Writeup
permalink: /writeups/wargames/bandit/level5
---

# [Bandit Level 4 -> Level 5](http://overthewire.org/wargames/bandit/bandit5.html)

## Level Goal: 

> The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

## Write-up: 

First, navigate to the ```inhere``` directory. 

```shell
cd inhere
```

Second, loop through all the files in the directory and check which file is human-readable/ascii using the '''file''' command.

```shell
for i in $(ls); do file -i "./$i"; done;
```

The output will display that all the files are binary except for ```./-file07: text/plain; charset=us-ascii```. Display the contents of the file.

```shell
cat ./-file07
```

The output will display the password to log into bandit6.

```shell
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```

SSH into bandit5 using the discovered password to complete the next level.

```shell
ssh bandit5@bandit.labs.overthewire.org -p 2220
```

<!--Proceed to the next level write-up.-->
