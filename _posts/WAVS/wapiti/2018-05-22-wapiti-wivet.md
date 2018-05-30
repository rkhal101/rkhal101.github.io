---
layout: post
title: "Wapiti Tutorial - Run Wapiti on WIVET"
author: Rana Khalil
categories: [wapiti, wivet]
description: A tutorial that explains how to run wapiti on the WIVET application and lists the crawling coverage obtained by wapiti.
fullview: true
permalink: /_posts/WAVS/wapiti/wapiti_wivet
---

In this tutorial, we'll run a scan with the default Wapiti configuration on the [WIVET](https://github.com/bedirhan/wivet) application to determine the crawling coverage of the Wapiti scanner. 

Prerequisites: Run the WIVET application ([covered here](/_posts/WAVS/wivet)). For this tutorial, the WIVET application is run on localhost port 8090 and [Wapiti](http://wapiti.sourceforge.net/) version 3.0.1 is used.

The topics covered are:
- Scanner Configuration
- WIVET Result


## Scanner Configuration
The following script (wapiti-wivet-script.sh) is used to run Wapiti against the WIVET application.

```*
#!bin
wapiti -u http://127.0.0.1:8090/ \
-x http://127.0.0.1:8090/logout.php \
-x http://127.0.0.1:8090/offscanpages.* \
-x http://127.0.0.1:8090/pages/100.php

```


The first line indicates the URL that will be used as a base for the scan. The remaining lines of code exclude the given URLs from being scanned. We added the "offscanpages" link so that the scanner does not scan the off scan pages which are the "Statistics", "Current Run" and "About" pages. Similarly, we added the "logout" and "100" links so that the scanner does not click on the logout link and logout/exit from the application before the scan is done. 

To run the script, fire up the terminal, navigate to where the script is saved and run the following command:

```*
bash wapiti-wivet-script.sh
```

Once the scan is finished, wapiti will output the location of the generated report as shown in the below figure:

<center><img src="/images/blogs/wapiti/wapiti-terminal-output.png" width="70%" height="70%" style="border: 2px solid black"/></center><br>

For this specific application, we are not interested in the vulnerability count. Instead, we're interested in the crawling coverage of the scanner which is automatically calculated by the WIVET application. In order to view the crawling coverage in the WIVET application, click on the Current Run link on the left menu. As can be seen in the below image, the Wapiti scanner achieves a score of 50%.

<center><img src="/images/blogs/wapiti/wapiti-wivet.png" width="70%" height="70%" style="border: 2px solid black"/></center><br>


## WIVET Result
Wapiti scores a crawling coverage of 50% (slightly better than [ZAP](/_posts/WAVS/ZAP/zap_wivet)), which is still pretty low! One thing to note is that the test was done under the default settings. It is possible that if the scanner is configured appropriately the crawling coverage might be significantly higher. 