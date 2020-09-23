## git提交常用命令

在当前目录新建一个Git代码库

git init

git add README.md
git commit -m "first commit"
git branch -M master
git remote add origin git@github.com:wwyjc/test.git
git push -u origin master

设置提交代码时的用户信息

```
$ git config [--global] user.name "[name]"
$ git config [--global] user.email "[email address]"
```

提交工作区自上次commit之后的变化，直接到仓库区

```
$ git commit -a
```

git删除远程仓库文件

```
git rm -r --cached a/2.txt //删除a目录下的2.txt文件  删除a目录git rm -r --cached a

git commit -m "删除a目录下的2.txt文件" 

git push
```

![img](https://images2015.cnblogs.com/blog/614638/201610/614638-20161031111156080-736554510.png)

## git常见错误

### 问题1

![img](https://img-blog.csdnimg.cn/20190611012953403.png)

第一句报错：
fatal: remote origin already exists.
远程起源已经存在。

第二句报错：
git@github.com: Permission denied (publickey).
fatal: Could not read from remote repository.
git@github.com：权限被拒绝（publickey）。
致命：无法从远程存储库读取。

第三句报错：
Please make sure you have the correct access rights
and the repository exists.
请确保您拥有正确的访问权限
并且存储库存在。

经过翻译可以得知我是在上传过程中没有权限所以被拒绝了，经过了对git的一番了解以后得知我好像做少了其中一个比较重要的一步，就是设置一个SSH KEY，即是密钥，（出于安全考虑，Github 服务器和我们本地的通讯要求使用 SSH Key 来验证）。这个时候只需设置一个密钥就行了。

![image-20200923095327702](C:\Users\LC\AppData\Roaming\Typora\typora-user-images\image-20200923095327702.png)

![image-20200923095353270](C:\Users\LC\AppData\Roaming\Typora\typora-user-images\image-20200923095353270.png)

![image-20200923095433519](C:\Users\LC\AppData\Roaming\Typora\typora-user-images\image-20200923095433519.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20190611015442313.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80NDM5NDc1Mw==,size_16,color_FFFFFF,t_70)

Github上面的key创建完成后就可以执行git push --set-upstream origin master这条指令了。

\#为什么要用git push#
git push -u origin master 上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用git push了。

git push，默认只推送当前分支，这叫做simple方式。此外，还有一种matching方式，会推送所有有对应的远程分支的本地分支。Git 2.0版本之前，默认采用matching方法，现在改为默认采用simple方式。

### 问题2

$ git push -u origin master
To github.com:wwyjc/dataFile.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'github.com:wwyjc/dataFile.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

出错：
`! [rejected] master -> master (fetch first) error: failed to push some refs to ' 。。。'`

出现这个问题是因为github中的README.md文件不在本地代码目录中，可以通过如下命令进行代码合并

```
git pull --rebase origin master
```