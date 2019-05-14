# 目标检测/人头监测
1. **idl接口定义语言文件的读取**
正常open，然后readlines，再进行处理即可  
2. **使用tf导入图片，报错：UnicodeDecodeError: 'utf-8' codec can't decode byte 0x89 in position 0: invalid start byte**  
解决方法：使用rb模式代替r采用2进制导入即可，image_raw_data=tf.gfile.FastFile("./1.png","rb")  
3. **在pycharm中可以正常import，但是在cmd中却包no module错误**
在pycharm中运行的时候，IDE默认把导入的项目文件夹作为搜索目录，但是当在命令行中执行的时候，只会在当前路径下进行搜索。以命令行的打开位置为文件目录
4. **安装pycocotool，默认安装会出错**
先安装Cython，在使用pip+git安装大佬改写的windows版本的pycocotools
pip install git+https://github.com/philferriere/cocoapi.git#subdirectory=PythonAPI
5. **将.proto文件，编译成py文件**  
下载好protoc，建议使用1.4版本，高版本有可能会出现无法编译的情况。直接把压缩包中的exe文件放到要编译的文件夹中，运行命令（把路径下所有的.protos文件转成.py）
protoc object_detection/protos/\*.proto --python_out=.
6. **faster-Rcnn在本机上进行测试，总会爆内存无法继续**
可能与faster-Rcnn本身的训练机制有关
7. 修改了config中的eval_config中的num_examples成功提高识别率 ，faster_rcnn_inception_v2_coco在仅仅跑了1k步之后，AP已经达到了0.3以上
8. 明显faster-Rcnn系列比ssd系列慢一些，但是理论上精度更高。
9. pytorch用visdom库进行参数的可视化，类似tensorboard
10. ssd系列对于小目标检测精度低，训练图片质量敏感
11. **利用tensorflow object detection api训练自己的目标检测模型的时候，效果很差**
不要忘记修改eval下边的num值，默认是8000
12. 安装bazel（手动安装过于繁琐）
使用Chocolatey包管理工具进行安装。(跟pip类似)
- 安装Chocolatey：cmd中：@powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
- 安装bazel：choco install bazel
13. bazel依赖python2，所以安装的过程中会自动下载py2，并且自动增加环境变量。但是并不能通过python2在命令行中进行操作。
14. 使用bazel编译toco。
进入tensorflow/lite 使用bazel build toco 即可。出错，暂时不使用此方法。
15. 在D:\pycharm\tensorflow\tensorflow\lite\python下边有个tflite_convert.py。可以使用此，代替使用bazel编译。
tflite_convert  --graph_def_file=saved_model/tflite.pb --output_format=TFLITE   --output_file=./model.tflite --inference_type=FLOAT  --input_arrays=x   --output_arrays=output --input_shapes=1,300,300,1
