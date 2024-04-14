## AV Engines
VirusTotal - ``` https://www.virustotal.com/gui/home/upload ```

![image](https://github.com/tHeStRyNg/SecureSphereLabs/assets/118682909/d04500c6-761e-4c0c-9942-ea2bef328f6e)

```
root@cloud1:/opt/sqlmap# curl -X POST https://www.virustotal.com/vtapi/v2/file/scan -F apikey=b5b24bcfc00757dc6d4e566207d51cf97f6e0ea34f6643475cf726475b9bdf29 -F file=@myn.exe
{"md5":"d3bb436495fa55c27609acfd8397235d","permalink":"f-5c9488072190679ef15825888b34e0486425991a451cb780e8cf1364f5bac200-1713051502","resource":"5c9488072190679ef15825888b34e0486425991a451cb780e8cf1364f5bac200","response_code":1,"scan_id":"5c9488072190679ef15825888b34e0486425991a451cb780e8cf1364f5bac200-1713051502","sha1":"6c5ac1b984a859d18b8955531b46e7459eca87cc","sha256":"5c9488072190679ef15825888b34e0486425991a451cb780e8cf1364f5bac200","verbose_msg":"Scan request successfully queued, come back later for the report"}
```
## Submit a file

```curl -X POST https://www.virustotal.com/vtapi/v2/file/scan -F apikey=b5b24bcfc00757dc6d4e566207d51cf97f6e0ea34f6643475cf726475b9bdf29 -F file=@myn.exe```

## Get the report on the above submission
```curl --request GET --url "https://www.virustotal.com/vtapi/v2/file/report?apikey=b5b24bcfc00757dc6d4e566207d51cf97f6e0ea34f6643475cf726475b9bdf29&scan_id=5c9488072190679ef15825888b34e0486425991a451cb780e8cf1364f5bac200-171305150&resource=5c9488072190679ef15825888b34e0486425991a451cb780e8cf1364f5bac200"```

### Response with report url:

```
{"md5":"d3bb436495fa55c27609acfd8397235d","permalink":"https://www.virustotal.com/gui/file/5c9488072190679ef15825888b34e0486425991a451cb780e8cf1364f5bac200/detection/f-5c9488072190679ef15825888b34e0486425991a451cb780e8cf1364f5bac200-1713051502","positives":57,"resource":"5c9488072190679ef15825888b34e0486425991a451cb780e8cf1364f5bac200","response_code":1,"scan_date":"2024-04-13 23:38:22","scan_id":"5c9488072190679ef15825888b34e0486425991a451cb780e8cf1364f5bac200-1713051502","scans":{"ALYac":{"detected":true,"result":"Trojan.CryptZ.Marte.1.Gen","update":"20240413","version":"2.0.0.10"},"APEX":{"detected":true,"result":"Malicious","update":"20240413","version":"6.521"},"AVG":{"detected":true,"result":"Win32:SwPatch [Wrm]","update":"20240413","version":"23.
```

### Buildig your own Antivirus based on Clamav Fork
* https://docs.clamav.net
* https://www.clamav.net/
* fork --> https://github.com/Cisco-Talos/clamav