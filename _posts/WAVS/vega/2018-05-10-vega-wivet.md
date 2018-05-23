---
layout: post
title: "Vega Tutorial - Run Vega on WIVET Application"
author: Rana Khalil
categories: [vega, wivet]
description: A tutorial that explains how to run Vega on the WIVET application and lists the crawling coverage obtained by Vega.
fullview: true
permalink: /_posts/WAVS/vega/vega_wivet
---

Prerequisites: Run the WIVET application (Refer to this [tutorial](/_posts/WAVS/wivet)). For this tutorial, we'll be using the Firefox browser and running the WIVET application on localhost port 8090.

The topics covered are:
- Run Scan
- WIVET Results

## Run Scan
Click on Scan on the top menu in Vega > select Start New Scan. In the Select a Scan Target window, select the option Choose a target scope for scan and click on the Edit Scopes button. Under the Base Path option add the following URL:

```*
http://127.0.0.1:8090/
```

Under the Exclude (URL or pattern) option add the following URLs:
```*
http://127.0.0.1:8090/offscanpages.*
http://127.0.0.1:8090/logout.php
http://127.0.0.1:8090/pages/100.php
```

<center><img src="/images/blogs/vega/wivet-scope.png" width="60%" height="60%" style="border: 2px solid black"/></center><br>

Click OK and then click Next. You will be presented with a Select Modules window. Keep the default selected modules with the exception that the option "Bash Environment Variable Blind OS Injection..." under Injection modules should be unselected. After trial and error, we noticed that this option starts a new session (Even if a cookie is set in the Authentication option) and does not add to the crawling coverage on WIVET and therefore we opted to not include it. 

<center><img src="/images/blogs/vega/not-included.png" width="60%" height="60%" style="border: 2px solid black"/></center><br>

Click Next. In the Authentication Options window, we need to add the session cookie used by the WIVET application. To get to the session cookie, visit the url of the application on your browser (we will be using Firefox) and right click and select Inspect Element. Click on the Network tab > click on the Reload button if you can't see any requests > click on one of the requests. This should open a side menu. Click on the Cookies option in the side menu.

<center><img src="/images/blogs/vega/wivet-cookie-vega.png" width="80%" height="80%" style="border: 2px solid black"/></center><br>

Add the above cookie under the Set-Cookie or Set-Cookie2 value option in Vega. 

<center><img src="/images/blogs/vega/cookie-vega.png" width="60%" height="60%" style="border: 2px solid black"/></center><br>

Click Next > click Finish.

## WIVET Results
Once the scan is over, click on the Current Run option in WIVET.

<center><img src="/images/blogs/vega/vega-wivet.png" width="60%" height="60%" style="border: 2px solid black"/></center><br>

As can be seen in the above figure, Vega scores a crawling coverage of 14% (much lower than [ZAP](/_posts/WAVS/ZAP/zap_wivet) and [Wapiti](/_posts/WAVS/wapiti/wapiti_wivet)), which is pretty low! One thing to note is the test was done under the default settings. If Vega is configured properly it is possible that it can acheive a score of [50%](http://sectoolmarket.com/price-and-feature-comparison-of-web-application-scanners-unified-list.html). Considering that there is a huge improvement that comes with configuration, this should shed some light on users that trust the default configuration when performing their tests. A lower crawling coverage means a lower chance of finding and exploiting vulnerabilities! 

