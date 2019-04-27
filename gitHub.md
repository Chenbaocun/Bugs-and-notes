#git学习笔记

##常用命令
1. 查询git的用户名和密码  
git config user.name  
git config user.email

2. 修改、添加用户名和密码（global 意思是在此电脑的所有repo中使用这个设置）
git config --global user.name “username”  
git config --global user.email “email”  
3. 用户名和邮箱的作用  
   - 用来记录每次的commit
   - 开源项目的contribution是根据邮箱进行统计的。  
4. 创建目录  
   git init  
5. 查看仓库（工作区）当前的状态
   git status
6. 比对文件，找到修改的地方
   git diff readme.md
7. 将文件添加到暂存区，并提交到本地repo
   git add readme.md   
   git commit -m "注释"  
8. 查看提交记录
git log (返回带Author和Date的完整日志)
git log --pretty=oneline
返回结果中乱码是commit id，它是一个SHA1计算出来的16进制的数
9. 版本回退
git reset --hard HEAD^(HEAD表示当前版本，回退到上一个版本,这个操作会使git log中的记录也消失，现在repo已经回退到上个版本，HEAD也已经指向了回退后的上一个版本)
^太多的时候可以使用 HEAD~100进行回退
10. 版本回退后，返回回退前的版本(前提：命令行在上次回退之后没有被关闭)
git reset --hard 1094a(commit id 无需全写，但也不能写太少，以保证查询结果只有一个)
11. 命令行关闭，或者电脑关闭，无法找到commit id，如何进行版本回退？
git reflog(返回所有的命令记录，找到想要返回的版本 commit id)
git reset --hard commit id 即可
12. 工作区（Working Directory）
项目的文件夹称为工作区
13. 版本库（Repository）
在工作区文件夹中有一个隐藏的文件夹就是.git文件夹。
git版本库中主要包括两部分：
&emsp; - Stage(暂存区)
&emsp; - master(Git在init时创建的master分支)HEAD指针指向当前版本库的分支
.git版本库示意图：
![.git版本库](/img/Repository.jpg)
流程：git add命令将文件添加到了暂存区，git commit命令将之前add到暂存区的文件统一提交到分支中，提交之后，暂存区会被清空，并且使用git status命令将返回working tree is clean。表示工作区在上次提交之后没有任何修改，无需commit
14. 比对工作区文件与版本库中的最新版本有什么不同
git diff HEAD --readme.md
15. 撤销工作区的修改
如果在工作区中对文件进行了修改，并且已经无法手动还原，可以使用git checkout --readme.md
*如果当前状态：修改完还未add到暂存区。将撤销修改到与版本库中版本一致*
*如果当前状态：修改完并且已经add到暂存区。将撤销修改到上次add到暂存区之后的状态*
16. 撤销暂存区的添加
如果不希望把现在暂存区的文件进行提交，可以使用git reset HEAD <file>把暂存区内的文件从暂存区中撤销到工作区。
17. 如果错误文件添加到了版本库，撤销操作可以使用版本回退
git reset --hard HEAD^
18. 删除文件
git rm readme.md 这个命令不但会删除工作区的文件，还会将修改写入暂存区。
git commit -m 'remove readme.md'
如果是误删，可以使用checkout命令将工作区恢复到与版本库一直的状态。git checkout --readme.md
19. github中https与SSH的区别？
https与ssh下的git都可以直接进行git clone 操作
https方式每次进行push的时候，都要输入账号密码进行身份验证
但是对于SSH方式时，由于每个人的电脑都不尽相同，所以可以直接使用ssh公钥与私钥机制进行身份验证。
20. 生成ssh key
- step1：进入C:\Users\Administrator查看是否有.ssh文件夹，文件夹中是否有id_rsa和id_rsa.pub文件，如果有可以跳过第二步
- step2：在git bash中输入命令 ssh-keygen -t rsa -C "email@qq.com"，一路回车即可，生成的公钥和私钥存储在step1中的路径下。
- step3：在GitHub上：头像>>Setings>>SSH and GPG keys>>New SSH key 随便添加一个Title，把id_rsa.pub文件中的公钥复制到网页上即可。
ps:如果有在不同电脑上进行提交的需求，可以添加多个SSH key即可。
21. 将本地库与远程库进行关联
git remote add origin git@github.com:Chenbaocun/Bugs-and-notes.git
22. 将本地库的所有内容推送到远程库中
git push -u origin master
ps:-u参数的意义：在第一次push时，一般会添加-u参数，此时Git不仅会把本地的master分支推送到远程仓库的master分支，还会把本地的master分支与远程的master分支关联起来，在以后的push以及pull操作时就可以简化命令，省略-u
23. git add. git add -u git add -A 区别
- git add. 提交所有修改的和新建的数据暂存区
- git add -u 除了可以发现所有的修改与新建，还可以发现删除
- git add -A 除了前两个的所有功能,还可以发现替换.
24. 使用git add类命令时：warning: LF will be replaced by CRLF in pycharm.md.
git config core.autocrlf false  //将设置中自动转换功能关闭
