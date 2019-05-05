# 目标检测/人头监测
1. **idl接口定义语言文件的读取**
正常open，然后readlines，再进行处理即可  
2. **使用tf导入图片，报错：UnicodeDecodeError: 'utf-8' codec can't decode byte 0x89 in position 0: invalid start byte**  
解决方法：使用rb模式代替r采用2进制导入即可，image_raw_data=tf.gfile.FastFile("./1.png","rb")  
3. **在pycharm中可以正常import，但是在cmd中却包no module错误**
在pycharm中运行的时候，IDE默认把导入的项目文件夹作为搜索目录，但是当在命令行中执行的时候，只会在当前路径下进行搜索。

4. **安装pycocotool，默认安装会出错**
先安装Cython，在使用pip+git安装大佬改写的windows版本的pycocotools
pip install git+https://github.com/philferriere/cocoapi.git#subdirectory=PythonAPI
5. **将.proto文件，编译成py文件**  
下载好protoc，建议使用1.4版本，高版本有可能会出现无法编译的情况。直接把压缩包中的exe文件放到要编译的文件夹中，运行命令（把路径下所有的.protos文件转成.py）
protoc object_detection/protos/\*.proto --python_out=.
6. **faster-Rcnn在本机上进行测试，总会爆内存无法继续**
可能与faster-Rcnn本身的训练机制有关
7. 
