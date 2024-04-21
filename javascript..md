### Javascript

#### Examples of Inline JS and DOM manipulation

* DOM Manipulation XSS

``` <iframe src="javascript:alert(`xss`)"> ```
``` <iframe src="javascript:alert(`Hello World`)"> ```

* Javascript is a browser side scripting language that allows developers to manipulate, the contents of the page dinamically. 
* Inline JS allows every one to manipulate the contents of a webpage via the url bar Examples:
* Displays any cookies the site has placed in your browser

CODE :

``` java<b></b>script:alert(document.cookie) ```

* https://www.hackthissite.org/articles/read/405
* https://www.hackthissite.org/articles/read/906

#### Obfuscation

https://jsconsole.com/
https://www.toptal.com/developers/javascript-minifier
https://beautifytools.com/javascript-obfuscator.php
https://obfuscator.io/
https://matthewfl.com/unPacker.html
https://www.boxentriq.com/code-breaking/cipher-identifier

```
┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ curl -X POST http://94.237.49.166:51487/serial.php
N2gxNV8xNV9hX3MzY3IzN19tMzU1NGcz┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ echo "N2gxNV8xNV9hX3MzY3IzN19tMzU1NGcz"|base64 -d
7h15_15_a_s3cr37_m3554g3┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ curl -s http://94.237.57.59:38999/serial.php -X POST -d "serial=7h15_15_a_s3cr37_m3554g3"
HTB{ju57_4n07h3r_r4nd0m_53r14l}┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ curl -s http://83.136.253.251:34072/keys.php -X POST "null"
4150495f70336e5f37333537316e365f31355f66756e┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ echo "4150495f70336e5f37333537316e365f31355f66756e"|base64 -d
�^t��_�M���_߽�ߝ��^�߮_�]����┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ echo "4150495f70336e5f37333537316e365f31355f66756e"|base64 -d|xxr
bash: xxr: command not found
┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ echo "4150495f70336e5f37333537316e365f31355f66756e"|base64 -d|xxd
00000000: e35e 74e3 de5f ef4d f7e9 ee5f dfbd f7df  .^t.._.M..._....
00000010: 9dfb df5e 9edf ae5f df5d f9e5 feba ef9e  ...^..._.]......
00000020: 9e                                       .
┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ echo "4150495f70336e5f37333537316e365f31355f66756e"|xxd
00000000: 3431 3530 3439 3566 3730 3333 3665 3566  4150495f70336e5f
00000010: 3337 3333 3335 3337 3331 3665 3336 3566  37333537316e365f
00000020: 3331 3335 3566 3636 3735 3665 0a         31355f66756e.
┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ echo "4150495f70336e5f37333537316e365f31355f66756e"|xxd -d
00000000: 3431 3530 3439 3566 3730 3333 3665 3566  4150495f70336e5f
00000016: 3337 3333 3335 3337 3331 3665 3336 3566  37333537316e365f
00000032: 3331 3335 3566 3636 3735 3665 0a         31355f66756e.
┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ echo "4150495f70336e5f37333537316e365f31355f66756e"|xxd -p -r
API_p3n_73571n6_15_fun┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ curl -s http://83.136.253.251:34072/keys.php -X POST -d "key=API_p3n_73571n6_15_fun" 
HTB{r34dy_70_h4ck_my_w4y_1n_2_HTB}┌─[eu-academy-1]─[10.10.15.41]─[parrot@parrot]─[~]
└──╼ [★]$ 

```