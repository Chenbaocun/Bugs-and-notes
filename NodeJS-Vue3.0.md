# NodeJS,Vue学习笔记
## 环境版本
- NodeJS(v10.15.3)
- Npm(6.9.0)
- Vue-Cli(3.8.2)
- Vue(2.6.10)
### bug及学习记录
1. DOM是指定义访问和操作HYML文档的标准。DOM树下边包含，<html><head><body>等标签。  
2. Nodejs安装：直接在官网下载最新的msi安装即可，安装的过程中会配置environment variables。安装过程附带npm的安装。  
3. Vue最新稳定版的安装：npm install vue  
4. Vue-cli是命令行工具，安装：npm install -g vue-cli     -g是为了在全局中使用vue命令（Vue貌似安装到了c盘）  
5. 对于windows的node版本控制，可以使用NVM（Node Version Manager），可以方便地切换NodeJS版本。地址：
Windows：https://github.com/coreybutler/nvm-windows  
6. 创建vue项目：与Django类似。进入指定目录打开shell，运行命令vue init webpack FirstVue-HelloWorld。  
7. Init vue项目的时候vue cli报错。Failed to download repo vuejs-templates/webpack-simple: tunneling socket could not be established, cause=connect ECONNREFUSED 127.0.0.1:80
解决方法：npm config set http-proxy null,npm config set proxy null
8. 设置淘宝镜像：npm install -g cnpm --registry=https://registry.npm.taobao.org
9. cnpm install cnpm -g升级 cnmp
继续尝试无果后
还是不行
10. 发现cli改名了Npm install -g @vue/cli和npm install -g @vue/cli-init。
11. 卸载旧版本的vue命令：npm uninstall vue-cli -g
12. 查看端口 netstat-ano
13. Npm config ls
14. 忘记mysql密码：
首先登录MySQL。  
mysql> use mysql;  
mysql> update user set password=password('123') where user='root' and host='localhost';  
mysql> flush privileges; 
15. 在vue cli3.0中创建项目的命令 vue create或者vue ui可以进入可视化的创建页面。
14. 后端采用Django
15. 连接mysql报错：Error loading MySQLdb module: No module named 'MySQLdb'
解决方法：因为Python3.5+并不支持MySQLdb，使用MySql可以使用pymysql代替，据说两者使用方式相同，
用pip安装pymysql，然后pymysql.install_as_MyQLdb()即可
16. 运行命令（npm run serve）
17. 打包命令（npm run build）
18. 打包后的dist文件放到Django后无法引入css样式
(1)在vue项目根目录下新建vue.config.js。添加内容如下：
//这个是自己加的
module.exports = {
 // 基本路径
//publicPath: './',
 // 输出文件目录
 outputDir: 'dist',
assetsDir:'static'
};
（2）运行npm run build ，把生成static文件夹中的文件剪切出来，放到根目录下，再整体放到Django的static文件夹下边就行了。
19. 反向inspectdb  正想先 makemigrations (初始化 python manage.py migrate)
20. 创建超级用户：python3 manage.py createsuperuser
用户名：chenbaocun
邮箱：1066134123@qq.com
密码：52ni
21. File was loaded in the wrong encoding: 'UTF-8'
使用GBK编码Reload即可。
UTF-8是万国码，世界通用的网站编码，GBK是大陆通用的网站编码。
22.Vue的路由，是在前端网页之间的路由，而后台路由是，用来索引存储在服务器上的各种资源，比如img，js等。
23. 对于组件化的vue，最重要的也是为了实现单页面，以及，组件的复用，因此通过路由的方式，<router-link>所指向的组件，都会在<router-view>的位置进行替换。
21. 后台运行nohup python manage.py runserver 0.0.0.0:80 >/dev/null 2>&1&
22. apache启动
service httpd start 启动
service httpd restart 重新启动
service httpd stop 停止服务
23. 查看进程:ps -ef.
结束进程：kill -9 pid
24. 端口相关
netstat -nap #会列出所有正在使用的端口及关联的进程/应用
netstat -lnp|grep 80 查看80端口正在被哪个端口占用
25. 在centos6.x中防火墙使用的是iptables，但是到了centos7.x中，默认防火墙变成了	firewalld。
26. 查看防火墙状态：firewall-cmd --state
开启防火墙：service firewalld start
查看防火墙开放端口列表： firewall-cmd --zone=public --list-ports
27. Windows和Linux回车换行问题，先安装dos2unix
yum install -y dos2unix
28. Pycharm创建的venv无法再linux上运行,会出现python空格及回车问题。Venv只能在同一平台中进行项目之间的隔离。
29. 安装指定版本的包：pip3 install django==1.0.7
30. pip show pip 查看pip版本
    python -m pip install --upgrade pip 升级pip
31. 删除文件夹 rm -rf dirname
32. 查看已经安装过的npm包：npm list -g --depth 0
33. 安装完axios之后，无法引用：因为axios并不是vue的一个插件，所以不能用vue.use的方式进行引入。使用vue.prototype.$ajax(axios)引入。使用this.$ajax调用即可。
34. Axios与django交互的问题。必须在前端将要发送的数据用qs模块进行序列化成类似get形式的字符串。
35. Django接收到的数据形式是QueryDict的形式。e.g.
<QueryDict: {'UserNum': ['222222222'], 'PassWord': ['33333333333']}>
36. 在axios的回调函数中无法选中this的解决方法：添加bind(this)即可
37. 服务器上的mysql版本太低(5.5)，将django版本将为2.0
38. 使用清华的镜像 pip install -i https://pypi.tuna.tsinghua.edu.cn/simple django==2.0   2.0版本是2017年底出的
39. Django甚至无需在logout之后在前端删除cookie，他自己就可以删掉。还是在后端没有自行向前端回复命令命令的情况下。可能在进行auth.logout之后就会自行发送了。就像在login之后，前端就已经存储了一个seesionid。
40. 现在项目中执行makemigrations会报错，直接在数据库中建表，再反向。
41. 安装vue cli
npm install -g @vue/cli  (-g是全局安装参数)
42. 查看vue cli 版本
vue --version
43. 创建vue项目：
vue ui 使用图形化界面创建vue项目
vue create hello-world 通过命令行创建vue项目，命令繁琐。
44. 创建Django项目
45. 安装element ui ：npm i element-ui -S
46. 安装axios:npm install axios --save
47. 安装qs:npm install --save axios vue-axios qs (用来解决vue中post请求以 a=a&b=b 的格式)
48. 安装vue-router：npm install --save vue-router
49. before-upload中由于axios的异步，导致无法return false，即使是添加sleep也无法阻止。改用on-change，并且取消自动上传，由于上传成功也会调用onchange，所以添加ready判断。
