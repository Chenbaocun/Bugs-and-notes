# vue学习笔记
#### 1. ES6有块级作用域，最好实用let 代替var
#### 2. const
- 标志符修饰为常量，初始化必须赋值，且后续无法修改
- 对象不能改，但是如果对象是一个{name:'123'}这样的值的话，内部属性是可以修改的。
#### 3. v-on 用来进行事件的监听
- v-on:click='increment'
- 语法糖：@click='increment'
- increment 是method中定义的方法。也可以使用像count++这样的简单运算。
#### 4. v-on:click='increment'不加括号
- 如果不进行参数传递可以不加括号
- 但是不加括号默认是会传入一个event参数的，可以在事件触发的function（event）内使用event获取这个对象
- 传递参数的话，可以按照函数的参数定义调用即可
- 如果在传递参数的同时需要得到event可以在传实参时使用$event传入就行了
#### 5. v-on的修饰符
- .stop : 如果一个按钮嵌套在一个div内，且两个div都定义了点击事件，那么如果btn触发了点击事件，就会由于事件冒泡，导致div中的事件也会触发。为了阻止这个冒泡可以使用@click.stop='btn'
- .prevent: 如果一个标签如<input type='submit'>点击默认会执行提交操作，如果想阻止这类标签的默认事件可以使用 v-on:click.prevent='click(aaa)'
- 监听键盘按键像enter，可以使用@keyup.enter='keyup'
- .once:使按键等点击事件只触发一次，多次点击无效。@click.once='click'
- .native: 用来监听 **组件** 的原生事件
