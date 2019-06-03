# CentOS 命令及bug记录
1. apache命令
- service httpd start 启动
- service httpd restart 重新启动
- service httpd stop 停止服务
2. clear（）清屏
3. rz 上传文件
4. sz filename 下载文件。
5. 修改主机名
hostname Tom（临时）
vi /etc/hostname（直接改文件，永久的，但是也是小写的）
hostnamectl set-hostname Tom 只能改成小写的。
vim /etc/hosts里的配置信息 将第二个参数改为Tom
6. 安装rz
yum install lrzsz
7. Centos安装python3
https://blog.csdn.net/lovefengruoqing/article/details/79284573
8. Centos 安装mysql
https://www.cnblogs.com/silentdoer/articles/7258232.html
9. firewall-cmd --state时报错
第一步，vim /usr/bin/firewall-cmd， 将#！/usr/bin/python -Es 改为 #！/usr/bin/python2 -Es（到目前为止，上面提到的问题已解决）
第二步，vim /usr/sbin/firewalld, 将#！/usr/bin/python -Es 改为 #！/usr/bin/python2 -Es (这一步是针对于防火墙报错，进行的修改)
10. 安装git
yum install -y git
git --version
11. 安装protobuf
12. 安装zip
yum install -y unzip zip
13. 删除文件夹
rm -rf
14. 新建文件夹
mkdir flodername
15. 阿里云的监控插件安装后，会自动运行在进程中。
16. centos在cpu占用在100%之后，依旧可以保持高效的响应。
