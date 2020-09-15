# vue学习笔记
#### 1. ES6有块级作用域，最好使用let 代替var
- var没有块级作用域
- {
  var name = '张三'
}
console.log(name) // 此处也是可用的
- 可能引起的问题：当别人调用外层的fun的时候，内部的属性却被其他人改了，那么打印就会出现问题。
- 多个按钮监听点击事件时，使用循环添加点击事件，如果响应里边都有变量i的话，那么最后他们都会循环结束时的i
- if、for没有作用域，可以使用闭包进行数据的访问，但是function有作用域
#### 2. const
- 标志符修饰为常量，初始化必须赋值，且后续无法修改
- 对象不能改，但是如果对象是一个{name:'123'}这样的值的话，内部属性是可以修改的。
#### 3. v-on 用来进行事件的监听
- v-on:click='increment'
- 语法糖：@click='increment'
- increment 是method中定义的方法。也可以使用像count++这样的简单运算表达式。
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
#### 6.vue的生命周期
- beforeCreate、Created、beforeMount、mounted、beforeDestroy、Destroyed
#### 7.插值操作
- mustache语法{{message}} e.g:{{firstname +' '+ lastname}} 或者{{firstame}} {{lastname}} 表达式：{{counter * 2}}
- <h1 v-text='message'>你好</h1> //你好会被覆盖掉
#### 8.v-once
- <h2 v-once>{{message}}</h2>
- 只会绑定一次，后续即使message再发生改变，该标签也不会改变
#### 9.v-for: 数组类型展示
- <div v-for='item in message'>
  {{item}}
</div>
#### 10.v-html 解析标签
- <h2 v-html='url'></h2>
- data:{
  url:'<a href='www.baidu.com'>百度一下</a>'
}
#### 11.v-pre,使绑定的数据原封不动地展示出来
- <h1 v-pre>{{message}}</h1> //结果直接显示{{message}}
#### 12.v-cloak，处理由js绑定数据延迟所带来的，标签闪动
- <h1 id='app' v-cloak>{{message}}</h1>
- 在数据绑定之后该标签会被删除
- 所以通过给v-cloak设置css显示与否，来解决此类闪动问题。
#### 13.v-bind 动态绑定属性,不可以直接在属性上使用{{message}}，模板语法只能在content部分使用
<a v-bind:href='url'></a>
data:{
  url = 'www.baidu.com'
}
- v-bind语法糖：<a :href='url'></a>
#### 14.动态绑定class。对象语法，多个class会自动合并
- <h2 v-bind:class='active'>{{message}}</h2>
- <h2 :class='active'>{{message}}</h2>
- <h2 :class='{类名:布尔值}'>{{message}}</h2>
e.g. <h2 :class='{line:isActive}'>{{message}}</h2>
data:{
  isActive:true
}
- {line:isActive}可以直接在methods中进行return，data记得使用this进行调用
#### 15.绑定class的数组
- <h2 :class=[active,line]></h2> 如果没加引号，相当于是变量，可以通过data进行赋值，并和原本标签上的class合并
- 如果加了双引号，相当于直接写了类名，并和原本标签上的class合并
#### 16. v-for
- <ul>
    <li v-for='(item, index) in movies'> <li>
  </ul>
  <ul>
    <li v-for='(id, name，index) in movies'> <li>
  </ul>
#### 17.动态绑定style
- <h1 :style="{fontSize:'50px'}">{{message}}</h1> //值必须加单引号，否则会当成变量并到data中去找，如果找不到就报错
- 也可以像15一样使用数组进行绑定
- <h1 :style=[basrStyle, basrStyle1]>
data:{
  basrStyle={backgroundColor:'red'},
  basrStyle={fontsize:'100px'}
}
#### 18.计算属性 computed，可以对一些数据进行计算后再使用{{fullname}}进行绑定，直接使用名词命名，不要用动词起头
computed 是有缓存的，多次调用值调用一次，但是methods是会每次都调用的
computed:{
  fuulname: function(){
    return this.firstname +' ' +this.lastname
  }
}
- 其实也可以使用方法{{getfullname()}}
#### 19.计算属性的setter和getter
在计算属性computed中，属性有set和get方法
computed：{
  firstName:{
    set: function(firstname){
      this.firstame = firstname
    }
    get:function(){
      return this.firstName
    }
  }
  //如果只需要读的话，可以简写
  firstname: function(){
    return this.firstame
  }
}
#### 20.computed与methods的对比：
- computed会进行缓存，多次调用不会重新计算，但是如果数据发生改变的话，还是会响应式地自动进行修改的。
- 但是methods是每次调用都重新计算
#### 21.对象字面量的增强写法
- const obj = {
    name:'whi',
    age：'24'，
    run: function(){
      console.log('跑')
    }，
    eat：function(){
      console.log("吃")
    }
  } //{}成为字面量
