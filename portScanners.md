#### NMAP
https://nmap.org/

Install
```apt-get install nmap -y```

Example
```nmap -A -sS -sV -Pn <HOST> ```

Slow Down Port Scan

```nmap -A -sS -sV -Pn -T[1-5] <HOST>```
