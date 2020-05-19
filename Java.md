# Java学习笔记 2019-2020
### 视频链接:https://www.bilibili.com/video/BV1A4411K7Gx
### 教程连接：https://www.liaoxuefeng.com/
#### 1. Java中的 +
- 在java中 str+int -->str，而在Python中str + int会报错，除非自行将int转换成str。所以在输出时可以直接使用str和数值型变量进行拼接
- 在java中 char + int ,会先将char转成ASCII或者Unicode编码再进行加法
- 任何类型和 str 相+，都会变成字符串
#### 2. idea的项目结构
- project 项目根路径
- module 模块,创建后自带一个src文件夹，用于在其中进行源代码的书写，还有一个iml文件存储相关配置信息。
- package 包，包的名称一般使用类似域名的反向，如com.baidu.day01。在文件夹内显示的是com/baidu/day01
- package里边可以进行.java文件的书写。创建class出来的是.java。编译后生成.class。这个.class文件存储在项目跟路径下的out文件夹内
##### 3.method方法的定义和调用
- 一般都会使用
```java
  public static void 方法名称(String[] args){
    方法体；
  }
```
- 调用时在main函数中进行调用
- 不允许进行方法的嵌套定义， 顺序无所谓，且没必要像c语言一样进行提前的函数声明
- 方法定以后不会执行，与Python等编程语言逻辑一致。
#### 4.定义方法的注意事项
- 返回值的类型需要在定义时进行给定
- 形参必须给类型，但是不能像Python一样给它进行赋值，完成默认值的设定
- 所有变量第一次出现前边必须跟着类型
- 语句结束有；括号结束没有；
- return和Python一样，可以只写个return，后边不加内容。此时效果同不写一样
#### 5.Method的overlord
- 方法名相同，但是参数个数不同。
- 方法名相同，参数个数相同，参数类型不同
- 方法名相同，参数个数相同，参数类型相同，但是参数的顺序不同
- 定义多个名称相同，但是参数个数不同的方法，在调用时，根据参数个数自行匹配，能找到即可。
#### 6.Method的无关因素
- 与形参的名称无关
- 参数的返回值类型无关（如果其他完全一致，只有返回值类型不同的话，会产生歧义，函数将不知道套入那个方法）
#### 7.java中的方法重载只是为了保证在严格的变量类型定义下的函数操作，这个操作在Python中，由于其动态类型的原因，这个功能是其函数天然存在的。
#### 8.java中的整形：byte ，short，int，long
#### 9.java的println函数其实就是在jdk中对不同的数据类型进行了重载，所以我们可以随意地向这个函数内传入参数。
#### 10.数组Array
- 属于引用类型，由基本数据类型构成
- 数组内的元素，数据类型是一致的
- 数组的长度在程序运行期间不能改变
#### 11.数组的动态创建方式：指定数组的长度
- 数据类型[] 数组名 = new 数据类型[长度]
- 例如 int[] a = new int[100]
- double[] b = new double[100]
- String[] c = new String[100]
#### 12.静态创建方式：指定数组内的元素
- 数据类型[] 数组名 = new 数据类型[]{元素1，元素2....}
- int[] a = new int[]{1.2.3}
- String[] b = new String[]{"hello","world!"}
- 编译器会根据元素个数推算出数组的长度。
#### 13.静态和动态初始化方法的两步写法
- 先创建变量 int[] a;
- 赋值 a = new int[20]; 或者a = new int[]{1,2,3,4};
- 但是如果采用了下边的缩略写法的话，不能使用此两步写法。
#### 14.静态初始化方式的缩略写法
- int[] a ={1,2,3,4,5} //省去new 数据类型[]
#### 15.静态创建数组时的默认操作
- int[] a =new int[10]. 此时默认会把默认在数组内放十个0
- float型，默认赋0.0
- string 字符型，默认赋'\u0000'
- 布尔类型，默认赋false
- 引用类型，默认赋null
#### 16.java中内存划分成五个部分
- 栈(Stack):存放的都是方法中的局部变量。方法的运行一定要在栈当中运行。
  - 局部变量：方法的参数，或者是方法内部定义和使用的变量
  - 作用域：一旦超出作用域，立刻从栈内存当中消失。
- 堆（Heap）：凡是new出来的对象都存储在堆内存中。
  - 堆内部存储的数据都有一个16进制的地址
  - 对内部的数据都有默认值。规则和15条列举的一致。