- 属性的增强写法
const name ='张三'
const age = '20'
const obj = {name， age}
- 原来写法：
const obj = {name:name,
            age:age
}
#### 22.函数的增强写法
const  obj = {
  run(){

  },
  eat(){

  }
}
#### 23.v-if、v-if-else、v-else
<h1 v-if="score >90">优秀</h1>
<h1 v-if-else="score >=80">良好</h1>
<h1 v-else>一般</h1>
#### 24.虚拟dom的复用问题，
- 用key可以解决这个问题 key = 'email'
#### 25.v-show和v-if
- v-if='true' 或者 v-if='false' 是在dom中删除和增加标签
- v-show是在给标签display：none样式与否，来控制是否显示。
#### 26.v-for最好绑定key
- 原因：在进行data的数组插值的时候，如果v-for没有绑定key的话，插入位置之后的标签都会重新赋值，最后一个元素再创建一个新的标签
- 但是如果绑定了key的话，就不会出现这种操作，而是只创建新的值的标签。
- <li v-for='item in items' :key='item'> //应该绑定唯一的数据，重复会报错
#### 27.哪些数组的方法是响应式的？
- push、pop、shift(删除第一个元素)、unshift(在数组最前边添加元素，一个或多个)、
- splice(start, end, ...num):删除元素(删除从start开始的end个元素)，插入元素(插入后边的所有多个num)，替换元素（如果删的个数和加的个数一样的话，看起来就像是替换元素）
- sort()
- reverse()
- Vue.set(this.letters,0,'bbb') // vue内部把数组中第0位替换为'bbb'
- 通过索引赋值并不是响应式的。如this.message[0] = 1
#### 28.表格标签
<table>
  <thead>
    <tr>
      <th>书籍名称</th>
    </tr>
  </thead>
  <tbody>
   <tr>
    <td>
    </td>
   </tr>
  </tbody>
</table>
#### 29.保留两位小数：toFixed(2)
#### 30.filters 自动将(num | filter) 竖线前边的num传入过滤器，并将计算结果返回
{{price | filters}}
filters:{
  showPrices(price){
    return '$' + price.toFixed(2)
  }
}
#### 31.高阶函数filter
const num = [1,2,3,5,6,7,8,9,7]
let newNum = nums.filter(function (n){
  return n < 5
  })
结果 = [1,2,3]
nums.filter(n -> n < 10)
#### 32.map()
const num = [1,2,3,5,6,7,8,9,7]
let newNum = nums.map(function (n){
  return n * 2
  })
结果 = [2,4,6,10...]
nums.map(n -> n * 100)

#### 33.reduce()
const num = [1,2,3,4,5,6]
let num = nums.reduce((pre, n) -> pre + n)

#### 34.v-model双向绑定，用在form表单上,标签和data是双向绑定的，任一端发生改变，两边都会进行修改，与其绑定的v-text或者{{message}} 都会发生改变
<div id='app'>
  <input type='text' v-model='message'>
  {{message}}
</div>
也可以自己实现双向绑定，比如监听输入框的input事件，事件触发之后在回调函数中主动修改data中的值
也可以直接在@input后边使用$event.target.value
#### 35.v-model结合radio类型(圆圈选择)
<label for='male'>
  <input type='radio' id=male> 男
</label>
#### 36.checkbox
<input type= 'checkbox' id = 'agree' v-model='isAgree'>
<h2 >{{message}}</h2>
如果有多个checkbox，那么可以使用数组来进行双向绑定
<input type= 'checkbox' value='篮球' v-model='isAgree'>
<input type= 'checkbox' value = '足球' v-model='isAgree'>
<input type= 'checkbox' value = '乒乓球' v-model='isAgree'>
<input type= 'checkbox' value = '羽毛球' v-model='isAgree'>
data:{
  checkbox:[]
}
#### 37.select
<select v-model = 'fruit'>
  <option value='苹果' >香蕉</option>
  <option value='苹果' >苹果</option>
  <option value='苹果' >香蕉</option>
</select>
data:{
  fruit:''
}

- 同时选择多个的复选框
<select v-model='fruit' multiple>
  <option value='苹果' >苹果</option>
  <option value='苹果' >苹果</option>
  <option value='苹果' >苹果</option>
</select>
data:{
  fruit:[]
}
#### 38.v-on的修饰符
- lazy修饰符加上之后，会使得数据的刷新并不是实时的，而是回车等让input失去焦点的操作，才让变量进行更新
v-on.lazy = ''
<div id='app'>
    <input type='text' v-model.lazt='message'>
    <h2>{{message}}</h2>
</div>
#### 39.v-model绑定的数据默认会绑定成String类型
v-model.number='age' //可以让绑定的数据是number类型
v-model.trim='age' //可与去除前后的空格
#### 40.组件化开发
- 1.创建构造器组件
 const cpnConstructor = Vue.extends({
   template:'<div><h2></h2></div>'
   })
- 2.注册组件
  Vue.component('cpn', cpnConstructor)组件的标签名
- 3.
const app = new Vue({
  el:'#app',
  data:{

  }
  })
- 4.之后就可以全局使用， 自己构建的组件了<cpn></cpn>
#### 41.组件注册的语法糖
直接把template:'<div><h2></h2></div>'}
放到注册阶段的：Vue.component('cpn',{template:'<div><h2></h2></div>'})

#### 42.全局组件和局部组件
40的组件是全局组件，可以在多个vue实例中进行调用，只需要正确实例化了就可以
局部组件：在实例化的过程中进行注册，那么最后也只能在这个组件中用
const app = new Vue(){
  el:'#app',
  data:{
    message:'你好'
  },
  component:{
    cpn:cpnConstructor
  }
}
**注意这些组件只能在id为app的组件内部使用**
#### 43.父组件和字组件
const cpnConstructor = Vue.extends({ //父组件
  template:'<div><h2></h2></div>'
  },
  component:{
    //可以在这进行组件的复用，相当于父子关系了
    cpn1: cpn1Constructor // 子组件
    })

