### Value Fuzzing
After fuzzing a working parameter, we now have to fuzz the correct value that would return the flag content we need. 

This section will discuss fuzzing for parameter values, which should be fairly similar to fuzzing for parameters, once we develop our wordlist.

#### Custom Wordlist
When it comes to fuzzing parameter values, we may not always find a pre-made wordlist that would work for us, as each parameter would expect a certain type of value.

For some parameters, like usernames, we can find a pre-made wordlist for potential usernames, or we may create our own based on users that may potentially be using the website.

For such cases, we can look for various wordlists under the seclists directory and try to find one that may contain values matching the parameter we are targeting. 

In other cases, like custom parameters, we may have to develop our own wordlist. 

In this case, we can guess that the id parameter can accept a number input of some sort. 

These ids can be in a custom format, or can be sequential, like from 1-1000 or 1-1000000, and so on. 

We'll start with a wordlist containing all numbers from 1-1000.

There are many ways to create this wordlist, from manually typing the IDs in a file, or scripting it using Bash or Python. 

The simplest way is to use the following command in Bash that writes all numbers from 1-1000 to a file:

```
tHeStRyNg@htb[/htb]$ for i in $(seq 1 1000); do echo $i >> ids.txt; done
```

Once we run our command, we should have our wordlist ready:

```
tHeStRyNg@htb[/htb]$ cat ids.txt

1
2
3
4
5
6
<...SNIP...>
```

Now we can move on to fuzzing for values.

#### Value Fuzzing

Our command should be fairly similar to the POST command we used to fuzz for parameters, but our FUZZ keyword should be put where the parameter value would be, and we will use the ```ids.txt``` wordlist we just created, as follows:

```
tHeStRyNg@htb[/htb]$ ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx


        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v1.0.2
________________________________________________

 :: Method           : POST
 :: URL              : http://admin.academy.htb:30794/admin/admin.php
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : id=FUZZ
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
 :: Filter           : Response size: xxx
________________________________________________

<...SNIP...>                      [Status: xxx, Size: xxx, Words: xxx, Lines: xxx]
```

We see that we get a hit right away. We can finally send another ```POST request``` using ```curl```, as we did in the previous section, use the ```id value``` we just found, and collect the flag.

#### Questions

Try to create the 'ids.txt' wordlist, identify the accepted value with a fuzzing scan, and then use it in a 'POST' request with 'curl' to collect the flag. What is the content of the flag?

##### Custom Wordlist

First we create our own wordlist which is a basic for loop from 0 to 1000 as followws:
```for i in $(seq 1 1000); do echo $i >> ids.txt; done ```

We confirm we have the file generated:

```

```

##### Value Fuzzing
* 1st we get teh fs value for the id
```
root@cloud1:/opt/repos/SecLists/Discovery/Web-Content# ffuf -w burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:35826/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded'|head

        /'___\  /'___\           /'___\
       /\ \__/ /\ \__/  __  __  /\ \__/
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/
         \ \_\   \ \_\  \ \____/  \ \_\
          \/_/    \/_/   \/___/    \/_/

       v2.1.0-dev
________________________________________________

 :: Method           : POST
 :: URL              : http://admin.academy.htb:35826/admin/admin.php
 :: Wordlist         : FUZZ: /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt
 :: Header           : Content-Type: application/x-www-form-urlencoded
 :: Data             : FUZZ=key
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200-299,301,302,307,401,403,405,500
________________________________________________

11                      [Status: 200, Size: 798, Words: 227, Lines: 54, Duration: 17ms]
1                       [Status: 200, Size: 798, Words: 227, Lines: 54, Duration: 17ms]
A                       [Status: 200, Size: 798, Words: 227, Lines: 54, Duration: 18ms]
4                       [Status: 200, Size: 798, Words: 227, Lines: 54, Duration: 18ms]
21                      [Status: 200, Size: 798, Words: 227, Lines: 54, Duration: 17ms]
AMOUNT                  [Status: 200, Size: 798, Words: 227, Lines: 54, Duration: 17ms]
2                       [Status: 200, Size: 798, Words: 227, Lines: 54, Duration: 18ms]
Address                 [Status: 200, Size: 798, Words: 227, Lines: 54, Duration: 18ms]
22                      [Status: 200, Size: 798, Words: 227, Lines: 54, Duration: 19ms]
ACCESSLEVEL             [Status: 200, Size: 798, Words: 227, Lines: 54, Duration: 19ms]
:: Progress: [48/6453] :: Job [1/1] :: 0 req/sec :: Duration: [0:00:00] :: Errors: 0 
```

* 2nd We use the Obtained ID from our for loop to try the one that works as follows:
```
root@cloud1:/opt/repos/SecLists/Discovery/Web-Content# curl http://admin.academy.htb:35826/admin/admin.php -X POST -d 'id=73' -H 'Content-Type: application/x-www-form-urlencoded'
<div class='center'><p>HTB{pXXXXXXXXXXXXXXXXXXXXXX}</p></div>
<html>
<!DOCTYPE html>

<head>
  <title>HTB Academy</title>
  <style>

```
And we capture the FLAG ^_^