- 方法区（Method Area）：存储.class相关信息，包含方法的信息
- 本地方法栈(Native  Method Stack):与操作系统相关
- 寄存器（pc register）：与cpu相关
#### 17.三元运算符
- b ? x : y //x和y的数据类型必须相同否则会报错。
- 同时三元运算符及and/or 逻辑运算符是短路计算的，计算到得出结果为止，不会做多余的计算。
#### 18.switch-break
- switch 匹配的结果需要是：整型、字符串或者枚举类型。
- 两个case可以合并在一起
```java
case1:
case2:
  System.out.println('a')
  break
```
- 在java12开始，switch更加简化了语法可以使用如下的 ->箭头形式。此时不再需要break语句。
  ```java
  case "apple" -> System.out.println("Selected apple");
  case "pear" -> System.out.println("Selected pear");
  case "mango" -> {
              System.out.println("Selected mango");
              System.out.println("Good choice!");
          }
  default -> System.out.println("No fruit selected");
  ```
- 如果有多个语句并且需要进行值的回调的话，可以使用yield关键字,返回的值可以赋给变量。
  ```java
  default -> {
                  int code = fruit.hashCode();
                  yield code; // switch语句返回值
              }
  ```
#### 19.遍历数组
- for(int i = 0;i<ns.length;i++)
- for(int n : ns )
- Arrays.toString()
- Arrays.deepToString() //多维数组的打印
#### 20.数组的排序
- 内置了Arrays.sort() // 改变原数组，引用型数组采用变更指针的方式进行排序，基本类型的数组是更改位置上的值来实现真正的排序。
#### 21.命令行参数
- psvm的默认参数是 String[] args .所以可以遍历传入的参数来获得传入的参数。
- 在命令行中传入参数使用 -符号，e.g. -version
#### 22.java源代码的编译和执行
- 编译：javac Main.java //.java文件被编译成.class文件
- 执行：java Main //并不需要写后缀
#### 23.public关键字
- 修饰的变量或者类表示可以被外部访问。
#### 24.private关键字
- 使成员变量或者成员方法只能在类内部访问。
#### 25.java中类的构造方法
- 如果不重写构造方法的话，java默认会自动创建一个无参数的构造方法，用于对象的初始化。
- 重写构造方法时，只有一个public修饰符，方法名与类名相同，可以传入参数，和Python类似，但是在实例化的时候需要使用new关键字，这与Python是不一致的。
- 可以写多个构造函数，实例化时会根据参数个数的不同，自动调用符合的构造函数。
- 构造方法内可以调用其他的构造方法，直接使用this(paras),根据参数个数的不同就可以完成对构造方法的调用。
#### 26.继承
- 和Python一样，所有类的基类都是object
- 与Python不同的是，java仅允许单继承
- protected 允许该成员变量或者成员方法可以被所有继承来的子类访问。
- 子类构造方法可以调用super(),调用父类的构造方法，默认会调用无参数的父类中的构造方法。
- 所有子类都可以向上转为更抽象的类型。
- 也可以向下转型，但是仅限于经过向上转型的对象。可以事先用instanceof判断，成功后再进行转型。
- 从java14开始有了简便写法
```java
if (obj instanceof String s) {
            // 可以直接使用变量s:
            System.out.println(s.toUpperCase());
        }
```
- 子类和父类是is kind of 关系，has关系等其他联系，可以通过增加成员变量的方式进行构造。
#### 27.多态
- 子类可以复写父类的方法(override):方法名相同，且返回值也相同。但是@override并不是必须的，可以不写，但是写上可以使编辑器帮助进行语法检查。
- Overload：方法签名不同，overload出来的方法是一个新方法。
- 方法调用依赖于调用时对象的实际类型，这种行为称之为多态。
- final关键字可以使方法不能被复写(重写)。
- final关键字可以使类不能被继承。
- final修饰变量时，必须在创建时进行初始化，并且后续无法再修改。
#### 28.抽象类
- 被abstract修饰的成员方法称为抽象方法，它是没有方法体的。
- 包含抽象方法的类必须也用abstract修饰。
- 所有继承自抽象类的子类都必须重写抽象方法。
- 如果实现抽象方法的话，该子类还必须被abstract关键字修饰。
- 而面向抽象编程的coder们就可以只关注由抽象类规定的规范，从而进行成员方法的调用，无需关心子类的具体实现。
- 抽象类无法进行实例化，它相当于一个类型规范。

#### 29.接口interface
- 如果一个抽象类没有字段，且所有的方法是抽象方法，那么这个抽象类就可以改写成interface
- interface是比抽象类还要抽象的抽象类，定义时只需写interface一个关键字即可。
- 接口中的所有成员方法都是public abstract的，所以这两个关键字无需写出来。
- 当一个具体的class去实现一个interface时，需要使用implements关键字。
- 可以implements多个接口
- 接口之间继承可以使用extends
- interface可以定义default方法, 使用default的关键字修饰即可。
