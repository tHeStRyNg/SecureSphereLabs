### Sub-domain Fuzzing

In this section, we will learn how to use ffuf to identify ```sub-domains``` (i.e., ```*.website.com```) for any website.

#### Sub-domains

A sub-domain is any website underlying another domain. For example, ```https://photos.google.com``` is the photos ```sub-domain``` of ```google.com```.

In this case, we are simply checking different websites to see if they exist by checking if they have a public DNS record that would redirect us to a working server IP. 

So, let's run a scan and see if we get any hits. Before we can start our scan, we need two things:

* A wordlist
* A target

Luckily for us, in the ```SecLists``` repo, there is a specific section for ```sub-domain wordlists```, consisting of common words usually used for sub-domains. 

We can find it in ```/opt/useful/SecLists/Discovery/DNS/```. 

In our case, we would be using a shorter wordlist, which is ```subdomains-top1million-5000.txt```. 

If we want to extend our scan, we can pick a larger list.

As for our target, we will use ```inlanefreight.com``` as our target and run our scan on it. 

Let us use ```ffuf``` and place the ```FUZZ``` keyword in the place of sub-domains, and see if we get any hits:

