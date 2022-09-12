---
title: file inclusion :directory traversal
date: 12,sep 2022 22:40 PM
categories : [Penetration Tester, Web Hacking ,file inclusion]
tags: [web hacking , file inclusion ]
---
# File Inclusion

Many web application  allow the user to get access into files streams or allows the user to upload files on the server . So other bad guys use this weakness for doing bad thing in the server like see some secret file or execute a malicious file.

---

![my_image](https://beaglesecurity.com/blog/images/File_inclusion_banner_840.png)

# how hacker discover  this vulnerabilities
the easiest way to see if an application is vulnerable to this type of attack is by simply determining if a URL uses a GET query. A GET request contains the parameters directly in the URL and would look something like this:

```url 
http://examplesite.com/?file=index.php
```

the website trust all his files  ?para=file.html , so the hacker try to spoof to access on the web server

# Directory traversal
i will start by what directory traversal is, describe how to carry out path traversal attacks and circumvent common obstacles

![](https://i0.wp.com/1.bp.blogspot.com/-ZppdtF_CDOM/XxIoq9FHL9I/AAAAAAAAl9s/UnmqgFoccsYDXagEHcOJ_IE17WipVVOZACLcBGAsYHQ/s1600/2.png?w=640&ssl=1)

# What is directory traversal
directory traversal is a web security vulnerability that make us as a hacker to read any file in the web server (include application code and data, credentials for back-end systems, and sensitive operating system files)

# Climbing the Directory
By appending ../ directly to the file path in the URL, we can attempt to change into higher directories in an effort to view system files and information not meant to be internet-facing.

```url 
http://examplesite.com/?file=../../../../etc/passwd
```
After climbing a few more levels, we finally hit paydirt and the contents of /etc/passwd are displayed to us right in the browser:

![](https://img.wonderhowto.com/img/original/76/70/63665863341306/0/636658633413067670.jpg)

## other case 
If an application requires that the user-supplied filename must end with an expected file extension, such as .png, then it might be possible to use a null byte to effectively terminate the file path before the required extension. For example:

```url
filename=../../../etc/passwd%00.png
```
various non-standart encodings (Adversaries may encode data with a non-standard data encoding system to make the content of command and control traffic more difficult to detect) by pass input filter
[Data Encoding: Non-Standard Encoding ](https://attack.mitre.org/techniques/T1132/002/).

so the solution is using a null byte to effectively terminate the file path before the required extension. 



