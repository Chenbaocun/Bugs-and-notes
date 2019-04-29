# 目标检测/人头监测
1. idl接口定义语言文件的读取  
正常open，然后readlines，再进行处理即可  
2. 使用tf导入图片，报错：UnicodeDecodeError: 'utf-8' codec can't decode byte 0x89 in position 0: invalid start byte  
解决方法：使用rb模式代替r采用2进制导入即可，image_raw_data=tf.gfile.FastFile("./1.png","rb")
