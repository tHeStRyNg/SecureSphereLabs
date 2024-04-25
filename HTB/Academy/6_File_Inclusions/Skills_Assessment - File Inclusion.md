### Skills Assessment - File Inclusion
#### Scenario
The company INLANEFREIGHT has contracted you to perform a web application assessment against one of their public-facing websites. They have been through many assessments in the past but have added some new functionality in a hurry and are particularly concerned about file inclusion/path traversal vulnerabilities.

They provided a target IP address and no further information about their website. Perform a full assessment of the web application checking for file inclusion and path traversal vulnerabilities.

Find the vulnerabilities and submit a final flag using the skills we covered in the module sections to complete this module.

Don't forget to think outside the box!

Target -->> Assess the web application and use a variety of techniques to gain remote code execution and find a flag in the / root directory of the file system. 
            Submit the contents of the flag as your answer.

#### Recon
##### Enumeration

* Target -- 94.237.62.195


#### NMAP - Network Enumeration
```
nmap -sC -sV -p- -Pn 94.237.62.195 -oN nmap/94.237.62.195.nmap -T4 -v

Discovered open port 54509/tcp on 94.237.62.195
PORT      STATE SERVICE VERSION
54509/tcp open  http    nginx 1.18.0
|_http-title: InlaneFreight
| http-methods: 
|_  Supported Methods: GET HEAD POST
|_http-server-header: nginx/1.18.0

Discovered open port 8080/tcp on 94.237.62.195
PORT     STATE    SERVICE    VERSION
8080/tcp filtered http-proxy

Discovered open port 25/tcp on 94.237.62.195
PORT   STATE SERVICE VERSION
25/tcp open  smtp?
| fingerprint-strings: 
|   GenericLines, GetRequest, HTTPOptions, Hello, Help, NULL, RTSPRequest: 
|     554-as8758.net SMTPBLOCKER ESMTP Service not available
|     554-No SMTP service
|     554-Sending on port 25 not allowed, use port 587
|_    clarification visit https://wiki.iway.ch/kb/wiki/Internet_Access/Sperrung_Port_25_(SMTP)
|_smtp-commands: SMTP EHLO 94-237-62-195.uk-lon1.upcloud.host: failed to receive data: connection closed
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :

Discovered open port 22/tcp on 94.237.62.195
Discovered open port 52269/tcp on 94.237.62.195
PORT      STATE    SERVICE VERSION
52269/tcp filtered unknown

Discovered open port 46104/tcp on 94.237.62.195
Discovered open port 46452/tcp on 94.237.62.195
Discovered open port 59007/tcp on 94.237.62.195
Discovered open port 37675/tcp on 94.237.62.195
Discovered open port 45305/tcp on 94.237.62.195
Discovered open port 59492/tcp on 94.237.62.195
Discovered open port 30074/tcp on 94.237.62.195
Discovered open port 40526/tcp on 94.237.62.195
Discovered open port 48359/tcp on 94.237.62.195
Discovered open port 33071/tcp on 94.237.62.195
Discovered open port 32676/tcp on 94.237.62.195
Discovered open port 42781/tcp on 94.237.62.195
Discovered open port 50085/tcp on 94.237.62.195
Discovered open port 38712/tcp on 94.237.62.195
Discovered open port 38393/tcp on 94.237.62.195
Discovered open port 48911/tcp on 94.237.62.195
Discovered open port 33677/tcp on 94.237.62.195
Discovered open port 38517/tcp on 94.237.62.195
Discovered open port 55177/tcp on 94.237.62.195
Discovered open port 35641/tcp on 94.237.62.195
Discovered open port 51427/tcp on 94.237.62.195
Discovered open port 39106/tcp on 94.237.62.195
Discovered open port 51868/tcp on 94.237.62.195
Discovered open port 31075/tcp on 94.237.62.195
Discovered open port 32054/tcp on 94.237.62.195
Discovered open port 55074/tcp on 94.237.62.195
Discovered open port 35070/tcp on 94.237.62.195

```







#### Enumeration
```
└──╼ [★]# ffuf -w /opt/repos/SecLists/Discovery/Web-Content/raft-large-directories.txt:FKK -u 'http://94.237.62.195:54509/FKK' -fs 15829

        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://94.237.62.195:54509/FKK
 :: Wordlist         : FKK: /opt/repos/SecLists/Discovery/Web-Content/raft-large-directories.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 15829
________________________________________________

images                  [Status: 301, Size: 169, Words: 5, Lines: 8, Duration: 36ms]
js                      [Status: 301, Size: 169, Words: 5, Lines: 8, Duration: 48ms]
css                     [Status: 301, Size: 169, Words: 5, Lines: 8, Duration: 53ms]
fonts                   [Status: 301, Size: 169, Words: 5, Lines: 8, Duration: 24ms]

```

##### Notes
* The webserver is on 54509 and seems to redirect to 8080 so seems nginx sservice an app on 8080 using proxy rewrite to 54509
* interesting directories found so far:

```
images                  [Status: 301, Size: 169, Words: 5, Lines: 8, Duration: 36ms]
js                      [Status: 301, Size: 169, Words: 5, Lines: 8, Duration: 48ms]
css                     [Status: 301, Size: 169, Words: 5, Lines: 8, Duration: 53ms]
fonts                   [Status: 301, Size: 169, Words: 5, Lines: 8, Duration: 24ms]
```
