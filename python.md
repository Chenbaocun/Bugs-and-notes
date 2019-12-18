# python基本语法及三方库等 以及bug
1. **urllib在使用时，报invalid proxy 127.0.0.1:1080**
暂未解决（关闭Internet的代理和关闭ss都无效）
2. 在Windows上同时安装python2和python3的时候，使用python命令会进入py2环境，使用py-3可以进入python3环境。
3. 如果把源码版的tensorflow添加到环境变量中，编译器则会自动地使用源码版的tensorflow，所以使用python import tensorflow会报错。
4. 源码版的tensorflow是最新版本的。包含所有的tensorflow源代码，以及各种接口，demo等。
5. **内置的open函数？w和wb区别**
w方式写入时:\n自动替换成\r\n进行换行
wb方式写入时:\n在Windows上不会被识别为换行，但是在Linux上就没区别了。
w可写
但是w+是可读可写。
6. **centos中对于字符串拼接的话应该用统一的双引号，若是单引号拼双引号，结果是单引号的，如果调用open的话就打不开了**。
示例：    file=open("../UploadVideos/"+"video"+".mp4",'wb+')---并不是这个问题
不知道为什么在view.py 中访问上一级用的是. 可能是因为Django启动的路径在上一级。
7. **centos上安装了jupyter之后找不到命令？**
环境变量没有配好
可以使用python jupyter（python是存在于环境变量中的）
也可以export PATH=/usr/local/python3/bin/:$path（不知道为什么会覆盖原来的所有命令，并且重启失效）
永久方法：vim /etc/profile 最后一行添加export
执行source /etc/profile
8. **配置远程jupyter**
https://www.cnblogs.com/wwwhza/p/8821117.html
sha1:dee28657e206:54415732c0f30dbc6aa1eae3cf4d7377474a74b3
9. **启动jupyter**
jupyter notebook (--allow-root)
10. 在启动新线程的时候一定不能使用相同的name，它们应该都是unique的，否则会造成上一个线程占用资源不释放而出错的情况。尤其是在线程中又调用自己。
11. **计算程序运行时间(单位为s)**
```python3
import time
start=time.clock()
需计算代码块
print(time.clock()-start)
```
12. **loc 与iloc的区别**
iloc（i有integer的意思，从0开始）只能用数字作索引，索引的是行号而不是index，loc（location）可以用数字或者字符串作索引，索引的是index
13. **在Ubuntu上安装Python3.8**
下载源码
安装build-essential
安装OpenSSL
安装OpenSSL-dev
./configure --prefix=/usr/local/python3.8 --enable-optimizations（并不是网上说的 --with-ssl）
make
sudu make install
安装过程若报缺少类库，自行进行安装即可
在Ubuntu18.04中，默认使用Python3调用Python3.6.5，且已经不自带Python2
安装完成后使用以下命令完成对Python和pip命令的绑定
sudo update-alternatives --install /usr/bin/python python /usr/local/python3.8/bin/python3.8
sudo update-alternaives -config python
sudo update-alternatives --install /usr/bin/pip pip /usr/local/python3.8/bin/pip3.8
sudo update-alternaives -config python
14. **把镜像改为国内源**
https://blog.csdn.net/sinat_21591675/article/details/82770360
在Ubuntu上创建.conf文件可以使用touch pip.conf命令

15. **pip 升级之后报错**
把/user/bin/pip 文件改为
from pip import __main__
sys.exit(__main__._main())
