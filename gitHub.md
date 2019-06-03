# git学习笔记

## 常用命令
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
&emsp; 12.1. Stage(暂存区)
&emsp; 12.2. master(Git在init时创建的master分支)HEAD指针指向当前版本库的分支
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
25. 第一次使用SSH key关联远程库的时候，会有询问你GitHub上的key是否来自与你。输入yes即可。
26. 查看远程库  
git remote
27. 查看分支  
git branch
28. 创建分支并切换分支  
git checkout -b dev
相当于两条命令 git branch dev 和git checkout dev
29. 合并分支  
git merge dev
Fast-forward(快进模式)，就是把master指向了dev，但并不是所有的合并分支都可以使用这种方式
30. 删除分支  
git branch -d dev
31. 分支冲突  
如果在新建分支上和master分支上都分别进行了commit，所以在合并分支的时候会出现conflict的情况。
解决方法：使用git status查看冲突文件。并且git会向冲突文件写入冲突信息。手动修改，删除等操作后，正常add commit即可。
32. 查看分支合并情况
git log --graph --pretty=oneline --abbrev-commit
33. 查看分支合并图
git log --graph
34. 分支管理策略  
使用Fast forward进行分支合并，在这种模式下，删除合并完的分支之后，会丢掉分支的信息，禁止使用Fast forward可以保留分支信息。
在这种模式下，每次merge都会提交一个commit，所以可以看见分支合并历史
git merge --no-off -m "merge with no off" dev
35. bug 分支  
当我们正在一个分支上进行开发的时候，需要对bug进行修改，但是我们现在手头上的工作还未完成不能commit，因此该怎么办呢？我们可以将现在的工作快照保存下来，在去处理bug。
&emsp; - git stash把当前自己分支上的工作进行存储
&emsp; - git checkout -b issue-101 创建bug分支
&emsp; - 修改bug add file 并且commit file
&emsp; - git checkout master 回到master
&emsp; - git merge --no-ff -m "merged bug fix 101" issue-101 合并bug分支 bug解决完成
&emsp; - git checkout dev 返回自己的工作分支
&emsp; - git stash list 查看之前工作现场 存储的列表
&emsp; - git stash apply恢复现场，并且git stash drop删除现场。可直接用git stash pop完成这两步操作。
36. 可以多次stash，在恢复的时候用git stash list查看，并使用git stash apply stash@{0}来选择恢复。
37. 强行删除分支  
当我们在一个分支上进行了修改，但是还未进行merge，但是我们现在需要删除它，但是我们使用git branch -d dev会提示我们还未进行merge无法合并，此时我们可以使用git branch -D dev 进行强行删除。
38. 向其他分支进行push  
git push origin dev
39. 其他人需要在其他分支进行开发  
git clone git@github.com:Chenbaocun/Bugs-and-notes.git之后只能看见master分支
git checkout -b dev origin/dev 这样才能看见新的分支
40. 在多人合作的过程中，遇到push冲突  
因为其他小伙伴对分支进行了push，当我们对同一个分支进行push的时候，就会出现冲突问题。
此时可以用git pull 把最新的origin/dev抓取下来
41. 在pull的过程中报There is no tracking information for the current branch.  
这是因为未指定本地dev与远程origin/dev的连接,利用git branch --set-upstream-to=origin/dev dev
命令设置链接即可。在使用pull进行合并，有冲突，手动解决即可。与分支冲突解决方法相同。
42. Rebase  
将提交记录整理成一条直线
只需git rebase即可。
43. 标签  
git tag 可以查看所有的标签  
给不容易记忆的commit id打上tag
git checkout dev转到要打标签的分支上
git tag v1.0
44. 给之前的commit打标签  
git tag v0.9 f52c633即可。
45. 显示tag的具体信息
git show <tagname>
46. 创建tag的时候添加注释  
git tag -a v0.1 -m "version 0.1 released" 1094adb
47. 操作标签  
- 命令git push origin <tagname>可以推送一个本地标签
- 命令git push origin --tags可以推送全部未推送过的本地标签
- 命令git tag -d <tagname>可以删除一个本地标签
- 命令git push origin :refs/tags/<tagname>可以删除一个远程标签
48. 让git bash 能够有一些颜色   
git config --global color.ui true
49. 给命令修改别名  
 git config --global alias.st status 删除直接在config文件中删除即可
50. 忽略一些文件
文本文件中填写要忽略文件的后缀.py等或者文件夹名称
51. 强制添加文件
git add -f App.class
52. 查看被禁止的规则
git check-ignore -v App.class
53. centos 中的rsa公钥存储在/root/.ssh/id_rsa.pub
53. centos中生成rsa配置ssh
https://blog.csdn.net/wzq793957419/article/details/68067204
54. 默认无法添加空文件夹到版本库中。可以通过创建一个.gitkeep文件的方式进行占位。
55. 如何创建.gitkeep文件？
type NUL > .gitkeep
56. 为什么我明明每天commit很多次，但是却不记录我的commit？
打开commit发现，commit是没有头像的，因为本地git的邮箱与github的邮箱不一致。使用git config --global user.name “emails” 进行重新设置。注意一定要有引号。
57. private仓库的贡献是否可以记录并展示在profile中？
可以，需要在settings Profile 勾选Include private contributions on my profile
