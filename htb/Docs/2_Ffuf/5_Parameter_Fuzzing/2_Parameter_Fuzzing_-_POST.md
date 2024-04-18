### Parameter Fuzzing - POST

The main difference between ```POST requests``` and ```GET requests``` is that ```POST requests``` are not passed with the URL and cannot simply be appended after a ```?``` symbol. 

```POST``` requests are passed in the data field within the ```HTTP request```. 

Check out the Web Requests module to learn more about HTTP requests.

To fuzz the data field with ffuf, we can use the -d flag, as we saw previously in the output of ```ffuf -h```. We also have to add ```-X POST``` to send POST requests.

```
Tip: In PHP, "POST" data "content-type" can only accept "application/x-www-form-urlencoded". So, we can set that in "ffuf" with "-H 'Content-Type: application/x-www-form-urlencoded'".
```

So, let us repeat what we did earlier, but place our ```FUZZ``` keyword after the ```-d flag```:

![image](https://github.com/tHeStRyNg/SecureSphereLabs/assets/118682909/c6fc3837-e773-45b1-90f8-48b45cb64e35)

As we can see this time, we got a couple of hits, the same one we got when fuzzing GET and another parameter, which is ```id```. Let's see what we get if we send a ```POST request``` with the ```id parameter```. 

We can do that with curl, as follows:

![image](https://github.com/tHeStRyNg/SecureSphereLabs/assets/118682909/008b8dd8-26b2-44c4-9ec3-8e6ed94e6bc3)

As we can see, the message now says Invalid ```id```!.
