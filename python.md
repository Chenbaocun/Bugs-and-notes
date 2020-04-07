# python基本语法及三方库等 以及bug
#### 1. urllib在使用时，报invalid proxy 127.0.0.1:1080
暂未解决（关闭Internet的代理和关闭ss都无效）
#### 2. 在Windows上同时安装python2和python3的时候，使用python命令会进入py2环境，使用py-3可以进入python3环境。
#### 3. 如果把源码版的tensorflow添加到环境变量中，编译器则会自动地使用源码版的tensorflow，所以使用python import tensorflow会报错。
#### 4. 源码版的tensorflow是最新版本的。包含所有的tensorflow源代码，以及各种接口，demo等。
#### 5. 内置的open函数？w和wb区别
- w方式写入时:\n自动替换成\r\n进行换行
- wb方式写入时:\n在Windows上不会被识别为换行，但是在Linux上就没区别了。
- w可写
- 但是w+是可读可写。
#### 6. centos中对于字符串拼接的话应该用统一的双引号，若是单引号拼双引号，结果是单引号的，如果调用open的话就打不开了。
示例：    file=open("../UploadVideos/"+"video"+".mp4",'wb+')---并不是这个问题
不知道为什么在view.py 中访问上一级用的是. 可能是因为Django启动的路径在上一级。
#### 7. centos上安装了jupyter之后找不到命令？
环境变量没有配好
可以使用python jupyter（python是存在于环境变量中的）
也可以export PATH=/usr/local/python3/bin/:$path（不知道为什么会覆盖原来的所有命令，并且重启失效）
永久方法：vim /etc/profile 最后一行添加export
执行source /etc/profile
#### 8. 配置远程jupyter
https://www.cnblogs.com/wwwhza/p/8821117.html
sha1:dee28657e206:54415732c0f30dbc6aa1eae3cf4d7377474a74b3
#### 9. 启动jupyter
jupyter notebook (--allow-root)
#### 10. 在启动新线程的时候一定不能使用相同的name，它们应该都是unique的，否则会造成上一个线程占用资源不释放而出错的情况。尤其是在线程中又调用自己。
#### 11. 计算程序运行时间(单位为s)
```python3
import time
start=time.clock()
需计算代码块
print(time.clock()-start)
```
#### 12. loc 与iloc的区别
iloc（i有integer的意思，从0开始）只能用数字作索引，索引的是行号而不是index，loc（location）可以用数字或者字符串作索引，索引的是index
#### 13. 在Ubuntu上安装Python3.8
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
#### 14. 把镜像改为国内源
- https://blog.csdn.net/sinat_21591675/article/details/82770360
在Ubuntu上创建.conf文件可以使用touch pip.conf命令

