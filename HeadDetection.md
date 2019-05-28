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
15. 从tf1.9开始，tflite_convert就作为和tensorflow一起安装的二进制工具了。以前版本的转换工具叫toco，测试发现toco在tf1.13仍然存在，但是和tflite_convert选项基本一致，可能已经合并了。
16. 在D:\pycharm\tensorflow\tensorflow\lite\python下边有个tflite_convert.py。从tensorflow1.9开始，这个脚本开始使用。可以使用此，代替使用bazel编译。
tflite_convert --graph_def_file=./tflite_graph.pb --output_file=./detection.tflite --input_shapes=1,300,300,3 --input_arrays=normalized_input_image_tensor --output_arrays='TFLite_Detection_PostProcess','TFLite_Detection_PostProcess:1','TFLite_Detection_PostProcess:2','TFLite_Detection_PostProcess:3' --inference_type=QUANTIZED_UINT8 --mean_values=128 --std=128 --change_concat_input_ranges=false --allow_custom_ops --default_ranges_min=0 --default_ranges_max=255
17. Windows版本的tensorflow无法直接使用toco导致无法convert，在阿里云centos上转换成功。建议出现此问题的话，在服务器上装一个cpu版本的转换一下就行。
18. 开始训练：--model_dir=training_ssd_fpn --pipeline_config_path=training_ssd_fpn/ssd_mobilenet_v1_fpn_shared_box_predictor_640x640_coco14_sync.config --num_train_steps=200000
19. 导出pb：python export_inference_graph.py --input_type=image_tensor --pipeline_config_path=training/faster_rcnn_inception_v2_coco.config --trained_checkpoint_prefix=training/model.ckpt-10282 --output_directory=saved_model
20. tflite只能转换ssd，对于faster-rcnn无法进行转换。转换的原理就是把op转换成轻量级的适合移动设备的op。不仅可以减小模型大小，还能加快检测速度。
21. tensorflow/examples/android中的demo可以直接把pb放到asset下，也可执行，但是速度很慢，没有经过tflite的转换。只能称之为TF Mobile
22. tensorflow\\lite\\examples\\android下边的例子是经过tflite转化的，速度明显也更快。
23. 开始训练：python model_main.py --model_dir=training_facessd --pipeline_config_path=training_facessd/ssd_mobilenet_v1_coco.config --num_eval_steps=2000
24. 对于ssd目标检测算法，本身对小目标检测存在问题，这也是ssd本身存在的问题。数据增强和一个很好的数据集对于最终模型的精度有明显提升。
25. TensorFlow object detection Api 中的config，对于小目标，从头重新开始训练反而比在coco等数据集上预训练结束的ckpt继续训练效果要好。
26. 修改eval_util.py中的eval_interval_secs 可以规定eval的间隔时间。（此方法无效）
在model_main.py 中的config = tf.estimator.RunConfig(model_dir=FLAGS.model_dir,save_checkpoints_steps=1000) 添加save_checkpoints_steps，如果设置了save_checkpoints_steps那么keep_checkpoint_max也一定要设置，否则如果时间内没有保存的话，会被garbage collect了。
27. export tflite_graph.pb:python export_tflite_ssd_graph.py --pipeline_config_path=training_ssd_fpn/ssd_mobilenet_v1_fpn_shared_box_predictor_640x640_coco14_sync.config --trained_checkpoint_prefix=training_ssd_fpn/model.ckpt-76000 --output_directory=saved_model_ssd_fpn
28.
