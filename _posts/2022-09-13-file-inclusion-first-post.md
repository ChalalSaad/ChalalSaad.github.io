---
title: file inclusion :directory traversal
date: 12,sep 2022 22:40 PM
categories : [Penetration Tester, Web Hacking ,file inclusion]
tags: [web hacking , file inclusion ]
---
# File Inclusion

Many web application  allow the user to get access into files streams or allows the user to upload files on the server . So other bad guys use this weakness for doing bad thing in the server like see some secret file or execute a malicious file.

---

![my_image](/assets/lib/img/3.png)


# Directory traversal
i will start by what directory traversal is, describe how to carry out path traversal attacks and circumvent common obstacles

![](/assets/lib/img/2.png)

## other case 
If an application requires that the user-supplied filename must end with an expected file extension, such as .png, then it might be possible to use a null byte to effectively terminate the file path before the required extension. For example:

```
filename=../../../etc/passwd%00.png
```
various non-standart encodings (Adversaries may encode data with a non-standard data encoding system to make the content of command and control traffic more difficult to detect.)==> by pass input filter

[Data Encoding: Non-Standard Encoding ](https://attack.mitre.org/techniques/T1132/002/)


so the solution is using a null byte to effectively terminate the file path before the required extension. 
