### Proedures

#### Recon

##### NMAP

``` nmap -sC -sV -A -Pn -oA nmap/<fileOutput> <ipOrDomain> ```


##### VHOSTS - Domains
Add any domains found to /etc/hosts

##### Confirm target OS
Confirm target OS with ping /dcpdump and TTL and correlate with nmap discovery banner

* Linux/MAC OS – 64
* Windows – 128
* Cisco Routers – 255
* DNS – depends on the DNS resolver (can range from 128 to 86400)

```
# ping 10.129.181.116
PING 10.129.181.116 (10.129.181.116) 56(84) bytes of data.
64 bytes from 10.129.181.116: icmp_seq=1 ttl=63 time=7.63 ms
64 bytes from 10.129.181.116: icmp_seq=2 ttl=63 time=7.78 ms
64 bytes from 10.129.181.116: icmp_seq=3 ttl=63 time=7.76 ms
```

So this confirms the TTL 63 so Linux box

You can also use tcpdump as follows:

``` 
tcpdump -i tun0 -v -n ip src 10.129.181.116
```
then on another shell drop netat to 22 for example

```
nc -zv 10.129.181.116 22
```

And you should be able to only see the packets as follows below ```ttl 63```

```
root@cloud1:/opt/repos# tcpdump -i tun0 -v -n ip src 10.129.181.116
tcpdump: listening on tun0, link-type RAW (Raw IP), capture size 262144 bytes
11:05:26.008219 IP (tos 0x0, ttl 63, id 0, offset 0, flags [DF], proto TCP (6), length 60)
    10.129.181.116.22 > 10.10.15.41.46576: Flags [S.], cksum 0x9708 (correct), seq 1050554249, ack 1765552463, win 65160, options [mss 1357,sackOK,TS val 2162116772 ecr 2221788402,nop,wscale 7], length 0
11:05:26.019534 IP (tos 0x0, ttl 63, id 32497, offset 0, flags [DF], proto TCP (6), length 52)
    10.129.181.116.22 > 10.10.15.41.46576: Flags [.], cksum 0xc1e3 (correct), ack 2, win 510, options [nop,nop,TS val 2162116784 ecr 2221788410], length 0
11:05:26.073981 IP (tos 0x0, ttl 63, id 32498, offset 0, flags [DF], proto TCP (6), length 93)
    10.129.181.116.22 > 10.10.15.41.46576: Flags [P.], cksum 0x9d54 (correct), seq 1:42, ack 2, win 510, options [nop,nop,TS val 2162116838 ecr 2221788410], length 41
11:05:26.074296 IP (tos 0x0, ttl 63, id 32499, offset 0, flags [DF], proto TCP (6), length 52)
    10.129.181.116.22 > 10.10.15.41.46576: Flags [F.], cksum 0xc182 (correct), seq 42, ack 2, win 510, options [nop,nop,TS val 2162116839 ecr 2221788410], length 0
```

