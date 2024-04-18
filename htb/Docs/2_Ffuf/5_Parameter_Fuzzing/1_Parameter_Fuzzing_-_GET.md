### Parameter Fuzzing - GET

If we run a recursive ```ffuf``` scan on ```admin.academy.htb```, we should find ```http://admin.academy.htb:PORT/admin/admin.php```. 

If we try accessing this page, we see the following:

![image](https://github.com/tHeStRyNg/SecureSphereLabs/assets/118682909/a5e5b383-0ded-4278-a7e9-c83164499c6e)

That indicates that there must be something that identifies users to verify whether they have access to read the flag. 

We did not login, nor do we have any cookie that can be verified at the backend. 

So, perhaps there is a key that we can pass to the page to read the flag. 

Such keys would usually be passed as a parameter, using either a ```GET``` or a ```POST HTTP request```. 

This section will discuss how to fuzz for such parameters until we identify a parameter that can be accepted by the page.

``` Tip: Fuzzing parameters may expose unpublished parameters that are publicly accessible. Such parameters tend to be less tested and less secured, so it is important to test such parameters for the web vulnerabilities we discuss in other modules.   ```

#### GET Request Fuzzing

Similarly to how we have been fuzzing various parts of a website, we will use ffuf to enumerate parameters. 

Let us first start with fuzzing for ```GET``` requests, which are usually passed right after the URL, with a ```?``` symbol, like:

```http://admin.academy.htb:PORT/admin/admin.php?param1=key```.

So, all we have to do is replace ```param1``` in the example above with ```FUZZ``` and rerun our scan. 

Before we can start, however, we must pick an appropriate wordlist. 

Once again, ```SecLists``` has just that in ```/opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt```. 

With that, we can run our scan.

``` Once again, we will get many results back, so we will filter out the default response size we are getting. ```

```
tHeStRyNg@htb[/htb]$ ffuf -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key -fs xxx


        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.1.0-git
________________________________________________

 :: Method           : GET
 :: URL              : http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key
 :: Wordlist         : FUZZ: /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 40
 :: Matcher          : Response status: 200,204,301,302,307,401,403
 :: Filter           : Response size: xxx
________________________________________________

<...SNIP...>                    [Status: xxx, Size: xxx, Words: xxx, Lines: xxx]
```

We do get a hit back. Let us try to visit the page and add this ```GET``` parameter, and see whether we can read the flag now:

![image](https://github.com/tHeStRyNg/SecureSphereLabs/assets/118682909/916017e3-3809-410e-ba16-710618aa2ce7)

As we can see, the only hit we got back has been ```deprecated``` and appears to be no longer in use.
