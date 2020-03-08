Do Not Stop
=====

## Category: Networking

> "One of my servers was compromised, but I can't figure it out. See if you can solve it for me!"

# Methodology
First thing I did was open the PCAP up in wireshark to see any strange traffic. Everything looked relatively normal except for one thing: I spotted DNS traffic querying for a domain name that was base 64 encoded. I quickly decoded the string and found that the string was actually a command. The DNS reply also had base64 encoded traffic, which ended up being the output of the command.

> ls -la

> total 2512
 
> drwxr-xr-x    1 root     root          4096 Mar  6 04:44 .

> drwxr-xr-x    1 root     root          4096 Mar  6 08:09 ..

> -rw-r--r--    1 root     root         12288 Mar  6 04:42 .Makefile.swp

> -rw-r--r--    1 root     root           104 Mar  5 23:50 Dockerfile

> -rw-r--r--    1 root     root           119 Mar  5 23:50 Makefile

> -rw-r--r--    1 root     root            28 Mar  5 23:50 flag.txt

> -rwxr-xr-x    1 root     root       2533823 Mar  6 04:44 server

> -rw-r--r--    1 root     root          1693 Mar  5 23:50 server.go