#### 15. pip 升级之后报错  
- 把/user/bin/pip 文件改为
from pip import __main__  
sys.exit(__main__._main()_)   
#### 16. 在pycharm中使用Ctrl+q可以查看源码中函数的docstring
#### 17. 如果同级模块无法使用import导入
可以右击mark directory as source root
#### 18. 关于Python文件夹中的pyc文件
- 当Python发现我们在脚本中使用import将某个模块引入时，由于此类模块是实现编好且经过测试的，因此开发者认为此类文件不会经常改变，因此将其使用cpython进行预编译成pyc文件，其中包存储编译后的字节码。
因此当脚本重新运行时，如果发现了字节码，并且没有对其修改过，就直接调用该pyc文件。如果主动删除，再次运行会重新产生。
是否修改的验证方式：检查源文件与字节码的时间戳。
#### 19. list的sort方法中的key参数
```python3
# 获取列表的第二个元素
def takeSecond(elem):
    return elem[1]
##### 列表
random = [(2, 2), (3, 4), (4, 1), (1, 3)]
##### 指定第二个元素排序
random.sort(key=takeSecond)
##### 输出类别
print '排序列表：', random
```
#### 20. tuple元组
- 如果在定义元组时，只初始化一个元素，必须使用（1，），否则Python解释器不会认为定义的变量是一个元组，而是int之类
元组时不能对其自身进行修改的，如果想要修改需要使用切片等操作重新构建一个新元组
元组只有两个类方法：就是count 和 index
#### 21. 格式化字符串%后边的元素上是一个元组tuple，可以使用tuple和list等进行替换
#### 22. 在字符串中使用双引号   
- 单引号定义字符串，内部使用双引号
- 双引号定义字符串，内部使用转义字符
#### 23. 字符串匹配
str.count()不仅可以在字符串中数元素出现次数，还可以找子字符串
#### 24. 字符串中使用isspace判断字符串是不是空字符串
\r\t\n都认为是空白字符
#### 25. 对象的属性也可以是对象
#### 26. 多继承时，如果多个父类中存在同名的属性或者方法，将调用最先调用的的父类中的属性或者方法
- 具体的执行顺序可以使用cls.__mro__()魔法方法进行查看
#### 27. 新式类和旧式(经典)类
- 在py3中默认创建的类时以object为基类的新式类，而在py2中，如果不指定继承(object)将默认不以obj为基类。建议无论py2还是3都使用object为基类
#### 28. 单例模式
- 在多次调用实例化对象的后，只会有一个实例对象
思路：重写new对象，使用类变量对new后的cls进行记录，判断cls是否为none，已经分配过内存了，分配了就不再进行分配了。
同理init
#### 29. try catch捕获未知异常
- 我们并不能记住所有的像ValueError或者ZerodivisionErro等，我们可以使用这样的代码
```python3
try:
  pass
catch Exception as result:
  print("未知错误,%s"%result)
```
#### 30. 函数内部的异常，会层层上传，上传到调用的地方，最好还是在主程序调用函数的时候用try catch包裹，要不要在函数内进行包裹见仁见智
#### 31. 如果在import两个不同模块中调用了同名函数，则先引入的会被覆盖，会使用后引入的。可以给先导入的as一个别名即可
#### 32. import的模块搜索路径  
- 首先会在当前目录下进行搜索，如果没有就去系统内置模块路径下进行查找。可以使用module.__file__ 属性对模块路径进行查看。
#### 33. 遍历list并按条件删除的正确姿势
```python3
a= [1,2,3,4]
for i in a:
  if i ==1:
    a.remove(i)
```
- 由于remove会使a在删除元素的位置前移，但i却是累加的，所以，会使得部分元素无法遍历到。
- 解决思路： 遍历采用复制的list，删除使用原来的list
- 或者使用b = filter(lambda x: x>5,a)
- b = [i for i in a if i >5]
- 或者从后向前进行遍历
```python3
a = [1,2,3,4,5,6,7,8]
print(id(a))
for i in range(len(a)-1,-1,-1):
    if a[i] > 5:
        pass
    else:
        a.remove(a[i])
print(id(a))
print('--------------------')
print(a)
```
#### 34.对eval的使用:
```python3
Synset = synset
paths.append(eval(v))# 单引号的问题，使得Synset('writer's_name.n.01')，就算定义了函数Synset()，相当于无法传入一个参数而报错
```
- 如果字符串的list中都是基础数据类型(string,int)等，可以直接将字符串转成list等。
- 但是如果字符串中list的基本元素包含有函数，需要首先定定义同名函数
- 如果基本元素带有单引号的话，由于字符串存储时有自带两个单引号，这是就算定义了那个函数，但是由于单引号的原因，相当于字符串的参数对应不上，原本只要传入一个字符串，由于中间存在单引号的关系，导致解析失败。
#### 35.对list进行遍历并根据条件进行修改
- 使用
```python3
for node in path：
  if ...:
    path.index(node) = 。。。。
```
如果是简单的赋值这种是可以的
- 但是较为复杂，特别是所赋的值可能与原来类型不同的话，会导致报错。（应该是因为数据类型不同导致内存中的未知错误）。尽量避免这样写，而是选择使用遍历索引的方式进行修改。
