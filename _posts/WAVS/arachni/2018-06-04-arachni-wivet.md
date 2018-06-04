---
layout: post
title: "Arachni Tutorial - Run Arachni on WIVET"
author: Rana Khalil
categories: [arachni, wivet]
description: A tutorial that explains how to run Arachni on the WIVET application and lists the crawling coverage obtained by Arachni.
fullview: true
permalink: /_posts/WAVS/arachni/arachni_wivet
---

In this tutorial, we'll run a scan with the default Arachni configuration on the [WIVET](https://github.com/bedirhan/wivet) application to determine the crawling coverage of the Arachni scanner. 

Prerequisites: Run the WIVET application ([covered here](/_posts/WAVS/wivet)). For this tutorial, the WIVET application is run on 192.168.0.18 port 8090 and [Arachni](http://www.arachni-scanner.com/) version 1.5.1-0.5.12 is used.

The topics covered are:
- Scanner Configuration
- WIVET Result


## Scanner Configuration
The following script (arachni-wivet-script.sh) is used to run Arachni on the WIVET application.

```*
#!bin
./arachni http://192.168.0.18:8090/ --checks trainer --audit-links --audit-forms \
--scope-include-pattern 'http://192.168.0.18:8090/' \
--scope-exclude-pattern 'http://192.168.0.18:8090/offscanpages.*' \
--scope-exclude-pattern 'http://192.168.0.18:8090/logout.php' \
--scope-exclude-pattern 'http://192.168.0.18:8090/pages/100.php' \
--http-cookie-string="PHPSESSID=77d4ad6bbe505bba989152390e4e9e25" \
--report-save-path=wivet-arachni-report.afr
```

- Line 1 uses the check Trainer to poke and prope all inputs on the given URL in order to uncover new input vectors. In other words it is used to crawl the application. 
- Line 2 restricts the scope of the scan to URLs that contain the given URL. 
- Lines 3 to 5 exclude the given URLs from being scanned. We added the "offscanpages" link so that the scanner does not scan the off scan pages which are the "Statistics", "Current Run" and "About" pages. Similarly, we added the "logout" and "100" links so that the scanner does not click on the logout link and logout/exit from the application before the scan is done. 
- Line 6 passes the “PHPSESSD” session cookie to Arachni so that a single session is maintained across the scan.
- Line 7 is used to set the path for the outputted report.

To run the script, fire up the terminal, navigate to where the script is saved and run the following command:

```*
./arachni_reporter wivet-arachni-report.afr --reporter=html:outfile=wivet-arachni-report.html.zip
```

For this specific application, we are not interested in the vulnerability count. Instead, we're interested in the crawling coverage of the scanner which is automatically calculated by the WIVET application. In order to view the crawling coverage in the WIVET application, click on the Current Run link on the left menu. As can be seen in the below image, the Arachni scanner achieves a score of 94%.

<center><img src="/images/blogs/arachni/arachni-wivet.png" width="70%" height="70%" style="border: 2px solid black"/></center><br>

## WIVET Result
Arachni scores a crawling coverage of 94%, which is still pretty high compared to [ZAP](/_posts/WAVS/ZAP/zap_wivet), [Wapiti](/_posts/WAVS/wapiti/wapiti_wivet) and [Vega](/_posts/WAVS/vega/vega_wivet)!