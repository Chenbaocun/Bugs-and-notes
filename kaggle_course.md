# kaggle's course 学习笔记
1. **dropna subset=[col] 参数**
删除指定col列中为nan的行
2. **fit_transform 和 transform 的区别**
前者先fit，拟合出必要的参数如均值u和标准差Delta，再进行transform（数据的转换）。
如果在训练集上已经训练出来了必要的参数，如果再需要对验证集上的feature进行transform，就不用再重新进行必要参数的拟合了，直接进行transform即可。