#### 44.模板的分离写法：模板可以拆出来写，然后使用id在原来constructor位置进行注册就行了
- <script type='text/x-template' id='cpn'>
  <div></div>
</script>
- 直接使用<template> 标签
<template id ='cpn'>
  <div>哈哈哈
  </div>
</template>
#### 45.组件可以访问vue实例中的数据？
组件是不可以访问vue实例中的data
组件有地方保存自己的数据：
Vue.component('cpn',{template:'<div><h2></h2></div>',
data(){ //这个data必须是一个函数，而不能是一个对象，如果有多个组件实例，他们并不会共享这其中的数据。如果不用函数的话，而是使用data：那么它们一个更改，其他组件都会更改，也就丧失了组件复用的目的了
  return{
    title:'abc'
  }
  }})
methods也可以有
computed也可以有
#### 46.父子组件之间的通讯
- 在最外层组件发送网络请求
- 通过pass props向子组件传递数据（props数据验证）
在组件标签上使用v-bind绑定，然后在组件定义部分使用props来接收。props：{cmovies:Array} 可以实现对类型的限制，默认值，或者required(必须传个值过来)在element ui中见过
坑：v-bind='myInfo'这是错误的，是不支持驼峰的。 可以使用my-info来对标myInfo
- 通过事件emit events向父组件传递数据（子传父）
#### 47.watch可以监听某个变量的改变
#### 48.this.$chlidren 可以在父组件中访问子组件实例
- 使用this.$chlidren[1]使用索引的方式不太好，因为如果在组件内部添加了其他的组件的话，索引值是会变的
- 所以可以直接给自定义的组件赋予ref属性 <cpn ref = 'aaa'></cpn>
- 然后可以使用this.$refs.aaa来获得该组件，然后就可以获得该组件的内部数据或者方法了
#### 49.this.$parent用来在子组件中访问父组件
- 可以使用this.$root 访问根组件
#### 50.slot插槽，在template定义的时候就直接预留<slot>标签
<template>
  <div>
    <p>这是一个模板，可以在vue实例化的时候，填写在component标签中</p>
    <slot></slot> //在用的时候插入需要的组件就行了，此处插槽里可以写入默认的标签
  </div>
</template>
用法：<cpn><div>啊啊啊啊</div></cpn>
如果要插入多个标签的话，会拿这些标签去替换插槽的位置
#### 61.如果有多个<slot>插槽的话
默认如果传入一个组件的话，这几个<slot>都会被替换
如何让它只替换特定的插槽呢？ <slot name='left'></slot> 给插槽添加name属性就行了。使用的时候<cpn slot='left'>
#### 62.编译的作用域
- 父组件的data和methods只能在它自己的范围内使用，子组件是无法使用的，子组件的data也是只能在自己的范围内使用
- 父组件模板的所有东西都会在父级作用域内编译，子组件模板的所有东西都会在子级作用域内编译
#### 63.作用域插槽（？？？？？）
父组件中有一个子组件，但是并不是一直想使用这个子组件的标签格式，但是又需要子组件中的数据，此时就可以使子组件的样式包裹在<slot :data = 'plange'>插槽中,并使用v-on绑定子组件中的数据。然后在父组件中就可以使用
<div slot-scope='slot'>
  <span v-for='item in slot.data'>{{slot.data}} </span>
<slot>
来完成既使用子组件的数据，但是更新了子组件的样式的目的。
父组件替换插槽的标签，但是内容由子组件来提供
#### 64.多个js文件中同名的变量属于全局变量，会相互影响，通过闭包可以把这些变量限制在自己的作用域内。
#### 65.常见的模块化规范：CommonJS(Node)、AMD、CMD、ES6的Modules
#### 66.ES6中的模块化，使用新增的关键字 export 和 import，如果不使用webpack或者脚手架的话，是只能使用这种方法的。
es6中可以使用如下的方法导出变量
export{
  flag, sum
}
export var num1 = 1000
export var height = 1.88
也可以使用 const{add, mul} = require('./mathUtils.js')

在其他js文件中就可以使用import {num1, height} form'./a.js'
- 函数也可以这样导出和导入
- ES6中类的定义是通过class关键字进行的，在ES5中是使用function来定义的
#### 67.使用export default来导入导出，导出的没有命名，使用的时候可以自己命名
const a = '1'
export default a //只能有一个export default

