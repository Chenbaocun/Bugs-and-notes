# 安卓移动开发
1. Android Studio自带jre(java run environment)，不安装jdk也是可以使用的
2. NDK环境为在开发app的过程中使用C，C++提供可能。
3. **targetSDKversion、minSDkversion、compileSDKversion**
- minSdkVersion：规定app能运行的最低版本。如果手机安卓版本小于这个版本，则无法运行，这也是应用商店判断某个应用能否运行在某台设备上的重要指标。在开发的过程中，AS会根据这个版本判断，是否能使用某个sdk下定义的方法，如果进行使用的话会出现warning。
- compileSdkVersion：规定程序编译的版本。一般选择最新的sdk版本，它不会影响app在安卓设备上的运行，它是在AS层次上的一个参数，并不会被打包进app中。他的主要作用是：在编译的时候检查代码的错误和警告。其次是一些三方库使用了高版本的sdk，所以compileSDKVersion需要选择比他们更高的版本。
- targetSDKVersion：开发过程中使用的api版本，是app在设备上运行时方法的选择指标。系统通过这个参数保证app的向前兼容性，如果app运行在>19的设备上，但是targetSdkVersion是小于19的，那么还按照targetSdkVersion的指定版本的api进行运行。对于后续sdk新添加的版本中的api，那么可以采用重构app，提升targetSdkVersion即可。
