# python三方库等bug
1. urllib在使用时，报invalid proxy 127.0.0.1:1080
暂未解决（关闭Internet的代理和关闭ss都无效）
2. 在Windows上同时安装python2和python3的时候，使用python命令会进入py2环境，使用py-3可以进入python3环境。
3. 如果把源码版的tensorflow添加到环境变量中，编译器则会自动地使用源码版的tensorflow，所以使用python import tensorflow会报错。
4. 源码版的tensorflow是最新版本的。包含所有的tensorflow源代码，以及各种接口，demo等。
