<!-- TOC -->

- [常用命令](#%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)
- [重要概念](#%E9%87%8D%E8%A6%81%E6%A6%82%E5%BF%B5)
- [重点理解](#%E9%87%8D%E7%82%B9%E7%90%86%E8%A7%A3)
- [问题总结](#%E9%97%AE%E9%A2%98%E6%80%BB%E7%BB%93)
- [参考链接](#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5)

<!-- /TOC -->

> [其他版本-详细](https://github.com/CyC2018/CS-Notes/blob/master/notes/Git.md)

### 常用命令

```shell
#连接GitHub
git config --global user.name "Your Name"
git config --global user.email "email@example.com"
git config -l
git version

#新建工作区
git init
#工作区中文件的状态
git status
#将工作区中的文件全部存入暂存区
git add .
#将暂存区的文件存入分支，形成一个版本
git commit -m "版本描述信息"

#关联远程仓库
git remote add "标识名" "远程仓库地址"
#查看关联的远程仓库
git remote -v
#把本地main分支上记录的所有版本推送到远程仓库
git push "标识名" main
#远程仓库复制到本地，并自动形成一个本地仓库
git clone "远程仓库地址"
#增量更新文件
git pull "标识名" main

#查看当前仓库所有分支，仓库中默认只有main分支
git branch
#新建分支
git branch "分支名"
#切换分支，默认分支是main分支
git checkout dev
#简易日志，去掉oneline是全日志
git log --oneline

#快速合并和三方合并
git merge "分支名"
#简易图示
git log --oneline --graph

```

### 重要概念

---

> * 工作区：执行 **git init** 的目录即为工作区【不包含 **.git** 目录】，所有文件都首先在工作区新建，然后可以存入仓库(版本库)
> * 暂存区：版本库中包含一个临时区域，在**.git** 目录内，保存下一步要提交的文件， 工作区的文件进入仓库时，要先进入暂存区
> * 版本库：工作区中有一个隐藏目录 `.git`，这个目录不属于工作区，而是git的 `版本库`，是git管理的所有内容 
> * 分支：是一个个版本最终存储的位置，版本库中包含若干分支，提交的文件存储在分支中

---



### 重点理解

---

> - 本地仓库和远程仓库
> - GitHub和Gitee是Git服务器，可在Git服务器构建远程仓库
> - 执行 **git commit** 时，默认是在main分支上保存版本
> - 每一次 **git commit** 就是一个版本
> - 两个分支进行合并，但它们含有对同一个文件的修改，则在合并时出现冲突，git无法决断该保留改文件哪个分支的修改
> - 快速合并和三方合并

---



### 问题总结

> Q：在使用https协议做push时，如果曾经使用过Gitee或者Github，密码有过改动报错。
>
> A：**凭据管理器** 删除对应凭证，再次使用时会提示重新输入密码。



### 参考链接

> [视频教程](https://www.bilibili.com/video/BV1Mf4y117f3)
>
> [课件资源](https://pan.baidu.com/s/18MmB-z8S6VU1qNHNrGtQnQ)
