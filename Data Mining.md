# DataMining相关bugs及技巧记录
1.**报错UnicodeDecodeError: 'utf-8' codec can't decode byte 0xba in position 0: invalid start byte**  
用记事本打开csv，另存为，把编码从A开头改成utf-8即可。爬虫自动生成的csv文件是ANSI编码.  
2. **pycharm运行结束后，不会自动结束。**  
Edit Configurations>>emulate terminal in output console 取消即可  
3. **由于网速问题带来的pip安装超时问题**  
	pip --default-timeout=100 install keras  
4. **TensorFlow-gpu安装**  
查看支持的cuda版本，下载安装相应版本的cuda，下载对应的cuDnn，解压之后复制到cuda安装根目录下。最后pip安装TensorFlow   
5. **安装TensorFlow-gpu的时候必须先安装visual C++ 1G左右**   
Pip国内镜像：
pip install --index-url https://pypi.douban.com/simple tensorflow
或pip install --index-url http://mirrors.aliyun.com/pypi/simple/ tensorflow  
6. **安装tensorflow之后使用时出现AVX指令警告**  
自行忽略吧，没啥影响  
7. **RequestsDependencyWarning: urllib3 (1.24.1) or chardet (3.0.4) doesn't match a supported version!**  
Gpu版本无需关系此警告，忽略警告代码：  
import os 
	os.environ['TF_CPP_MIN_LOG_LEVEL'] = '2'   
8. 无论是2017版vc Redistributable 还是环境变量都无法成功找到DLL，遂还是先安装1.12.0版本及对应cuda9和cuDnn7.4.2.24，等新的对应关系出来再说。实践证明这个选择是正确的。等在过段时间再升级tensorflow-gpu的更高版本吧。不过现在测试显示速度贼鸡儿慢，与cpu版本速度相差不大。（960m-compute capability=5）  
9. **使用tensorboard显示训练过程。**  
只有在程序运行的过程中才能进入网站，先在model.fit（）中添加callbacks属性callbacks=[TensorBoard(log_dir='./tmp/log')。路径中不能包含空格，然后再使用cmd进入python\Scripts下执行D:\python\Scripts>tensorboard.exe --logdir=path（log的路径）  
10. **git命令**  
Git add . Git add *
Git commit -m ‘init’
Git push -u origin master
Git pull
git remote add origin 你的远程库地址  
11. **使用豆瓣源进行pip安装opnecv**  
pip  install  -i  https://pypi.doubanio.com/simple/  --trusted-host pypi.doubanio.com  opencv-python  
12. **k匿名对于数据挖掘工作是不是有用？**
&emsp;对于数据挖掘工作来讲，如果对一个字段进行简单的替换，使其不再具备语义，对于数据挖掘工作来讲是没有丢失可用信息的。因为在数据挖掘工作中，用到的只是这个字段的标识。但是当攻击者得知你的替换准则之后，就会造成数据的泄露。但是在k匿名工作中，信息丢失是匿名算法的性能评价准则，追求既达到k匿名，又保证足够少的信息丢失，这种信息丢失是无可避免的，及时攻击者知道了泛化方法，他一定程度上也得不到准确的泛化前的结果，但是更能保护用户的的隐私。
13. **k匿名的直观理解**
&emsp;对一些字段进行泛化，从而达到在整个数据集中，至少存在k条记录，从而达到不能唯一区分一个人的作用。
14. **数字泛化**
&emsp; 拿手机号举例，就是将手机号中的某几位抹去，即可实现泛化的效果。
15. **汉字泛化**
将单一单词转为单词集合。
