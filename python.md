# python三方库等bug
1. urllib在使用时，报invalid proxy 127.0.0.1:1080
暂未解决（关闭Internet的代理和关闭ss都无效）
2. 在Windows上同时安装python2和python3的时候，使用python命令会进入py2环境，使用py-3可以进入python3环境。
3. 如果把源码版的tensorflow添加到环境变量中，编译器则会自动地使用源码版的tensorflow，所以使用python import tensorflow会报错。
4. 源码版的tensorflow是最新版本的。包含所有的tensorflow源代码，以及各种接口，demo等。
5. 内置的open函数？w和wb区别
w方式写入时:\n自动替换成\r\n进行换行
wb方式写入时:\n在Windows上不会被识别为换行，但是在Linux上就没区别了。
w可写
但是w+是可读可写。
6. centos中对于字符串拼接的话应该用统一的双引号，若是单引号拼双引号，结果是单引号的，如果调用open的话就打不开了。
示例：    file=open("../UploadVideos/"+"video"+".mp4",'wb+')---并不是这个问题
不知道为什么在view.py 中访问上一级用的是. 可能是因为Django启动的路径在上一级。
7. centos上安装了jupyter之后找不到命令？
环境变量没有配好
可以使用python jupyter（python是存在于环境变量中的）
也可以export PATH=/usr/local/python3/bin/:$path（不知道为什么会覆盖原来的所有命令，并且重启失效）
永久方法：vim /etc/profile 最后一行添加export
执行source /etc/profile
8. 配置远程jupyter
https://www.cnblogs.com/wwwhza/p/8821117.html
sha1:dee28657e206:54415732c0f30dbc6aa1eae3cf4d7377474a74b3
9. 启动jupyter
jupyter notebook (--allow-root)
10. 在启动新线程的时候一定不能使用相同的name，它们应该都是unique的，否则会造成上一个线程占用资源不释放而出错的情况。尤其是在线程中又调用自己。
11. 
