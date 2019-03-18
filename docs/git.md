---
title: Git
---

# Git

--------------------------------------------------------------------------------

## 生成公钥

````
```bash
ssh-keygen -t rsa -C "shineniefei@qq.com"
```
一路Enter~别输入内容（默认密码空，默认用户位置）
````

## 查看公钥

````
```bash
# 查看公钥，屏幕打印出来的内容
cat ~/.ssh/id_rsa.pub
```
````

## 将公钥添加到git

1. 复制查看到的公钥
2. 登录网页版，点击Settings - SSH and GPG keys - New SSH key,新建公钥,粘贴，保存
3. 测试是否联通

  ```bash
  ssh -T git@github.com
  ```

## 本地配置用户

````
```bash
git config --global user.email "shineniefei@qq.com"
git config --global user.name "shineniefei"
```
````

## 克隆项目clone

1. 登录网页版，进入项目的首页，选择ssh方式 git@git.oschina.shineniefei/bccnui.git
2. 进入本地工作目录

  ```bash
  # clone 项目
  git clone git@git.oschina.shineniefei/bccnui.git
  # 从远程获取最新版本到本地
  git pull origin master
  ```

## 本地仓库关联远程库

1. 登录网页版，进入项目的首页，选择ssh方式 git@git.oschina.shineniefei/bccnui.git
2. 进入本地工作目录

  ```bash
  # 本地仓库关联远程库,远程库的名字就是origin。
  git remote add origin git@git.oschina.shineniefei/bccnui.git
  # 从远程的origin的master主分支下载最新的版本到origin/master分支上,fetch会自动merge
  git fetch origin master
  # 比较本地的master分支和origin/master分支的差别
  git log -p master..origin/master
  # 进行合并
  git merge origin/master
  ```

  _上述过程其实可以用以下更清晰的方式来进行：_

  ```bash
  #从远程获取最新的版本到本地的tem分支上,之后再进行比较合并
  git fetch origin master:tmp
  git diff tmp
  git merge tmp
  ```

## 本地创建一个版本库

````
```bash
# 新建项目目录
mkdir exemple
# 切换目录
cd exemple
# 初始化GIT仓库
git init
# 加入文件到仓库
git add README.md
# 提交暂存带注释
git commit -m "说明"
```
````

## git命令

### pull

````
```bash
# 从远程获取最新版本并merge到本地
git pull origin master
```
*上述命令其实相当于git fetch 和 git merge*  
*在实际使用中，git fetch更安全一些*  
*因为在merge前，我们可以查看更新情况，然后再决定是否合并*
````

### push

````
```bash
# 本地库的所有内容推送到远程库,u选项会指定一个默认主机
git push -u origin master
# 本地库的所有内容推送到远程库
git push origin master
# 默认只推送当前分支
git push
```
````

### log

````
```bash
# 查看提交日志
git log
# 以一行显示日志
git log --pretty=oneline
# 查看分支合并图
git log --graph
```
````

### reset

````
```bash
# 退回上一版本
git reset --hard HEAD^
# 退回上上版本
git reset --hard HEAD^^
# 退回10个版本
git reset --hard HEAD~10
# 指定到某个xxx版本
git reset --hard xxx
# 撤销（unstage）暂存区
git reset HEAD readme.txt
```
````

### reflog

````
```bash
# 用来记录你的每一次命令
git reflog
```
````

### status

````
```bash
# 查看仓库状态，查看冲突
git status
```
````

### rm

````
```bash
# 删除文件
git rm readme.txt
# 提交删除的内容
git commit -m "删除readme.txt"
```
````

### checkout

````
```bash
# 撤销add和commit的内容
# 恢复删除的内容
git checkout -- readme.txt
# 创建dev分支，然后切换到dev分支：
git checkout -b dev
# 切换回master分支
git checkout master
```
````

_git checkout -b参数表示创建并切换，相当于以下两条命令：_<br>
_git branch dev_<br>
_git checkout dev_

### branch

````
```bash
# 查看当前分支
git branch
# 创建分支
git branch <name>
# 删除分支
git branch -d <name>
```
````

### merge

````
```bash
# 合并dev分支内容到当前分支
git merge dev
```
````

## remote

````
```bash
# 删除远程 Git 仓库
git remote rm origin
```
````
