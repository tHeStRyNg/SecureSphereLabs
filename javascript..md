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
