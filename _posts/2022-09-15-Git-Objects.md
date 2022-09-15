---
title: Git Objects
date: 15,sep 2022 
categories : [development,git]
tags: [development, git , repository,github ,managing system ,Unix,Lunix]
---
#  Git Objects
![global_pic_git_objects](/assets/global_git_object.png)

Git is a managing system the core of Git is a simple key-value data store , you can insert any kind of content into your repository , for which git will hand you back a unique key you can use later to read your content.
Is a definition from [git](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects) community. 

So actually **objects** is  where git stores its representation of all files, directories, and commits that's it.

if you want to know more deeply  stuff you can read [git](https://git-scm.com/book/en/v2/Git-Internals-Git-Objects) documention  , because in this post i will do a real example of git objects , 

---
## Types of git objects

If you have read documentation  git, you know that git stores different types of objects in .git/objects. The object types 
are:

- Blobs - Contain the contents of a file.
-  Trees - List the contents of a directory, connecting "blobs" with names and permissions to reference files and subdirectories.
-  Commits - Store a reference to a specific version of the code (a single tree), the direct parentage (parent commit hash(es)), and other metadata.


![second_global_git_object](/assets/other_global_git.png)


## practice  git objects 

The best way to practice git is to use it. Create a directory, add some files, make some changes, explore and answer any outstanding questions you might have thru hands on practice. This will help clear up things and help build muscle memory.
so in this post i will use my personal tool that i use it to practice my knowledge in git , really recommended
for us as beginners is : 
[git-katas](https://github.com/eficode-academy/git-katas)


![git-katas](/assets/git-katas.png)

---

1. the name of the folder that contains a exercise in object is :**investigation** ,open the README.md file to understand the object of this exercise and get started with your task:


```shell
$ cd inverstigation
$ ls
$ cat README.md
$ source setup.sh
```
![](/assets/git_object.note.png)


![](/assets/git_object2.png)

---
### find the objects 
in order to see objects in this repository **tree** is our friend.

```shell
$ tree -aC
```
- -a :  see all files, including the hidden ones
- -C :  color option

![](/assets/git_object3.png)

---
 this is our tree related to .git folder ,but most important folder here is actually the **objects** , so is contains some subfolders and some files ,  so what all those files mean ? 


 so we will try to grap the full file of object or  the full file name of object  , actually file contains a hash as you can see here, but full hash begins with sub name then the file name , so we will try actually to get the whole file name or full hash , so **find** command is our friend

```shell
$ find .git/objects -type f 
```

![](/assets/git_object4.png)


---
so we get i six files path but me as i told you, im interested in the subfolder name and file name , so we will try to use the [awk](https://www.geeksforgeeks.org/awk-command-unixlinux-examples/) command to get only what we want 


```shell
$ find .git/objects/ -type f | awk -F/ '{print $3$4}
```


![](/assets/git_object55.png)

---
so i get the full hash of the files object actually in this directory , so the first command that i'm going to use is actually to see the type of these object


```shell
$ git cat-file -t hash
```
![](/assets/git_object6.png)


---
or you can print to see the content of hash

```shell
$ git cat-file -p hash
```

![](/assets/git_object7.png)

---

we know that git is a  managing system that's mean he must help me to full managing my files , so when i use git i should feel power and fast.
sometimes you will have huge files in your repository  that's mean massive objects , so in this case you can't check the files one by one is , so this command line help you to get all the type or all the content of your object in one line fast (**DRY**) 


```shell
$ for i in $(find .git/objects -type f | awk -F/ '{print $3$4}'); git cat-file -t $i
```
