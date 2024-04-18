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

![image](https://github.com/tHeStRyNg/SecureSphereLabs/assets/118682909/20f34bf9-ea60-4c65-aa7d-a2b02f05c89e)

We see that we do get a few hits back. Now, we can try running the same thing on ```academy.htb``` and see if we get any hits back:

![image](https://github.com/tHeStRyNg/SecureSphereLabs/assets/118682909/1eac6787-21e9-4741-b7b1-cb65ed8d61d5)

We see that we do not get any hits back. Does this mean that there are no sub-domain under ```academy.htb```? - Noooooo.

This means that there are no public sub-domains under academy.htb, as it does not have a public DNS record, as previously mentioned. 

Even though we did add ```academy.htb``` to our ```/etc/hosts``` file, we only added the main domain, so when ffuf is looking for other sub-domains, it will not find them in ```/etc/hosts```, and will ask the public DNS, which obviously will not have them.

#### Questions

Try running a sub-domain fuzzing test on 'inlanefreight.com' to find a customer sub-domain portal. What is the full domain of it?