导入：import aaa from './a.js' //无需写大括号，也可以随便写变量名，因为导出的数据肯定只有一个值
- 使用这种引用方法，必须给<script src='info.js' type='module'></script>
- 如果要一次性全部导入，可以import * as aaa from './a.js'
#### 68.webpack和grunt区别
- 模块化和打包,前端模块化打包工具
- grunt更加强调的是前端流程的自动化，模块化不是它的核心
- webpack更加更加强调模块化开发管理(ES6, commonjs的模块化都可以)，而文件压缩合并、预处理等功能，是他附带的功能
- webpack模块是需要node环境的
- 安装命令：npm -install webpack@3.6.0 -g 进行全局安装，在任何路径下的终端中都有可以用到webpack
#### 69.webpack的使用
- src文件夹：main.js
- dist文件夹：distribution 打包的前端程序
- 打包命令：webpack ./src/main.js .dist/bundle.js (生成的js文件名叫bundle.js )
- 默认如果使用commonjs的require('aa.js')进行模块化的开发，是访问不到js文件的，因为浏览器不认这种语法，但是使用webpack进行一次打包，会自动将commonjs的等的模块语法转为可用的语法，从而可以完成模块化的开发。其他
#### 70.webpack除了使用命令行参数外，还可以使用配置文件
webpack.config.js
step1: 使用npm init命令初始化package.json文件
step2: 在webpack.config.js中写如下代码：
const path = require('path')
module.exports = {
  entry : './src/main.js',
  output : {
    path: path.resolve('__dirname', 'dist')
    filename :'bundle.js'
  }
}
steps: 此时就可以直接使用 webpack命令打包，而不需要69所述的带参数的打包命令进行打包了
#### 71.也可以直接使用nom run build进行打包，但是需要在package.json中进行映射的设置
- 在'scripts'部分添加'build'的命令
- 如'script' : 'webpack ' //优先会使用本项目中的webpack版本
- 运行时是不需要webpack的，他的作用只是在打包的时候用
- 所以可以在开发时安装dev环境下的局部包： npm install webpac@3.6.0 --save-dev,安装成功后，package.json中就会多一个'devDependencies'键值对
devDependencies: {'webpack': '^3.6.0'}
#### 72.如果什么都不设置的话，像webpack这种命令都会使用全局安装的webpack，如果进行了71配置，是会优先使用本地安装的webpack
#### 73.webpack中使用css。也是要将css文件打包到js文件中，也是需要安装一个css loader来打包css文件
step1:根据webpack打包时的文件依赖，从webpack.config.js到main.js,再到被引用模块的js文件中的依赖，所以我们需要首先将css文件在main.js文件中引用
so:在main.js中使用 require('./css/aaa.css') 不予要使用变量来接
step2:此时如果使用npm run build来打包，会报错，提示需要使用合适的loader（官网有说明，css-loader）。
step3：安装css-loader npm install --save-dev css-loader
step4: 在webpack.config.css文件中进行配置
module.exports = {
  entry : './src/main.js',
  output : {
    path: path.resolve('__dirname', 'dist')
    filename :'bundle.js'
  },
  module:{
    rules:{
      test:/\.css$/,    (以.css结尾的文件，.有特定含义，所以需要转义)
      **use:['css-loader']**
    }
  }
}
step5:此时如果使用npm run build打包，之后还是无法访问css（因为css文件只负责加载，不负责解析）
step6：还需要安装一个style-loader
直接在上述use:['style-loader'，'css-loader'] //多个loader是从右向左进行读取的。反过来是会直接在打包的时候报错
#### 74.webpack-less文件的处理
- require('./css/special.less') 如果直接npm run build的话，也会报错，因此需要添加loader
- npm install --save-dev less-loader less （less用来把less转成css）
- 多个loader可以把use弄成一个对象数组
use：[{loader:'style-loader'},
  {loader:'css-loader'},
  {loader:'less-loader'}]
顺序依旧是从右往左
#### 75.webpack的图片
使用css中的url来引用背景图片的话，需要安url-loader
npm install --save-dev url-loader
use: [{
  loader: 'url-loader',
  options:{
    limit: 13000 //单位是kb，如果要显示的图片小于这个值，则会自动转成base64格式，否则的话，会提示需要安装file loader，直接安装一下就行了，不需要配置。然后图片由于需要源文件，所以需要重新打一次包
  }
  }]
打包完之后还是虽然图片进入了dist文件夹，但是还是无法访问到，我们可以在webpack.config.js中output部分进行一个publicpath赋值
output : {
  path: path.resolve('__dirname', 'dist'),
  filename :'bundle.js',
  publicPath: 'dist' //后续所有使用url进行引用的css图片，都会在在写的路径前边拼接一个dist前缀
},
#### 76.图片文件处理
- 修改文件的名称
options:{
  limit:8192,
  name:'img/[name].{hash:8}.{ext}' /img目录下，名称与原来一致，8位hash值，扩展名是原来扩展名
}
#### 77.默认webpack打包不会把ES6转成ES5
那么如何设置可以让其在打包的时候可以自动转成ES5呢？ 使用babel
step1：安装babel对应的loader npm install --save-dev babel-loader@7 babel-core babel-preset-es2015
step2：配置webpack.config.js
use:[loader :'babel-loader',
  options:{preset:['es2015']} //这个就是ES6
  ]
