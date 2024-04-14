### WebScanners

#### 1 - Nikto 
Description: nikto - ubuntu 20.x web vulerability scanner shell - 2024 version 2.1.5

Install --> ``` apt-get install nikto -y ```
Exec --> ```nikto -C all -h https://xfr.xyz```

#### 2 - Shodan
Description: Shodan gathers information about all devices directly connected to the Internet. If a device is directly hooked up to the Internet then Shodan queries it for various publicly-available information. The types of devices that are indexed can vary tremendously: ranging from small desktops up to nuclear power plants and everything in between.

Exec --> https://www.shodan.io


Install --> ```pip3 install -U --user shodan```

Install --> ```apt install python3-shodan```

setup API_KEY --> ```shodan init <API_KEY>```

search wordpress sites version 1.4.7 exploitable or linked to CVE (Common Vulnerabilities and Exposures) --> ```shodan count wordpress 1.4.7```

Output
`` 19 ``

then we grab all data from what was found to a json structured gz file --> ```shodan download wordpressFile wordpress 1.4.7```

Output
```Search query:                   wordpress 1.4.7```

```Total number of results:        19```

```Query credits left:             0```

```Output file:                    wordpressFile.json.gz```

Untar the file

```gunzip wordpressFile.json.gz```

Cat file and pass it to json beautifier or just use vscode but each line corresponds to data regarding each found host
With the particular vulnerability corresponding to wordpress 1.4.7