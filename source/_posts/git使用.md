---
title: git使用
type: categories
date: 2021-03-19 10:31:54
categories: 
- git
tags:
- init

---

### create a new repository on the command line

```shell
echo "# extodb" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/hotwa/extodb.git
git push -u origin main
```



### push an existing repository from the command line

```shell
git remote add origin https://github.com/hotwa/extodb.git
git branch -M main
git push -u origin main
```