#### 78.webpack配置vue
引用vue的三种方式：
- 直接下载vue.js
- CDN引用
- 使用npm安装引用，安装之后保存在node_modules模块中。npm install vue --save /不加dev的原因，是因为vue不像webpack一样，只在开发环境中使用，上线部署时也是需要依赖vue的。
- 默认会安装最新的vue
#### 79.然后就可以使用vue进行开发了
- import Vue from 'vue'
- 此时的vue是runtime-only版本的，但是此版本内没有compiler可以用于编译template
- 但是runtime-complier，代码中有compiler用于编译template
- 可以在webpack.config.js中的resolve字段中添加
alias:{
  'vue$':'vue/dist/vue.esm.js'
}
- 此时再次使用npm run build就可以直接使用vue了
#### 80.template和el的关系
- 如果el和template同时存在的话，template会把el指向的标签替换掉
#### 81.添加版权的plugin
在module.export{
  plugin:{
    new webpack.BannerPlugin('最终解释权归...所有')
  }
}
然后重新打包就可以在bundel.js开头就能看见自定义的版权信息了
#### 82.html-webpack-plugin 插件:自动生成一个index.html文件，并将打包的js文件，自动通过<script>标签插入到body中
- npm install html-webpack-plugin --save-dev
- 在webpack.config.js中的export module下边的pulgin标签内写new HtmlWebpackPligin(template = 'index.html') //可以指定自动生成的index.html的模板，也可以不指定
- 重新npm run build 之后可以在dist中发现有一个新的index.html文件，这个文件中，自动引入的打包的bundel.js文件
#### 83.js压缩插件 uglyfyjs-webpack-plugin，指定版本号为1.1.1，和cli2保持一致
- npm install uglyfyjs-webpack-plugin@1.1.1 --save-dev
- 然后和上边一样在plugin标签中写new uglyfyJsPlugin()
- 导入使用const uglifyjs-webpack-plugin = require('uglyfyjs-webpack-plugin')
- 然后重新打包后就是已经压缩过的js文件了。
#### 84.webpack-dev-server搭建本地服务器
- npm install --save-dev webpack-dev-server@2.9.1
- devServe:{
  contentBase: './dist',
  inline: true
}
- 如果不是全局安装的，可以在package.json中添加'dev'命令 'dev':'webpack-dev-server --open' 此时的npm run dev就是在本地去寻找webpack-dev-server了
#### 85.webpack配置分离
- 将webpack.config.js 进行拆分，例如开发时 需要一个配置文件，上线时需要另一个配置文件
- 那么可以建立多个xxx.config.js配置文件，公共配置放在base.config.js,其他不同场景下的export module放到不同的配置文件内
- 在打包时需要合并不同的配置文件，需要安装 npm install webpack-merge --save-dev模块
- const webpackMerge = require('webpack-merge')
- module.export = webpackMerge(baseConfig, { // baseConfig也是需要使用require('./baseConfig.js')导入
  plugins:[new webpackMerge()]
  })
- 那么在打包的时候用哪个配置文件呢？ 需要在package.json中script 中的 bulid命令指定命令 'webpack config ./build/prod.config.js'
#### 86.cli的使用
使用vue cli可以快速搭建vue开发环境以及对应的webpack配置，重点是生成webpack配置
#### 87.更换npm淘宝镜像
- npm install -g cnpm -registry=https://registry.npm.taobao.org
- 后续就可以直接使用cnpm进行模块的安装了
#### 88.初始化脚手架
- npm install -g @vue/cli
- 使用vue --version命令可以查看vue cli的版本（？？？？= 。=）
- cli3 可以拉取脚手架2的模板 （为此需要安装 npm install @vue/cli-init -g）
#### 89.分别创建cli2项目和cli3项目
- cli2：vue init webpack my-object  创建过程中选runtime-only，貌似性能会高一些
- cli3：vue create my-object
#### 90.ESlint：用来规范js代码，如果不符合规范的话，webpack自动编译会报错，还是别用了，像是奇怪的 函数名和括号之间必须有一个空格
#### 91.Chrome的v8引擎，可以直接将js代码转成机器码，跳过了字节码的过程
#### 92.runtime-only和runtime-compiler的区别
- runtime-compiler:   template-> ast -> render -> vdom ->UI
- runtime-only :render -> vdom -> UI (步骤更少，性能更强)
#### 93.cli 3.0中public中的图片并不会根据大小来判断转不转base64，而是直接复制到dist中去
#### 94.图形界面 vue ui
#### 95.箭头函数，多用于将函数作为参数传递到函数内部的情况下,例如setTimeout((num1, num2) => return num1 + num2 ,100)
- const a =function (){
  console.log(a)
}
- 转为箭头函数   const ccc = (参数列表) => {
}
- e.g. const sum = (num1, num2) => { return num1 + num2}
- 如果只有一个参数，小括号是可以省略的
- const negtive = num1 => {return -1 * num1}
- 如果函数体内部只有一行代码的话，小括号也是可以省略的
- const sum = (num1, num2) => return num1 + num2
#### 96.箭头函数中的this用法
- 在箭头函数中使用this，打印的是window对象
const obj = {
  aaa(){
      setTimeout( function(){
        console.log(this)
        })
      setTimeout(() => console.log(this)) // 此时返回的是obj对象
  }
}
- 如果在对象中嵌套setTimeout(function(){ return this}) 此时调用会输出window
- 箭头函数中的this，引用的是最近作用域中的this，所以如果上述的function是箭头函数形式的话，返回的是obj
#### 97.路由
路由器属于网络层的设备，使用子网掩码进行公网ip同子网ip的转换
- 前端渲染：随着ajax的出现，有了前后端分离的模式，使得前后端开发分离开来，提升了分工合作的效率，前端人员不需要懂后端代码，更不需要写后端代码，后端只提供数据，前端负责页面显示和数据请求。
- 前端变成三部分: 前端，后端，静态资源服务器
 - 访问过程： url ->静态资源服务器得到html、css等 -> 浏览器渲染 -> 通过ajax请求后端api服务器 -> 动态渲染前端页面 ->访问过程结束
 - 后端注重数据处理，性能优化；前端注重交互及可视化
 - 可以多端请求同一个数据

- 后端渲染：初期阶段主要是后端渲染，jsp、django、flask等等
  - 访问过程： url ->服务器 ->后端路由 ->获取数据 -> 把数据渲染到页面中 ->返回给前端浏览器 ；渲染过程是在后端，返回前端的是插入好数据的html代码
  - 缺点：页面由后端人员嵌入后端语言进行编写的，看起来非常混乱，开发和维护比较麻烦
- 单页面富应用：
  - SPA （single page web application）主要是在前后端分离的基础上加上了一层前端路由，由前端维护了一套路由规则
  - 默认请求时会返回所有的html+js+css代码，而前端路由维护的路由规则，将不同的组件的html+css+js渲染出来，此时页面并不会刷新。不会重新向服务器发送请求
#### 98.url的hash和h5的history
- vue保证url改变,但是页面不刷新的原理：vue-router使用location.hash来进行url的转换，location.hash本质上也是在改变location.href。但是页面不会发生刷新
- 使用h5中的history，可以使用history对象修改url，直接history.pushState({},'','home'),页面url改为了/home ，但是整个页面是不会改变的
 - 这些url会被压入一个栈，使用后退或者使用history.back()将每个url弹出栈
 - history.go(-1) ,展出上一个url，如果是正数的话，会展出后边第n个url
- 直接history.replaceState({}, '','about'),这个是直接替换，是无法返回的
#### 99.安装vue-router
- import VueRouter from 'vue-router'
- import Vue from 'vue'
- 安装插件：Vue.use(VueRouter)
- 创建路由对象 const router =new Router({
   routes //这个也是键值对的形式，相当于routes：routes，这是ES6的一个对象的增强写法
  })
- const routes = []
- 将router传入到vue实例中，需要把router导出，可以使用export default router
- 然后在main.js中直接import router from './router.js'
- 然后添加在
new Vue({
      el:'#app',
      router,
      render: h => h(App)
}).$mount('#app');
中即可
#### 100.使用vue-router
- 创建路由组件:直接通过右键创建填写就可以
- 配置组件和了路径的映射关系：
  - const routes=[{path:'/home',component:}, {path:'lock',component:}]
- 使用路由：通过<router-link>和<router-view>，这两个标签是vue-router中已经注册过的两个组件
  - <router-link to="/home">首页</router-link> //最后会被渲染成a标签
  - <router-link to="/about">首页</router-link>
  - <router-view></router-view> //指定router-link指向的组件显示的位置
#### 101.路由的默认值和修改为history的模式
- 修改项目的首页
const routes=[{path:'',redirect:'/home',component:index}, {path:'/',component:index}]
- 路径后边带个#号，是因为使用了hash值模式，而history模式是不带#的，如何设置呢？
- const router=new VueRouter({
    routes，
    mode:'history' //在此配置history模式
    linkactiveClass: 'active'
});
#### 102.router-link的其他属性
- tag属性:tag='button',tag ='div' ,默认渲染成a标签，如果想要渲染成其他标签的话可以使用tag标签
- replace，只需要写一个单独的replace就可以了，相当于history.repalceState(),使浏览器不能进行返回后退或者前进
- 点击<router-link>之后会给标签添加router-link-active 的class，可以使用这个class进行css编写，以达到点击变色等功能
- router-link-active是可以自定义的，只需要在router-link标签中添加active-class='active'即可
- 如果想对所有的router-link都统一自定义active class，可以在
const router=new VueRouter({
    routes，
    mode:'history'
    linkactiveClass: 'active'
});
#### 103.通过代码跳转路由
- 在监听事件中，使用this.$router.push('/hello') //pushState方式，可以返回
- this.$router.replace('/hello') //replace方式，是不允许返回的
#### 104.vue-router动态路由的使用
- router在定义阶段就const routes=[{path:'',redirect:'/home/:userid',component:index}]
- 然后在<router-link v-bind:to="/home/" + userid >
- 子组件获取如何获得传递的userid呢?
   - this.$route.params.userid //this.$route 拿到的是当前活跃的route
#### 105.路由的懒加载
- 随着组件越来越多，js文件越来越大，如果每次都把所有的js文件加载的话，必将出现页面延迟的情况
- 所以如果我们能把不同路由对应的组件分割成不同的代码块（js）文件中，然后当路由被访问的时候才加载对应组件，这样就更高效了。
- 路由的懒加载就是将路由对应的组件打包成一个一个js代码块
- 只有路由被访问到的时候，才加载对应的组件，使得页面的响应速度变快
- const routes=[{path:'',redirect:'/home',component:() => import('../component/Home')}]
  - 这样只有当该路由被访问的时候才会被加载。build的时候也会被打包成一个个小的js文件
#### 106.路由嵌套
  const routes=[{path:'',redirect:'/home', component:index, chlidren:[
  {
    path:'news', component:'index' //不用加最前边的/
  },
  {
    path:'message',component:()=> import('../component/message')
  }
  ]},
{path:'/',component:index}]
- 之后再使用<router-link to="/home/news">配合<router-view>就可以使用了 ，最前边必须加/否则会直接从原来路由基础上进行拼接
#### 107.vue-router的参数传递
- 动态路由：使用params /router/:id ,跳转时可以使用/router/123, 然后使用this.$route.params.id
- <router-link :to="{path:'/profile', query:{name:'why', age:18, height:1.83}}">
- 此时的url会变成get带参数的方式，用？name=1&height=1.88
- 跳转后的组件使用{$route.query} //显示对象，选择具体属性直接.name 或者.height这样就可以
- 通过代码跳转的话，就是使用this.$router.push/replace(path: '/home', query:{name:'kobe',age:19})
#### 108$router和$route有什么区别
- this.$router 是全局一样的
- 但是this.$route是与当前活跃的组件有关
- Vue.use(Vuerouter),注册全局组件，使得所有的组件都能使用这个对象
- 类似<HomeView></HomeView>这种，可以使用<home-view></home-view>进行代替，是可以的
#### 109.所有的组件都继承自vue的原型
- 所以如果使用Vue.prototype.test = (a,b) => return a + b
- 那么所有的组件都会增加一个test方法
- 属性也是一样的Vue.prototype.name = "张三"。那么所有的组件默认都会增加一个name属性
#### 110.全局导航守卫，来监听组件的跳转
- 原生修改标题的方式:document.title = 'aaa'
- 为了实现点击每个组件实现不同的标题的话，可以在组件的created生命周期的回调函数中进行上述的修改
- 但是总不能每个组件中都写一次。
- 所以其实是可以通过监听组件切换来写一个修改标题的语句，就是全局导航守卫
- router.beforeEach((to, from, next)=>{  //前置钩子
  document.title = to.meta.title //这个meta可以在routes中进行设置
  next() //跳转到to
- 如果是路由嵌套的话，是不能直接使用to.meta获得数据的
  - 而是应该从to.matched[0].meta.name
}
  )
- 还有后置钩子 afterEach(to, from)
#### 111.导航守卫，不同的路由自己是可以独享的
- 就是在定义routes的时候，使用beforeEnter: (to, from, next) =>{

}
  - 这种情况下，只有跳转这个组件才会触发导航守卫的判断
#### 112.vue-router-keep-alive
- 默认情况下，组件之间切换后，组件原来的状态是没有保留下来的，如果重新回到原来的组件，界面会显示默认的初始界面，而这个界面是重新创建的。
- 不同的组件会频繁的创建和销毁，可以使用created和destoryed函数来验证这个行为
- 如果不像让vue重新创建组件的话，就可以设置为keep-alive，使得浏览器得以缓存
- 如果不像让组件频繁重新创建的话，我们可以使用
<keep-alive>
  <router-view/>   //如果没有什么属性或者content的话，我们可以使用单标签形式，看起来更加简洁。使用router-view的话，每个在此位置展示的组件都会保持keep-alive，所以组件都不会频繁地创建和销毁
</keep-alive>
- 但是出现了新的问题：就是当某个组件中有嵌套的子组件的时候，再次切换回来的会后，子组件默认会没有展开，也就是说子组件被隐藏了，这是path路径带来的问题
- 解决方式:
- 跳走之前记录当前组建的path
beforeRouterLeave(to, from, next){
  this.path = this.$router.path
  next()
}
- 再次跳回的时候，跳转到记录的path中
  - actived(){
    this.$router.push(this.path)
  }
- activated和deactivated钩子函数只有在组件被<keep-alive>包裹的时候才有激活和不激活一说，所有只有组件被这两个函数包裹的时候，这两个钩子函数才会有效果
#### 113.<keep-alive>的属性
- 可以使用正则表达式进行匹配
- include = "Profile,home...." // 填写组件的name，name在创建组件的时候可以定义,这里不能随便加空格的
- exclude = ""
#### 114.关于在slot上绑定类
- 在插槽上绑定类最终是不会起效果的，因为插槽后续会被传入的组件所替换掉
- 但是<slot>可以通过v-if来控制其有没有，如果有的话，对应的组件可以替换slot=""属性中对应的插槽
#### 115.路径的别名
- 当组件中调用不同路径下的资源的时候，有可能会出现多次的../../../此时就可以使用别名
  - 例如@可以直接指到src文件夹
  - 也可以自定义别名
  - 在cli2 的webpack.base.conf.js中
  的resolve：{
    alias：{
      '@':resolve('src'),
      'assets':resolve('src/assets') //这里是不能直接使用@的
    }
  }
- 当在import语句中是可以直接使用@开头的
- 但是在标签中例如src ='', 此时需要使用~号开头
#### 116.Promise
- ES6中异步编程的一种解决方案
- 异步请求：我们封装了一个网络请求的函数，但是由于网络请求或者服务器计算的时间，我们并不能立即拿到返回的结果，所以如果采用同步的方式的话，浏览器将卡住。
- 所谓为了保持前端页面还能继续干其他的事情，例如使其他的按钮还能点击，此时我们可以向封装的网络请求的函数中传入另外一个函数，当服务器返回结果有，由这个函数将结果渲染在页面上等
- 这样的函数就称之为回调函数
- 回调地狱：如果在回调函数中又嵌套了新的回调函数，那么将出现回调地狱的问题
- promise就可以使用更加优雅的方式解决这种问题
#### 117.使用Promise
- 模拟网络请求的时间花费
- reslove 和reject；两个本身又是函数
- new Promise((resolve, reject) =>{
    setTimeout(() => console.log('Hello World'), 1000)
  }).then(() => {
    console.log('Hello Python')
    })
#### 118.当有异步操作时，可以使用Promise对这个异步操作进行封装
- new -> 构造函数(1.保存了一些状态信息 2.执行传入的函数)
- new Promise((reslove, reject) => {
    //自己传入的函数
    // 异步操作
    setTimeout((data) => {
      reslove(data) //不要在此对返回的数据进行解析
      //reject('error message')
      }, 1000)
  }).then((data) =>{
    //处理data的代码
    }).catch((err) => {
      console.log(err)
      })
- 也可以再then的时候传入两个函数
- new Promise((resolve, reject) => {
  setTimeout(function(){
    resolve('Hello World')
    reject('Err')
    })
  }).then(data = >{console.log(data)}, error => {console.log(Error)})
#### 119.Promise的三种状态
- sync同步， async异步
- Promise的链式调用
  - 在then中再次return new Promise,然后继续处理then...如果再次进行网络请求的话，还可以继续return new Promise(reslove => {resolve(res + '111')})
  - 简便写法 return Promise.reslove(res +'111')
  - 更简便写法 直接 return res+'111' //内部会对结果进行包装
  - reject方法同理，但是简写的话是throw res + '111'
  - catch(err => console.log(err))
#### 120.Promise.all
- 如果有两个ajax请求，我们需要在两个请求都返回了有调用回调方法
- 思路1：两个全局变量记录两个请求是否都返回了，如果返回了修改对应的全局变量为true，然后判断两个变量是否都为true了，如果都已经成为true了，可以进行下一步操作
- 思路2：使用Promise.all方法，然后传入两个promise对象，对象内部进行网络请求，请求成功后调用resolve方法，当两个对象都调用了resolve方法之后，可以在then(results => {
    console.log(result[0]) //第一次请求的数据
    console.log(result[1]) //第二次请求的数据
  })中进行下一步操作
#### 121.Vuex
- 概念:专门为Vuejs应用程序开发的状态管理模式
- 把需要多个组件共享的变量全部存储在一个对象里面
- 然后把这个对象放在顶层的vue实例中，让其他组件可以使用
- 其实我们可以自己使用Vue.prototype.shareObj = shareObj
- 在其它的组件中也就可以使用this.shareObj.name 这样的方式来使用了
- 那么为什么还有有一个vuex呢？因为上述这种方式的数据并不是响应式的，也就是说如果更改shareObj中数值的话，是不会动态更改的
- 其实自己也是可以通过写逻辑的方式来做到响应式，但是自己封装相对会麻烦一些
- vuex是现成的提供这样一个在多个组件间共享状态的插件，可以直接使用
#### 122.什么样的状态需要vuex进行管理呢
- 多个状态需要在多个页面中共享
- 登录状态，用户名称，头像，地理位置等
- 商品收藏，购物车中加购的物品
- 对于这类的信息，我们可以放在同一的地方，对他们进行保存和管理并且还是响应式的
#### 123.安装vuex
- npm install vuex --save
- 在main.js或者新建一个store/index.js中 import Vue from 'vue'
- import Vuex from 'vuex'
- 全局注册 Vue.use(Vuex)
- 创建vue实例
  - const store = new Vuex.Store({
      state:{
        counter:1000
        },
      mutations:{}
      actions:{},
      getters:{},
      setter:{}
    })
  - export default store
- 然后在main.js中创建vue实例时，进行一下挂载
new Vue({
  el:'#app',
  store,
  render: h => h(App)
  })
- 挂载的过程相当于 Vue.config.$store = store
- 之后我们就可以在其他任意的组件中使用this.$store来获取共享的变量了,并且在mustache语法中是不需要写this的，直接{{$store.state.counter}}
- 如果需要更改state中的值也可以直接用{{$store.state.counter++}}，但是不推荐这样用，因为使用这种方法的话devtool是无法进行状态修改的跟踪的
- 正规的修改方案
  - 在mutation中进行修改
  mutation:{
    incerment(state){
      state.counter++
    }
    decreament(state){
      state.counter--
    }
  }
- 然后直接在@click='$state.commit('increment')'
- 或者写在点击事件的方法内部都可以
- 此时就可以使用devtools对状态的提交进行监控了
#### 124.devtools和mutations合作可以跟踪组件修改状态的行为
#### 125.单一状态树
- 一个项目中state一般只需要使用一个state实例就行了，方便后期管理和维护
#### 126.Getters
- getters类似于computed属性
- getters:{
  pow(state){
    return state.counter * state.counter
  }
}
- 跟computed类似的是，在调用时也不需要使用小括号当做函数来调用，而是使用属性的方式来调用， {{$store.getters.pow}}即可
- getters本身也可以也可以作为参数传入getters内部定义的函数中，来调用内部函数的计算结果，但是不能在函数内部调用它自己。因为环形调用了
#### 127.如果想要通过getters传递参数该怎么办呢？
- 该函数返回一个函数，这个函数可以调用，调用的时候可以传入参数。 好哈哈啊哈哈哈哈
- 返回的函数是持有外层函数传入的state对象的，有点类似于闭包？
#### 128.直接使用delete关键字进行对象内键值对的删除并不是响应式的
- 可以使用Vue.delete(state.info.age)
- Vue.set()//也是响应式的
#### 129函数的变量名在js中其实是可以用变量来表示的
- [name](state){
  state.counter++
}
#### 130.不要在mutation中进行异步操作
- 如果我们确实需要在vuex中进行异步操作的话，可以使用action来替代mutation进行异步操作
