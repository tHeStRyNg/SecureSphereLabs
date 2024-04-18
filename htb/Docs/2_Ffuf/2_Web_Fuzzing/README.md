### Web Fuzzing

We will start by learning the basics of using ffuf to fuzz websites for directories. We run the exercise in the question below, and visit the URL it gives us, and we see the following website:

![image](https://github.com/tHeStRyNg/SecureSphereLabs/assets/118682909/91239053-5526-4cad-9ffe-d6b30c6aee00)

The website has no links to anything else, nor does it give us any information that can lead us to more pages. So, it looks like our only option is to 'fuzz' the website.

### Fuzzing
The term fuzzing refers to a testing technique that sends various types of user input to a certain interface to study how it would react. 

If we were fuzzing for SQL injection vulnerabilities, we would be sending random special characters and seeing how the server would react. 

If we were fuzzing for a buffer overflow, we would be sending long strings and incrementing their length to see if and when the binary would break.

We usually utilize pre-defined wordlists of commonly used terms for each type of test for web fuzzing to see if the webserver would accept them. 

This is done because web servers do not usually provide a directory of all available links and domains (unless terribly configured), and so we would have to check for various links and see which ones return pages. For example, if we visit https://www.hackthebox.eu/doesnotexist, we would get an HTTP code 404 Page Not Found, and see the below page:
