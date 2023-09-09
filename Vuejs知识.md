



# [最全最新Vue、Vuejs教程，从入门到精通](https://www.bilibili.com/video/BV15741177Eh?p=9&spm_id_from=pageDriver)

# 零、ES6语法补充

## 1. 块级作用域

 ES5中的var是没有块级作用域的（if/for）
 ES6中的let是有块级作用域的(if/for)
 ES5之前由于if和for都没有块级作用域的概念，所以在很多时候，我们都必须借助于function的作用域来解决应用外面变量的问题。

建议以后把使用var变量的地方全部换为let

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>

<button>按钮1</button>
<button>按钮2</button>
<button>按钮3</button>

<body>
<script>
  // ES5中的var是没有块级作用域的（if/for）
  // ES6中的let是有块级作用域的(if/for)
  // ES5之前由于if和for都没有块级作用域的概念，所以在很多时候，我们都必须借助于function的作用域来解决应用外面变量的问题。

  // 1.变量作用域:变量再什么范围内是可用的
  // {
  //   var name = ' why';
  //   console.log(name);
  // }
  // //块内，块外皆可以使用
  // console.log(name);

  //2.没有块级作用域引起的问题 if块级
  var func;
  if(true) {
    var name = 'why';

    func = function(){
      console.log(name);
    }

    func()
  }
//这里两个func都可以打印，但是如果在其中一个地方把name修改了，第二个func打印的数据就不对了
  func()

  // 3. 没有块级作用域引起的问题:for的块级
  // 这样i就一直是3
  var btns = document.getElementsByTagName('button');
  for(var i=0;i<btns.length;i++){
      btns[i].addEventListener('click',function(){
        console.log('第' + i + '个按钮被点击');
      })
  }

  //以往解决办法使用闭包
  //为什么闭包可以解决问题:因为函数是一个作用域
  var btns = document.getElementsByTagName('button');
  for(var i=0;i<btns.length;i++){
    (function(i) {
      btns[i].addEventListener('click',function(){
        console.log('第' + i + '个按钮被点击');
      })
    })(i)
  }


  //以下就可以解决问题
  var btns = document.getElementsByTagName('button');
  for(let i=0;i<btns.length;i++){
    btns[i].addEventListener('click',function(){
      console.log('第' + i + '个按钮被点击');
    })
  }
</script>
</body>
</html>
```



## 2. const的使用

建议以后定义变量不需要修改值时候，使用const修饰

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<script>

  //1.注意一: 一旦给const修饰的标识符被赋值之后，不能修改
  const name = 'why';
  name = 'abc';

  //2.注意二: 在使用const定义标识符，必须进行赋值
  const name2;

  //3.注意三:常量的含义是指向的对象不能修改，但是可以改变对象内部的属性
  const obj = {
    name: 'why',
    age:18,
    height: 1.88
  }

  obj.name = 'kobe';
  obj.age = 40;
  obj.height = 1.87;

</script>
</body>
</html>
```

## 3.对象字面量的增强写法

ES6的写法更优美，建议以后使用ES6写法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">{{message}}</div>

<script src="../js/vue.js"></script>

<script>
    // angular(google) ->
    // TypeScript(microsoft) -> ts(类型检测)
    // flow(facebook) ->

    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊',
        }
    })

    //1.属性的增强写法
    const name = 'why';
    const age = 18 ;
    const height  = 1.88

    //ES5的写法
    const obj = {
        name: name,
        age: age,
        height: height
    }

    //ES6的写法
    const obj1 = {
        name,
        age,
        height
    }

    //2.函数的增强写法
    //ES5的写法
    const obj2 = {
        run:function (){

        },
        eat:function (){

        }
    }

    //ES6的写法
    const obj3 = {
        run(){

        },
        eat(){

        }
    }
</script>
</body>
</html>
```



#  一、邂逅Vuejs

## 1.认识Vuejs

### 	1.1 为什么学习Vuejs

  - Vuejs在前端需求中最多，找前端工作必备技能。

### 	1.2  简单认识一下Vuejs

-  vue是一个渐进式框架：可以将Vue作为应用的一部分嵌入，慢慢修改整个项目。 
- 可以不需要具备其他类似Angular、React，甚至jQuery的经验。（但需要一定HTML、CSS、JavaScript基础）
-  Vue有很多特点和web开发中常见的高级功能
   - 解耦视图和数据
   - 可复用的组件
   - 前端路由技术
   - 状态管理
   - 虚拟DOM

## 2.Vuejs安装方式

###  2.1  CDN引入

```html
<!-- 开发环境版本，包含了有帮助的命令行警告 --> <script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
```

```html
<!-- 生产环境版本，优化了尺寸和速度 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2"></script>
```

### 2.2 下载和引入

- 开发环境 https://vuejs.org/js/vue.js
- 生产环境 https://vuejs.org/js/vue.min.js

### 2.3 NPM安装管理

- 后续通过webpack和CLI的使用，使用该方式

## 3. Vuejs初体验

### 3.1 Hello Vuejs

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<!--定义一个容器-->
<div id="app">
    <h2>{{message}}</h2>
    <h3>{{name}}</h3>
</div>

<!--引入vue-->
<!--<script src="../js/vue.js"></script>-->
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
    //let(变量)、const(常量)
    // 编程范式:声明式编程
    const app = new Vue({
        el: '#app',      //用于挂在vue需要管理的对象
        data:{ //定义数据
            message: 'Hello Vuejs',
            name: 'ZYH'
        }
    })

    //原生js做法(编程范式:命令式编程)
    //1.创建div元素，设置id属性

    //2.定义一个变量叫message

    //3.将message变量放在前面的div元素中显示
</script>
</body>
</html>
```



### 3.2 Vue列表展示

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<div id="app">
    <ul>
        <li>{{movies[0]}}</li>
        <li>{{movies[1]}}</li>
        <li>{{movies[2]}}</li>
        <li>{{movies[3]}}</li>
    </ul>

    <ul>
        <li v-for="item in movies">{{item}}</li>
    </ul>

</div>

<!--引入vue-->
<!--<script src="../js/vue.js"></script>-->
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el:'#app',
    data:{
      message : '你好啊',
      movies : ['星际穿越','大话西游','盗梦空间','少年派']
    }
  })
</script>

</body>
</html>
```



### 3.3 案例：计数器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<div id="app">
  <h2>当前计数: {{counter}}</h2>

<!-- v-on监听click事件，当监听到了就计数++或自减-->
<!--  <button v-on:click="counter++">+</button>-->
<!--  <button v-on:click="counter--;">-</button>-->
    <button v-on:click="add">+</button>
    <button v-on:click="sub">-</button>
</div>

<!--引入vue-->
<!--<script src="../js/vue.js"></script>-->
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el:'#app',
    data:{
      counter : 0
    },

    methods:{
        add: function () {
            this.counter++;  //用来找到本对象中的counter，如果直接用counter会找全局变量的counter
            console.log('add被执行');
        },
        sub: function () {
            this.counter--;
            console.log('sub被执行');
        }
    }
  })
</script>
</body>
</html>
```



## 4. Vuejs的MVVM

### 4.1 Vue中的MVVM

- MVVM : Model ViewModel View

- view层
  - 视图层
  - 在我们前端开发中，通常就是DOM层。
  - 主要的作用是给用户展示各种信息。
- Model层
  - 数据层
  - 数据可能是我们固定死的数据，更多是来自我们服务器，从网络上请求下来的数据。
  - 在我们计数器案例中们就是后面抽取出来的obj，当然，里面的数据可能没有这么简单。
- VueModel层：
  - 视图模型层
  - 视图模型层是View和Model沟通的桥梁。
  - 一方面它实现了Data Binding，也就是数据绑定，将Model的改变实时的反应到View中。
  - 另一方面它实现了DOM Listener，也就是DOM监听，当DOM发生一些事件(带年纪、滚动、touch等)时，可以监听到，并在需要的情况下改变对应的Data。

## 5. 创建Vue时, options可以放那些东西

* el: 
  * 类型：string| HTMLElement
  * 作用：决定之后Vue实例会管理哪个DOM
* data:
  * 类型：Object | Function（组件中data必须是一个函数）
  * 作用：Vue实例对应的数据对象。
* methods:
  * 类型：{[key:string]:Function}
  * 作用：定义属于Vue的一些方法，可以在其他地方调用，也可以在指令中使用。
* 生命周期函数



# 二、Vue基础语法

## 1. 插值操作

### 1.1Mustache语法(胡子语法)                          

名字由来：{{}}类似与胡子

特性：

- 不仅可以直接写变量，还可以写简单的表达式
- ＋号连接
- 数值乘除法

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <h2>{{message}}</h2>
  <h2>{{message}},李银河</h2>
<!--  mustache语法中，不仅可以直接写变量，也可以写简单的表达式-->
  <h2>{{firstName + lastName}}</h2>
  <h2>{{firstName + ' ' +lastName}}</h2>
  <h2>{{firstName}} {{lastName}}</h2>
<!--  可以直接乘以2-->
  <h2>{{counter*2}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      firstName: 'kobe',
      lastName: 'bryant',
      counter: 100
    }
  })
</script>
</body>
</html>
```

### 1.2  v-once指令

内容只会改变一次，不会改变第二次。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <h2>{{message}}</h2>
<!--  只会改变一次即可，不会改变第二次-->
  <h2 v-once>{{message}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    }
  })
</script>
</body>
</html>
```

如下对其中message修改了，下面一个还是原来的数据

![image-20211104170242457](C:\Users\haosh\AppData\Roaming\Typora\typora-user-images\image-20211104170242457.png)



### 1.2  v-html指令

可以把字符串中的带标签的文字以html格式解析出来

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <div id = 'app'>
<!--        此时只会把url的字符串显示出来-->
        <h2>{{url}}</h2>
        <h2 v-html="url"></h2>
    </div>

<script src="../js/vue.js"></script>

<script>
    const app = new Vue({
        el: '#app',
        data :{
            message: '你好啊',
            url:'<a href="http://www.baidu.com">百度一下你就知道 </a>'
        }
    })
</script>
</body>
</html>
```

效果如下：

![image-20211104225017699](C:\Users\haosh\AppData\Roaming\Typora\typora-user-images\image-20211104225017699.png)

### 1.3 v-text指令

可以把message数据展示出来，但是一般不会用这个方法，这个方法会把标签体中的数据覆盖了，不像上面的方法可以拼接。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id = 'app'>
  <!--        此时只会把url的字符串显示出来-->
  <h2>{{message}},李银河</h2>
  <h2 v-text = "message">，李银河</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data :{
      message: '你好啊',
      url:'<a href="http://www.baidu.com">百度一下你就知道 </a>'
    }
  })
</script>
</body>
</html>
```

效果如下：

![image-20211104225457396](C:\Users\haosh\AppData\Roaming\Typora\typora-user-images\image-20211104225457396.png)

### 1.4 v-pre指令

使用不多,为了将标签体中数据原封不动的展示出来不进行渲染。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id = 'app'>
  <h2>{{message}},李银河</h2>

<!--  v-pre把标签体中数据原封不动的展示出来-->
  <h2 v-pre>{{message}},李银河</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data :{
      message: '你好啊',
    }
  })
</script>
</body>
</html>
```

效果如下：

![image-20211104225912600](C:\Users\haosh\AppData\Roaming\Typora\typora-user-images\image-20211104225912600.png)

### 1.5 v-cloak指令(斗篷指令)

使用场景，假如vue没有初始化完成前，{{message}}会直接展示在前端，初始化完成之后才会替换，使用v-cloak时候，可以在这个属性里面写隐藏，之后vue初始化完成之后，会取消这个属性。

一般不会用。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
      [v-cloak] {
        display: none;
      }
    </style>
</head>
<body>
<div id="app" v-cloak>
  {{message}}
</div>

<script src="../js/vue.js"></script>

<script>
  //在vue解析之前，div中有一个属性v-cloak
  //在vue解析之后，div中移除v-cloak属性
  setTimeout(function (){
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    }
  })
  },1000)
</script>
</body>
</html>
```



## 2.动态绑定属性

### 2.1 v-bind的基本使用

​	动态绑定之后，可以将imgURL中的链接数据动态解析渲染出来

```html
<!DOCTYPE html>
<html la<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <img v-bind:src="imgURL">
  <a v-bind:href="aURL">百度一下你就知道</a>

<!--  语法糖写法-->
  <img :src="imgURL">
  <a :href="aURL">百度一下你就知道</a>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      imgURL:'https://www.2008php.com/09_Website_appreciate/2010-07-11/20100711232024.jpg',
      aURL:'http://www.baidu.com'
    }
  })
</script>
</body>
</html>g="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <img v-bind:src="imgURL">
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      imgURL:'https://www.2008php.com/09_Website_appreciate/2010-07-11/20100711232024.jpg'
    }
  })
</script>
</body>
</html>
```

### 2.2 v-bind动态绑定class(对象语法)

可以使用class动态绑定，实现对于一些对象的样式控制,主要有一下几种使用方法，其中：是语法糖写法，可以使用v-bind：

```html
用法一：直接通过{}绑定一个类
<h2 :class="{'active': isActive}">Hello World</h2>

用法二：也可以通过判断，传入多个值
<h2 :class="{'active': isActive, 'line': isLine}">Hello World</h2>

用法三：和普通的类同时存在，并不冲突
注：如果isActive和isLine都为true，那么会有title/active/line三个类
<h2 class="title" :class="{'active': isActive, 'line': isLine}">Hello World</h2>

用法四：如果过于复杂，可以放在一个methods或者computed中
注：classes是一个计算属性
<h2 class="title" :class="classes">Hello World</h2>

```

对象语法补充：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .active{
            color: red;
        }
    </style>
</head>
<body>
<div id="app">
    <h2 class="active">{{message}}</h2>
    <h2 :class="active">{{message}}</h2>
<!--    <h2 v-bind:class="{Key1: value1, key2 : value2}">{{message}}</h2>-->
<!--    <h2 v-bind:class="{类名1:true,类名2:boolean}"></h2>-->
    <h2 v-bind:class="{active:isActive, line:isLine}">{{message}}</h2>
    <button v-on:click="btnclick">按钮</button>
</div>

<script src="../js/vue.js"></script>

<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊',
            active: 'active',
            isActive: true,
            isLine: true
        },
        methods:{
            btnclick:function (){
                console.log('111'),
                this.isActive = !this.isActive
            }
        }
    })
</script>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        .active{
            color: red;
        }
    </style>
</head>
<body>
<div id="app">
    <h2 class="active">{{message}}</h2>
    <h2 :class="active">{{message}}</h2>
<!--    <h2 v-bind:class="{Key1: value1, key2 : value2}">{{message}}</h2>-->
<!--    <h2 v-bind:class="{类名1:true,类名2:boolean}"></h2>-->
    <h2 v-bind:class="{active:isActive, line:isLine}">{{message}}</h2>
    <h2 class="title" v-bind:class="getClass()">{{message}}</h2>
    <button v-on:click="btnclick">按钮</button>
</div>

<script src="../js/vue.js"></script>

<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊',
            active: 'active',
            isActive: true,
            isLine: true
        },
        methods:{
            btnclick:function () {
                console.log('111'),
                    this.isActive = !this.isActive
            },
            getClass:function (){
                return {active:this.isActive, line:this.isLine}
            }
        }
    })
</script>
</body>
</html>
```



### 2.3 v-bind动态绑定class(数组语法)

可以使用如下数组语法，但是使用较少

```html
<h2 class="title" v-bind:class="['active','line']">{{message}}</h2>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <h2 class="title" v-bind:class="['active','line']">{{message}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    }
  })
</script>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <h2 class="title" v-bind:class="['active','line']">{{message}}</h2>
  <h2 class="title active line">{{message}}</h2>
    <h2 class="title" v-bind:class='getClass()'>{{message}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
        message: '你好啊',
        active: 'aaaa',
        line:'bbbb'
    },
      methods:{
          getClass : function (){
            return [this.active,this.line]
        }
      }
  })
</script>
</body>
</html>
```

### 2.4 v-bind动态绑定style(对象语法)

这种方法可以有利于之后封装成组件以后，能够通过传参改变样式。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
<!--  <h2 :style="{key(属性名):value(属性值)}">{{message}}</h2>-->
  <h2 :style="{fontSize:'50px'}">{{message}}</h2>
  <h2 :style="{fontSize:finalSize,backgroundColor:finalColor}">{{message}}</h2>
  <h2 :style=getStyles()>{{message}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      finalSize: '100px',
      finalColor: 'red'
    },
    methods:{
      getStyles:function (){
        return {fontSize:this.finalSize,backgroundColor:this.finalColor}
      }
    }
  })
</script>
</body>
</html>
```



### 2.5 v-bind动态绑定style(数组语法)

```html
<h2 :style="[baseStyle,baseStyle1]">
    {{message}}
  </h2>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <h2 :style="[baseStyle,baseStyle1]">
    {{message}}
  </h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      baseStyle: {backgroundColor:'red'},
      baseStyle1: {fontSize:'100px'},
    }
  })
</script>
</body>
</html>
```

## 3:计算属性

### 3.1 计算属性基本使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <h2>{{firstName + ' ' + lastName}}</h2>
  <h2>{{firstName}} {{lastName}}</h2>
  <h2>{{getFullName()}}</h2>
  <h2>{{fullName}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      firstName: 'Lebron',
      lastName: 'James'
    },
    //以下为计算属性
    computed:{
      fullName:function (){
        return this.firstName+' '+this.lastName
      }
    },
    methods:{
      getFullName(){
        return this.firstName+' ' + this.lastName
      }
    }
  })
</script>
</body>
</html>
```

### 3.2 计算属性复杂操作

可以对复杂数据中进行统计等操作

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <h2>总价格: {{totalPrice}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      books: [
        {id:110,name:'Unix编程艺术',price:119},
        {id:111,name:'代码大全',price:105},
        {id:112,name:'深入理解计算机原理',price:98},
        {id:113,name:'现代操作系统',price:87},
      ]
    },
    computed:{
      totalPrice:function (){
        let result = 0;
        for(let i=0;i<this.books.length;i++){
          result+= this.books[i].price
        }
        return result
      }
    }
  })
</script>
</body>
</html>
```

### 3.3 计算属性的setter和geter

​	一般情况下都不写set方法，所以可以用下面第二个简洁的写法来写

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">{{fullName}}</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      firstName: 'kobe',
      lastName: 'Bryant'
    },
    computed:{
      fullName:{
        //1:一般情况下不写set方法，只写get方法即可
        set:function (newValue){
          console.log('使用set方法',newValue);
          const names = newValue.split(' ');
          this.firstName = names[0];
          this.lastName = names[1];
        },
        get:function (){
          return this.firstName + ' ' + this.lastName
        }
      }

      //2:一般不写set时候会有以下更简洁的写法
      // fullname:function (){
      //   return this.firstName + ' '+ this.lastName;
      // }
    }
  })
</script>
</body>
</html>
```

### 3.4  计算属性和methods对比

一般如果只是简单拼接再界面渲染采用属性比较好，使用方法的话，使用几次调用几次，使用属性的话，如果数据没有改变，则会有一个缓存，不会被重复调用，如果其中有for循环的话，使用属性可以大大提高代码运行的效率。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
<!--    1.直接拼接：语法过于繁琐-->
    <h2>{{firstName}} {{lastName}}</h2>
<!--    2.通过定义methods -->
<!--    使用方法时候使用几次调用几次-->
    <h2>{{getFullName()}}</h2>
    <h2>{{getFullName()}}</h2>
    <h2>{{getFullName()}}</h2>
<!--    3.通过属性-->
<!--    使用属性时候不会频繁调用，没有改动不会重复调用，性能会提高很多-->
    <h2>{{fullName}}</h2>
    <h2>{{fullName}}</h2>
    <h2>{{fullName}}</h2>

</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
         message: '你好啊',
        firstName: 'Koba',
        lastName: 'Bryant'
    },
    methods:{
        getFullName:function (){
            return this.firstName + ' ' + this.lastName;
        }
    },
      computed:{
        fullName:function (){
            return this.firstName + ' '+ this.lastName;
        }
      }
  })
</script>
</body>
</html>
```

## 4. 事件监听

###  4.1v-on基本使用

@click是 v-on:click的简便写法，一般建议以后使用@click这种语法糖写法

```html
<button v-on:click="add">+</button>
<!--    <button v-on:click="sub">-</button>-->
<!--    @click是个语法糖-->
<button @click="sub">-</button>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>

<div id="app">
  <h2>当前计数: {{counter}}</h2>

  <!-- v-on监听click事件，当监听到了就计数++或自减-->
  <!--  <button v-on:click="counter++">+</button>-->
  <!--  <button v-on:click="counter--;">-</button>-->
  <button v-on:click="add">+</button>
  <!--    <button v-on:click="sub">-</button>-->
  <!--    @click是个语法糖-->
  <button @click="sub">-</button>
</div>

<!--引入vue-->
<!--<script src="../js/vue.js"></script>-->
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>
<script>
  const app = new Vue({
    el:'#app',
    data:{
      counter : 0
    },

    methods:{
      add() {
        this.counter++;  //用来找到本对象中的counter，如果直接用counter会找全局变量的counter
        console.log('add被执行');
      },
      sub() {
        this.counter--;
        console.log('sub被执行');
      }
    }
  })
</script>
</body>
</html>
</body>
</html>
```

### 4.2 v-on参数

- 当通过methods中定义方法，以供@click调用时，需要**注意参数问题**
- 情况一：如果该方法不需要额外参数，那么方法后的（）可以不添加。
  - 但是注意：如果方法本身中有一个参数，那么默认将原生事件event参数传递进去
- 情况二：如果需要同事传入某个参数，同时需要event时，可以通过$event传入事件。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
<!--  事件调用的方法没有参数-->
  <button @click="btn1Click()">按钮1</button>
  <button @click="btn1Click">按钮2</button>

<!--  在事件定义时，写函数时省略了小括号，但是方法本身是需要一个参数的-->
  <button @click="btn2Click(123)">按钮3</button>
<!--    这个时候传入的会显示undefine-->
  <button @click="btn2Click()">按钮4</button>
<!--    这个时候vue会默认将浏览器生产的event事件对象作为参数传入到方法中-->
  <button @click="btn2Click">按钮5</button>

<!--    方法定义时，我们需要event对象，同事又需要其他参数-->
<!--    在调用方式，如何手动获取到浏览器参数的event对象: $event-->
    <button @click="btn3Click(123,$event)">按钮6</button>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue( {
    el: '#app',
    data:{
      message: '你好啊'
    },
    methods:{
      btn1Click(){
        console.log('btn1_2Click');
      },
      btn2Click(event){
        console.log('--------',event);
      },
      btn3Click(abc,event){
            console.log('+++++',abc,event);
        }
    },

  })
</script>
</body>
</html>
```



### 4.3 v-on修饰符

- 在某些情况下，我们拿到event的目的可能是进行一些事件处理。
- Vue提供了修饰符来帮助我们方便的处理一些事件：
  - .stop：调用event.stopPropagation()
  - .preent：调用event.preventDefault()
  - .{keyCode | keyAlias}:只当事件是从特定键触发时才触发回调。
  - .native：监听组件根元素的原生事件。
  - .once：只触发一次回调。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<div id="app">
<!--    1.  .stop修饰符使用，当点击button时候，阻止divClick被调用，阻止冒泡 -->
    <div @click="divClick">aaaaaaaaaa
        <button @click.stop="btnClick">按钮</button>
    </div>


    <!--    2.  .prevent修饰符的使用,阻止默认时间，比如阻止提交按钮的默认提交事件  -->
   <br>
    <form action = 'baidu'>
        <input type="submit" value="提交" @click.prevent="submitClick">
    </form>

    <!--3. .监听某个键盘的键帽-->
    <input type="text" @keyup.enter="keyUp">

    <!--4. .once修饰符的使用:只触发一次-->
    <button @click.once="btn2Click">按钮2</button>
    
<!--    3.监听某个键盘的键帽点击-->
<!--    <inpt type="text" v-on:keyup="keyUp">-->
<!--        &lt;!&ndash;4. .once修饰符的使用&ndash;&gt;-->
<!--        <button @click.once="btn2Click">按钮2</button>-->

<!--    <inpt type="text" @keyup="keyUp">-->

<!--     <inpt type="text" @keyup.enter="keyUp">-->
</div>


<script src="../js/vue.js"></script>

<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊',
        },
        methods:{
            btnClick(){
                console.log('btnClick');
            },
            divClick(){
                console.log('divClick');
            },
            submitClick(){
                console.log('submitClick');
            },
            keyUp(){
                console.log('keyup');
            }
        }
    })
</script>
</body>
</html>
```



## 5.条件判断

### 5.1 v-if基本使用

可以通过v-if来实现某块区域代码是展示还是不展示

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <button @click="btnClick">是否显示</button>
  <h2 v-if ="isShow">
    <div>1111</div>
    <div>222</div>
    <div>333</div>
    {{message}}
  </h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      isShow: true,
    },
    methods:{
      btnClick(){
        this.isShow = !this.isShow;
      }
    }
  })
</script>
</body>
</html>
```

### 5.2  v-if和v-else使用

可以用来实现，当isShow为true时候渲染一种代码，为false时候显示另一种代码。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <button @click="btnClick">是否显示</button>
  <h2 v-if ="isShow">
    <div>1111</div>
    <div>222</div>
    <div>333</div>
    {{message}}
  </h2>
  <h1 v-else>isShow为false时候，显示这里</h1>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      isShow: true,
    },
    methods:{
      btnClick(){
        this.isShow = !this.isShow;
      }
    }
  })
</script>
</body>
</html>
```



### 5.3  v-if和v-else-if和v-else使用

这种使用比较少，这种逻辑比较复杂的，建议使用计算属性来实现代码如下：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    {{score}}
    <button @click="add">+</button>
    <button @click="sub">-</button>
    <h2 v-if="score>=90">优秀</h2>
    <h2 v-else-if="score>=80">良好</h2>
    <h2 v-else-if="score>=60">及格</h2>
    <h2 v-else>不及格</h2>


<!--    当这种复杂的显示不建议使用v-if，建议使用计算属性-->
    <h1>{{result}}</h1>
</div>

<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el:'#app',
        data:{
            score: 100,
        },
        computed:{
            result(){
                let showMessage = "";
                if(this.score>=90){
                    showMessage = "优秀";
                }else if(this.score>=80){
                    showMessage = "良好";
                }else if(this.score>=60){
                    showMessage = "及格";
                }else {
                    console.log(this.score);
                    showMessage = "不及格";
                }
                return showMessage;
            }

        },
        methods:{
            add(){
                this.score++;
            },
            sub(){
                this.score--;
            }
        }
    })
</script>
</body>
</html>
```

### 5.4 用户登录切换的案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <span v-if="isUser">
    <label for="username">用户账户</label>
    <input type="text" id="username" placeholder="用户账户">
  </span>
  <span v-else>
    <label for="email">用户邮箱</label>
    <input type="text" id="email" placeholder="用户邮箱">
  </span>
  <button @click="isUser = !isUser">切换类型</button>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      isUser: true
    }
  })
</script>
</body>
</html>
```

### 5.5 用户登录切换的案例小问题

小问题描述：

- 如果我们在有输入情况下，切换了类型，我们会发现文字依然显示之前输入的内容。
- 但是按照道理，我们应该切换到另一个input元素中了。
- 在另一个input元素中，我们并没有输入内容。
- 为什么会出现这个问题？

问题解答：

- 这是因为Vue在进行DOM渲染时，出于性能考虑，会竟可能的附庸已经存在的元素，而不是重新创建新的元素。
- 在上面的案例中，Vue内部会发现原来的input元素不在使用，直接作为else中的input来使用了。

解决方案：

- 如果我们不希望Vue出现类似重读利用的问题，可以给对应的input添加key。
- 并且我们需要保证key的不同。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <span v-if="isUser">
    <label for="username">用户账户</label>
    <input type="text" id="username" placeholder="用户账户" key="username">
  </span>
  <span v-else>
    <label for="email">用户邮箱</label>
    <input type="text" id="email" placeholder="用户邮箱" key="email">
  </span>
  <button @click="isUser = !isUser">切换类型</button>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      isUser: true
    }
  })
</script>
</body>
</html>
```

### 5.6 v-show的使用

当需要在显示与隐藏之间切片很频繁时候使用v-for

当只有一次切换时，通过使用v-if

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">

<!--  v-if:当条件为false时，包含v-if指令的元素，根本不会存在dom中-->
  <h2 v-if="isShow" id="aaa">{message}}</h2>

<!--  v-show: 当条件为false时，v-show仅仅是将元素的display属性设置为none时候-->
  <h2 v-show="isShow" id="bbb">{message}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      isShow: true
    }
  })
</script>
</body>
</html>
```

## 6.循环遍历

### 6.1 v-for遍历数组

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">

<!--  1.在遍历过程中，没有使用索引值(下标值)-->
  <ul>
    <li v-for="item in names">{{item}}</li>
  </ul>

<!--  2.在遍历过程中，获取索引值-->
  <ul>
    <li v-for="(item,index) in names">{{index+1}}.{{item}}</li>
  </ul>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      names: ['why','kobe','james','curry']
    }
  })
</script>
</body>
</html>
```

### 6.2 v-for遍历对象

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">

<!--  1.在遍历对象过程中，如果只是或者一个值，那么获取到的是value-->
  <ul>
    <li v-for="item in info">{{item}}</li>
  </ul>

<!--  2.获取key和value格式:(value,key)-->
  <ul>
    <li v-for="(value,key) in info">{{value}}:{{key}}</li>
  </ul>

  <!--  2.获取key和value格式:(value,key,index)-->
  <ul>
    <li v-for="(value,key,index) in info">{{value}}:{{key}}--{{index}}</li>
  </ul>

</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      info:{
        name:'why',
        age:18,
        height:1.88
      }
    }
  })
</script>
</body>
</html>

```

### 6.3 v-for使用过程中添加key

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    //添加key可以使得效率更高
    <ul>
        <li v-for="item in letters" :key="item">{{item}}</li>
    </ul>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      letters:['A','B','C','D']
    }
  })
</script>
</body>
</html>
```

4.12 哪些数组的方法是响应式的

只有通过索引修改数组中元素不是响应式的，所以一般不会用这个办法修改数组中的元素，一般使用的是splice来进行实现一样的功能。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
<!--    //添加key可以使得效率更高-->
    <ul>
        <li v-for="item in letters" :key="item">{{item}}</li>
    </ul>
    <button @click="btnClick">按钮</button>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      letters:['A','B','C','D']
    },
      methods:{
        btnClick(){
            //1.push方法响应式的
            this.letters.push('aaaa');

            //2.pop()可以是响应式的:删除数组中的最后一个元素
            this.letters.pop();

            //3.shift():删除数组中的第一个元素 响应式
            this.letters.shift('aaa','bbbb');


            //4.unshift():在数组最前面添加元素 响应式
            this.unshift('aaaaa','bbbb','ccccc')

            //5.splice():删除元素/插入元素/替换元素
            //splice(start)
            //删除元素:第二个元素参数传入你要删除几个元素(如果没有传，就删除后面所有元素)
            this.letters.splice(1);
            this.letters.splice(1,letters.length());
            //替换元素:第二个参数，表示我们要替换几个元素，后面是用于替换前面的数据
            this.letters.splice(1,3,'m','n','l');
            //插入元素:第二个参数，传入0，并且后面跟上插入元素
            this.letters.splice(1,0,'x','y','z');

            //2.通过索引值修改数组中的元素，没法响应式
            this.letters[0] = 'bbbbbb';
            //由于上面不是响应式的，所以一般不用上面的方法，如果需要则使用splice方法
            this.letters.splice(0,1,'bbb')


        }
      }
  })
</script>
</body>
</html>
<script>
    import Build from "../../资源/Vue笔记/Day 01/Vue源码/vue-2.5.21/packages/vue-server-renderer/build";
    export default {
        components: {Build}
    }
</script>
```

### 6.4 作业回顾和完成

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
  <style>
    .active{
      color: red;
    }
  </style>
</head>
<body>
<div id="app">
  <ul>
    <li v-for="(item,index) in movies" :class="{active:currentIndex == index}" @click="liClick(index)">{{index}}.{{item}}</li>
  </ul>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      movies:['海王','海贼王','加勒比海盗','海尔兄弟'],
      currentIndex:0
    },
    methods:{
      liClick(index){
        this.currentIndex = index;
      }
    }
  })
</script>
</body>
</html>
```

## 7.书籍购物车案例

### 7.1 购物车案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>

<div id="app">
    <div v-if="books.length">
    <table>
        <thead>
        <tr>
            <th></th>
            <th>书籍名称</th>
            <th>出版日期</th>
            <th>价格</th>
            <th>购买数量</th>
            <th>操作</th>
        </tr>
        </thead>

        <tbody>
        <tr v-for="(item,index) in books">
<!--            以下这种写法也可以,但是购买数量进行操作不方便-->
<!--            <td v-for="value in item">{{value}}</td>-->
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.date}}</td>
<!--            //1.方法一-->
<!--            <td>{{getFinalPrice(item.price)}}</td>-->
<!--            //2:使用过滤器-->
            <td>{{item.price | showPrice}}</td>
            <td>
                <button @click="decrement(index)" v-bind:disabled="item.count<=1">-</button>
                {{item.count}}
                <button @click="increment(index)">+</button>
            </td>
            <td><button @click="removeHandle(index)">移除</button></td>
        </tr>
        </tbody>
    </table>
    <h2>总价格:{{totalPrice | showPrice}}</h2>
    </div>
    <h2 v-else>购物车为空</h2>
</div>

<script src="../js/vue.js"></script>
<script src="main.js"></script>

</body>
</html>
```

```js
const app = new Vue({
    el:'#app',
    data: {
        books: [
            {
                id: 1,
                name: '《算法导论》',
                date: '2006-9',
                price: 85.00,
                count: 1
            },
            {
                id: 2,
                name: '《UNIX编程艺术》',
                date: '2006-2',
                price: 59.00,
                count: 1
            },
            {
                id: 3,
                name: '《编程珠玑》',
                date: '2008-10',
                price: 39.00,
                count: 1
            },
            {
                id: 4,
                name: '《代码大全》',
                date: '2006-3',
                price: 128.00,
                count: 1
            },
        ]},
    methods:{
        // getFinalPrice(price){
            // return '￥' + price.toFixed(2);
        decrement(index){
            return this.books[index].count--;
        },
        increment(index){
            return this.books[index].count++;
        },
        removeHandle(index){
            this.books.splice(index,1);
        }
        },
    computed:{
      totalPrice(){
          let totalPrice = 0;
          for(let i=0;i<this.books.length;i++){
              totalPrice += this.books[i].price*this.books[i].count;
          }
          return totalPrice;
      }
    },
        filters:{
            showPrice(price){
                return '￥' + price.toFixed(2);
            }
        }
})
```

```css
table{
    border: 1px solid #e9e9e9;
    border-collapse: collapse;
    border-spacing: 0;
}

th,td{
    padding: 8px 16px;
    border: 1px solid #e9e9e9;
    text-align: left;
}

th {
    background-color: #f7f7f7;
    color: #5c6b77;
    font-weight: 600;
}
```



### 7.2 js高阶函数 

```js
//编程范式:命令式编程/声明式编程
//编程范式:面向对象编程(第一公民:对象)/函数式编程(第一公民:函数)
//filter/map/reduce
// filters中的回调函数有一个要求:必须返回一个boolean值
// true:当返回true时，函数内部会自动将这次回调的n加入到新的数组中
// false: 当返回false时，函数内部会过滤掉这次的n

const nums = [10,20,111,222,444,40,50]

//1.fliter函数使用
let newNums = nums.filter(function(n){
    return n<100;
})
console.log(newNums);

//2.map函数使用
let new2Nums = newNums.map(function (n){
    return n*2;
})
console.log(newNums);

//3.reduce函数的使用
//reduce作用对数组中所有的内容进行汇总
new2Nums.reduce(function (preValue,n){
    return preValue+n;
},0)
```

## 8 v-model使用

### 8.1 v-model基本使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

<div id="app">
    <input type="text" v-model="message">
    {{message}}
</div>

<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊'
        }
    })
</script>

</body>
</html>
```



### 8.2 v-model原理

- 表单控件在实际开发中是非常常见的。特别是对用户信息的提交，需要大量的表单。
- Vue中使用v-mode指令来实现表单元素和数据的双向绑定。

v-model原理：

v-model其实是一个语法糖，它的背后本质上是包含两个操作：

- v-bind绑定一个value属性
- v-on指令给当前元素绑定input事件

也就是说下面代码等同：

```html
<input type="text" v-model="message">
等于
<input type="text" :value="message" @input="message = $event.target.value">
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <input type="text" v-model="message">
  <h2>{{message}}</h2>

  <input type="text" v-bind:value="message" v-on:input="valueChange">
  <h2>{{message}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    },
    methods:{
      valueChange(event){
        this.message = event.target.value;
      }
    }
  })
</script>
</body>
</html>

```

以下不常用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <input type="text" v-model="message">
  <h2>{{message}}</h2>

<!--  <input type="text" v-bind:value="message" v-on:input="valueChange">-->

    <input type="text" :value="message" @input="message = $event.target.value">
    <h2>{{message}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    },
    methods:{
      valueChange(event){
        this.message = event.target.value;
      }
    }
  })
</script>
</body>
</html>

```

### 8.3 v-model结合radio类型的使用

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    <label for="male">
        <input type="radio" id="male" name="sex" value="男" v-model="sex"> 男
    </label>
    <label for="female">
        <input type="radio" id="female" name="sex" value="女" v-model="sex">女
    </label>
    <h2>您选择的性别是:{{sex}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊',
            sex:'男'
        }
    })
</script>
</body>
</html>
```



### 8.4 v-model结合checkbox类型



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
<!--  1.checkbox单选框-->
  <label for="agree">
    <input type="checkbox" id="agree" v-model="isAgree">同意协议
  </label>
  <h2>您选择的是:{{isAgree}}</h2>
  <button :disabled="!isAgree">下一步</button>

<!--  2.checkbox多选框-->
  <input type="checkbox" value="篮球" v-model="hobbies">篮球
  <input type="checkbox" value="足球" v-model="hobbies">足球
  <input type="checkbox" value="乒乓球" v-model="hobbies">乒乓球
  <input type="checkbox" value="羽毛球" v-model="hobbies">羽毛球
  <h2>您的爱好是:{{hobbies}}</h2>
</div>


<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      isAgree:false,  //单选框
      hobbies:[]      //多选框
    }
  })
</script>
</body>
</html>
```

### 8.5 v-model:selsct

和checkbox一样，select也分单选和多选两种情况

单选：只能选中一个值

- v-model绑定的是一个值
- 当我们选中optiop中的一个时，会将它对应的value赋值到mySelect中

多选：可以选中多个值

- v-model绑定的是一个数组
- 当选中多个值时，就会将选中的option对应的value添加到数组mySelects

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
<!--  1.选择一个-->
  <select name="abc" id="" v-model="fruit">
    <option value="苹果">苹果</option>
    <option value="香蕉">香蕉</option>
    <option value="榴莲">榴莲</option>
    <option value="葡萄">葡萄</option>
  </select>
  <h2>您选择的水果是:{{fruit}}</h2>

<!--  2.选择多个,按下ctrl可以选中多个-->
  <select name="abc"  v-model="fruits" multiple>
    <option value="苹果">苹果</option>
    <option value="香蕉">香蕉</option>
    <option value="榴莲">榴莲</option>
    <option value="葡萄">葡萄</option>
  </select>
  <h2>您选择的水果是:{{fruits}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      fruit:'香蕉',
      fruits:[]
    }
  })
</script>
</body>
</html>
```

### 8.6 值绑定

- 我们之前的value中的值都是在定义input中直接定义的
- 但是在真实开发中，这些input的值可能是从网络获取或定义在data中的
- 所以我们可以通过v-bind:value动态给value绑定值

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>

</body>
</html><!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <!--  1.选择一个-->
  <select name="abc" id="" v-model="fruit">
    <option value="苹果">苹果</option>
    <option value="香蕉">香蕉</option>
    <option value="榴莲">榴莲</option>
    <option value="葡萄">葡萄</option>
  </select>
  <h2>您选择的水果是:{{fruit}}</h2>

  <!--  2.选择多个,按下ctrl可以选中多个-->
  <select name="abc"  v-model="fruits" multiple>
    <option value="苹果">苹果</option>
    <option value="香蕉">香蕉</option>
    <option value="榴莲">榴莲</option>
    <option value="葡萄">葡萄</option>
  </select>
  <h2>您选择的水果是:{{fruits}}</h2>

  <label v-for="item in originHobbies" :for="item">
    <input type="checkbox" :value="item" :id="item" v-model="hobbies">{{item}}
  </label>
  <h2>您选择的水果是:{{hobbies}}</h2>
</div>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      fruit:'香蕉',
      fruits:[],
      hobbies:[],
      originHobbies:['篮球','足球','乒乓球','羽毛球','台球','高尔夫球']
    }
  })
</script>
</body>
</html>
```

### 8.7 修饰符

lazy修饰符：

- 默认情况下，v-model默认是input事件中同步输入框的数据的。
- 也就是说，一旦有数据发生改变对应的data中的数据就会自动发生改变
- lazy修饰符可以让数据在失去焦点或回车时才会更新：

number修饰符：

- 默认情况下，在输入框中无论我们输入的是字母还是数字，都会被当做字符串类型进行处理。
- 但是如果我们希望处理的是数字类型，那么最好直接将内容当做数字处理。
- number修饰符可以让在输入框中输入的内容自动转换成数字类型。

trim修饰符：

- 如果输入的诶人首尾有很多空格，通常我们希望将其去除
- trim修饰符可以过滤内容左右两边空格

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>

<div id="app">
  <!--1.修饰符: lazy-->
  <input type="text" v-model.lazy="message">
  <h2>{{message}}</h2>


  <!--2.修饰符: number-->
  <input type="number" v-model.number="age">
  <h2>{{age}}-{{typeof age}}</h2>

  <!--3.修饰符: trim-->
  <input type="text" v-model.trim="name">
  <h2>您输入的名字:{{name}}</h2>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      age: 0,
      name: ''
    }
  })

  var age = 0
  age = '1111'
  age = '222'
</script>

</body>
</html>
```

# 三、组件开发

## 1.组件化实现和使用步骤

组件化是Vue.js中的重要思想

- 它提供了一种抽象，让我们可以开发出一个个独立可复用的小组件来构造我们的应用
- 任何应用都会被抽象成一颗树结构。

组件化思想的应用：

- 有了组件化的思想，我们之后的开发要充分的利用它
- 尽可能将页面拆分成一个个小的、可复用的组件。
- 这样让我们的代码更加方便组织和管理，并且扩展性也更强。

组件使用的三步骤：

- 创建组件构造器：调用Vue.extend()方法创建组件构造器
- 注册组件:调用Vue.component()方法注册组件
- 使用组件:在Vue实例的作用范围内使用组件

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
<!--  <h2>我是标题</h2>-->
<!--  <p>我是内容，哈哈哈哈</p>-->
<!--  <p>我是内容，哈哈哈哈红红火火恍恍惚惚</p>-->

<!--  3.使用组件-->
  <my-cpn></my-cpn>
  <my-cpn></my-cpn>
  <my-cpn></my-cpn>
</div>

<script src="../js/vue.js"></script>

<script>

  //ES6使用`可以实现换行
  // 之前换行
  const str = 'abc' +
          'cde'
  const s = `abc
              cde`
  //1.创建组件构造器对象
  const cpnC = Vue.extend({
    template:`<div>
                <h2>我是标题</h2>
                <p>我是内容，哈哈哈哈</p>
                <p>我是内容，哈哈哈哈红红火火恍恍惚惚</p>
               </div>`
  })

  //2.注册组件
  Vue.component('my-cpn',cpnC)

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    }
  })
</script>
</body>
</html>
```

## 2.全局组件和局部组件

在某个Vue实例下构造的组件是局部组件，一般开发中还是局部组件用的多

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  {{message}}
  <cpn></cpn>
</div>

<script src="../js/vue.js"></script>


<script>
  <!--1.创建组件构造器-->
  const cpnC= Vue.extend({
  template:`
            <div>
                <p>我是标题</p>
                <p>我是内容,hhhhh</p>
            </div>`
  })

  // 2.注册组件（全局组件，以为着可以在多个Vue实例下面使用）
  //   Vue.component('cpn',cpnC)

  //怎么才能是局部组件？   在Vue实例中创建即可

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    },
    components:{
      //cpn使用组件时候标签名字
      cpn: cpnC,
    }
  })
</script>
</body>
</html>
```

## 3.父组件和子组件区分

以下为以前的构造两个组件的使用方法

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  {{message}}
  <cpn1></cpn1>
  <cpn2></cpn2>
</div>

<script src="../js/vue.js"></script>


<script>
  <!--1.创建组件构造器-->
  const cpnC1= Vue.extend({
    template:`
            <div>
                <p>我是标题</p>
                <p>我是内容,hhhhh</p>
            </div>`
  })

  const cpnC2= Vue.extend({
    template:`
            <div>
                <p>我是标题2</p>
                <p>我是内容2,hhhhh2</p>
            </div>`
  })

  // 2.注册组件（全局组件，以为着可以在多个Vue实例下面使用）
  //   Vue.component('cpn',cpnC)

  //怎么才能是局部组件？   在Vue实例中创建即可

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    },
    components:{
      //cpn使用组件时候标签名字
      cpn1: cpnC1,
      cpn2: cpnC2,
    }
  })
</script>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  {{message}}
<!--  <cpn1></cpn1>-->
  <cpn2></cpn2>
</div>

<script src="../js/vue.js"></script>


<script>
  <!--1.创建组件构造器 子组件-->
  const cpnC1= Vue.extend({
    template:`
            <div>
                <p>我是标题1</p>
                <p>我是内容1,hhhhh1</p>
            </div>`
  })

  // 父组件
  const cpnC2= Vue.extend({
    template:`
            <div>
                <p>我是标题2</p>
                <p>我是内容2,hhhhh2</p>
                <cpn1></cpn1>
            </div>`,
    components:{
      cpn1:cpnC1
    }
  })

  // 2.注册组件（全局组件，以为着可以在多个Vue实例下面使用）
  //   Vue.component('cpn',cpnC)

  //怎么才能是局部组件？   在Vue实例中创建即可

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    },
    components:{
      //cpn使用组件时候标签名字
      // cpn1: cpnC1,
      cpn2: cpnC2,
    }
  })
</script>
</body>
</html>
```

## 4.注册组件语法糖写法

上面注册组件方式，可能有些繁琐

- Vue为了简化这个过程,提供了注册语法糖
- 主要是省去了调用Vue.extend()的步骤，而是可以直击使用一个对象来代替

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  {{message}}
  <cpn1></cpn1>
  <cpn2></cpn2>
</div>

<script src="../js/vue.js"></script>

<script>
  // 1.全局组件注册的语法糖

  // 创建组件构造器
  // const cpn1 = Vue.extend({
  //   template:`
  //           <div>
  //               <p>我是标题1</p>
  //               <p>我是内容1,hhhhh1</p>
  //           </div>`
  // })

  // 注册全局组件语法糖
  Vue.component('cpn1',{
    template: `
             <div>
                <p>我是标题1</p>
                <p>我是内容1,hhhhh1</p>
            </div>
    `
  })

  //注册局部组件的语法糖
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    },
    components: {
      'cpn2': {
        template:`
            <div>
                <h2>我是标题2</h2>
                <p>我是内容2，哈哈哈哈</p>
            </div>
            `
    }
  }
  })
</script>
</body>
</html>
```

## 5. 组件模板抽离写法

```html
<!--1.script标签 注意类型必须是：text/x-template-->
<!--<script type="text/x-template" id="cpn1">-->
<!--  <div>-->
<!--    <h2>我是标题</h2>-->
<!--    <p>我是内容aaaa</p>-->
<!--  </div>-->
<!--</script>-->

<!--2.template标签-->
<template id="cpn1">
  <div>
    <h2>我是template标题</h2>
    <p>我是内容哈哈哈哈</p>
  </div>
</template>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  {{message}}
  <cpn></cpn>
</div>

<!--1.script标签 注意类型必须是：text/x-template-->
<!--<script type="text/x-template" id="cpn1">-->
<!--  <div>-->
<!--    <h2>我是标题</h2>-->
<!--    <p>我是内容aaaa</p>-->
<!--  </div>-->
<!--</script>-->

<!--2.template标签-->
<template id="cpn1">
  <div>
    <h2>我是template标题</h2>
    <p>我是内容哈哈哈哈</p>
  </div>
</template>


<script src="../js/vue.js"></script>

<script>

  // 1.注册一个全局组件
Vue.component('cpn',{
  template:'#cpn1'
})

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    }
  })
</script>
</body>
</html>
```



## 6. 为什么组件中data会是函数？



如果不是函数的话，组件复用时候，会互相影响。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">{{message}}
  <cpn></cpn>
</div>

<template id="cpn">
  <div>我是组件
    <button @click="increment">+</button>
    总计数是:{{counter}}
    <button @click="decrement">-</button>
  </div>
</template>
<script src="../js/vue.js"></script>

<script>
  // 1.注册组件
  Vue.component('cpn',{
  template:'#cpn',
    data(){
    return {
      counter : 0
    }
    },
    methods:{
    increment(){
      this.counter++;
    },
      decrement(){
      this.counter--;
      }
    }
  })

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
    }
  })
</script>
</body>
</html>
```

## 7. 父子组件的通信

在开发中，往往一些数据需要从上层传递到下层：

- 比如一个页面中，我们从服务器请求到很多的数据
- 其中一部分数据，并非是我们整个组件打大组件来展示的，而是需要下面的子组件进行展示。
- 这个时候，并不会让子组件再次发送一个网络请求，而是直接让大组件（父组件）将数据传递给小组件（子组件）。

如何进行父子组件间的通信呢？

- 通过props向子组件传递数据
- 通过事件向父组件发送消息

![image-20211112173913252](C:\Users\haosh\AppData\Roaming\Typora\typora-user-images\image-20211112173913252.png)



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    {{message}}
    <cpn v-bind:cmovies = "movies" :cmessage="message"></cpn>
</div>

<template id = "cpn">
    <div>
        <p>{{cmovies}}</p>
        <p>{{cmessage}}</p>
        <ul>
            <li v-for="item in cmovies">{{item}}</li>
        </ul>
    </div>
</template>

<script src="../js/vue.js"></script>

<script>
    //父传子：props
    const cpn = {
        template:'#cpn',
        // props:['cmovies','cmessage'],
        props:{
            //1.类型限制
          // cmovies:Array,
          // cmessage:String,

            // 2.提供一些默认值
            cmessage:{
              type:String,
                default: 'aaaaa',
                required:true
            }
        },
        data(){

            return {}
        },
        methods:{

        }
    }

    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊',
            movies: ['海王','海贼王']
        },
        components:{
            cpn
        }
    })
</script>
</body>
</html>
```

## 8. 父传子(props中驼峰标识)

```html
<!--  //只能用cinfo，vue在v-bind中不支持驼峰标识-->
<!--  //cInfo得转换成c-Info才能识别使用-->
```

```cpp
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  {{message}}
<!--  //只能用cinfo，vue在v-bind中不支持驼峰标识-->
<!--  //cInfo得转换成c-Info才能识别使用-->
  <cpn :cinfo="info"></cpn>
</div>

<template id="cpn">
  <h2>{{cinfo}}</h2>
</template>

<script src="../js/vue.js"></script>

<script>
  const cpn = {
    template: '#cpn',
    props : {
      cinfo: {
        type: Object,
        default(){
          return {}
        }
      }
    }
  }
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      info: {
        name: 'why',
        age: 18,
        height: 1.88
      }
    },
    components: {
      cpn
    }
  })
</script>
</body>
</html>
```

## 9.子传父（自定义事件）

子传父通过自定义事件传递，注意发送的信号不能用驼峰标识

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  {{message}}
  <!--  //只能用cinfo，vue在v-bind中不支持驼峰标识-->
  <!--  //cInfo得转换成c-Info才能识别使用-->
  <cpn @itemclick = "cpnClick"></cpn>

</div>

<template id="cpn">
<!--  <h2>{{cinfo}}</h2>-->
  <div>
    <button v-for="item in categories"
            @click="btnClick(item)">
             {{item.name}}
    </button>
  </div>

</template>

<script src="../js/vue.js"></script>

<script>
  const cpn = {
    template: '#cpn',
    data() {
      return {
        categories: [
          {id: 'aaa', name: '热门推荐'},
          {id: 'bbb', name: '手机数码'},
          {id: 'ccc', name: '家用家电'},
          {id: 'ddd', name: '电脑办公'}
        ]
      }
    },
    methods:{
      btnClick(item){
        console.log(item);
        this.$emit('itemclick')
      }
    },
    props : {
      cinfo: {
        type: Object,
        default(){
          return {}
        }
      }
    }
  }
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      info: {
        name: 'why',
        age: 18,
        height: 1.88
      }
    },
    components: {
      cpn
    },
    methods: {
      cpnClick(){
        console.log("父亲接受到");
      }
    }
  })
</script>
</body>
</html>
```

## 10.组件通信-父子组件通信案例



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
    {{message}}
    <cpn :number1="num1"
         :number2="num2"
         @num1change = "num1change"
         @num2change = "num2change"
    ></cpn>
</div>

<template id="cpn">
    <div>
        <h2>props:{{number1}}</h2>
        <h2>data:{{dnumber1}}</h2>
<!--        <input type="text" v-model="dnumber1">-->
        <input type="text" v-model="dnumber1" @input="num1Input">
        <h2>props:{{number2}}</h2>
        <h2>data:{{dnumber2}}</h2>
<!--        <input type="text" v-model="dnumber2">-->
        <input type="text" v-model="dnumber2" @input="num2Input">
    </div>
</template>

<script src="../js/vue.js"></script>

<script>
    // angular(google) ->
    // TypeScript(microsoft) -> ts(类型检测)
    // flow(facebook) ->

    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊',
            num1:1,
            num2:2
        },
        methods: {
            num1change(value){
                // this.num1 =value * 1;
                this.num1 =parseInt(value);
            },
            num2change(value){
                this.num2 = value * 1;
            }
        },
        components: {
            cpn:{
                template : "#cpn",
                props:{
                    number1:Number,
                    number2:Number
                },
                data() {
                    return {
                        dnumber1: this.number1,
                        dnumber2: this.number2
                    }
                },
                methods:{
                    num1Input(event){
                        // 1.将input中的value赋值到dnumber中
                        this.dnumber1 = event.target.value;

                        //2.为了让父组件可以修改值,发出一个事件
                        this.$emit('num1change',this.dnumber1);

                        // 3.同时修饰dumber2的值
                        this.dnumber2 = this.dnumber1 * 100;
                        this.$emit('num2change',this.dnumber2);
                    },
                    num2Input(event){
                        this.dnumber2 = event.target.value;
                        this.$emit('num2change',this.dnumber2)

                        // 3.同时修饰dumber2的值
                        this.dnumber1 = this.dnumber2 / 100;
                        this.$emit('num1change',this.dnumber1);
                    }
                }
            }
        }
    })

    //1.属性的增强写法
    const name = 'why';
    const age = 18 ;
    const height  = 1.88

    //ES5的写法
    const obj = {
        name: name,
        age: age,
        height: height
    }

    //ES6的写法
    const obj1 = {
        name,
        age,
        height
    }

    //2.函数的增强写法
    //ES5的写法
    const obj2 = {
        run:function (){

        },
        eat:function (){

        }
    }

    //ES6的写法
    const obj3 = {
        run(){

        },
        eat(){

        }
    }
</script>
</body>
</html>
```



## 11.组件通信-父子组件通信（watch实现）

 ```html
 <!DOCTYPE html>
 <html lang="en">
 <head>
   <meta charset="UTF-8">
   <title>Title</title>
 </head>
 <body>
 
 <div id="app">
   <cpn :number1="num1"
        :number2="num2"
        @num1change="num1change"
        @num2change="num2change"/>
 </div>
 
 <template id="cpn">
   <div>
     <h2>props:{{number1}}</h2>
     <h2>data:{{dnumber1}}</h2>
     <input type="text" v-model="dnumber1">
     <h2>props:{{number2}}</h2>
     <h2>data:{{dnumber2}}</h2>
     <input type="text" v-model="dnumber2">
   </div>
 </template>
 
 <script src="../js/vue.js"></script>
 <script>
   const app = new Vue({
     el: '#app',
     data: {
       num1: 1,
       num2: 0
     },
     methods: {
       num1change(value) {
         this.num1 = parseFloat(value)
       },
       num2change(value) {
         this.num2 = parseFloat(value)
       }
     },
     components: {
       cpn: {
         template: '#cpn',
         props: {
           number1: Number,
           number2: Number,
           name: ''
         },
         data() {
           return {
             dnumber1: this.number1,
             dnumber2: this.number2
           }
         },
         watch: {
           dnumber1(newValue) {
             this.dnumber2 = newValue * 100;
             this.$emit('num1change', newValue);
           },
           dnumber2(newValue) {
             this.number1 = newValue / 100;
             this.$emit('num2change', newValue);
           }
         }
       }
     }
   })
 </script>
 
 </body>
 </html>
 ```

## 12.父访问子-children-refs

父子组件的访问方式：`$children`

- 有时候我们需要父组件直接访问子组件，子组件直接访问父组件，或者子组件访问根组件
  - 父组件访问子组件：使用`$children`或`$refs reference(引用)`
  - 子组件访问父组件：使用`$parent`
- 我们先来看看`$children` 的访问
  - `this.$children`是一个数组类型，它包含所有子组件对象。
  - 我们这里通过一个遍历，去除所有子组件的message状态



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <cpn></cpn>
  <cpn></cpn>
  <cpn ref="aaa"></cpn>

  <button @click="btnClick">按钮</button>
</div>
<template id="cpn">
  <h2>子组件</h2>
</template>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el:'#app',
    data:{
      message:'你好啊'
    },
    methods:{
      btnClick(){
        // 1.$children用的比较少
        // console.log(this.$children);
        // this.$children[0].showMessage();
        // for (let c of this.$children){
        //   console.log(c.name);
        //   c.showMessage();
        // }

        //2.$refs 用的最多：对象类型，默认是空的
        console.log(this.$refs.aaa.name);
      }
    },
    components:{
      cpn:{
        template:'#cpn',
        data(){
          return {
            name: '我是子组件的name'
          }
        },
        methods: {
          showMessage(){
            console.log('showMessage');
          }
        }
      },
    }
  })
</script>
</body>
</html>
```

## 13.子访问父

​		一般使用很少，会破坏耦合性

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>

<div id="app">
  <cpn></cpn>
</div>

<template id="cpn">
  <div>
    <h2>我是cpn组件</h2>
    <ccpn></ccpn>
  </div>
</template>

<template id="ccpn">
  <div>
    <h2>我是子组件</h2>
    <button @click="btnClick">按钮</button>
  </div>
</template>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      cpn: {
        template: '#cpn',
        data() {
          return {
            name: '我是cpn组件的name'
          }
        },
        components: {
          ccpn: {
            template: '#ccpn',
            methods: {
              btnClick() {
                // 1.访问父组件$parent
                // console.log(this.$parent);
                // console.log(this.$parent.name);

                // 2.访问根组件$root
                console.log(this.$root);
                console.log(this.$root.message);
              }
            }
          }
        }
      }
    }
  })
</script>

</body>
</html>
```

# 四、组件开发高级

## 1. slot插槽的基本使用

- slot翻译为插槽

  - 在生活很多地方都有插槽，电脑的USB插槽，插线板中的电影插槽。
  - 插槽的目的是让我们原来的设备具有更多的扩展性。
  - 比如电脑的USB我们可以插入U盘、硬盘、手机、音响、键盘、鼠标等。

- 组件的插槽：

  - 组件的插槽也是为了让我们封装的组件更加具有扩展性。
  - 让使用者可以决定组件内部的一些内容到底展示什么。

- 栗子：移动网站中的导航栏

  - 移动开发中，几乎每个界面都有导航栏。
  - 导航栏我们必然会封装成一个插件，比如nav-bar组件。
  - 一旦有了这个组件，我们就可以在多个界面复用了。

  

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <cpn><button>按钮</button></cpn>
  <cpn><p>hhhhhh</p></cpn>
</div>

<!--1.插槽基本使用<slot></slot>-->
<!--2.插槽的默认值<slot><button></button></slot>-->
<!--3.如果有多个值，同时放入组件进行替换时，一起作为替换元素-->

<template id="cpn">
  <div>
    <h2>我是组件</h2>
    <slot></slot>
<!--    加入默认值-->
    <slot><button></button></slot>
<!--    <button>按钮</button>-->
  </div>
</template>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el:'#app',
    data:{
      message:'你好啊',
    },


    components: {
      cpn:{
        template: '#cpn',
      }
    }

  })
</script>

</body>
</html>
<script>
  import Scroll from "../../资源/vuejs资料和代码/Day 08/预习代码/mall/src/components/common/scroll/Scroll";
  export default {
    components: {Scroll}
  }
</script>
```

## 2. 具名插槽使用

给插槽指定名字，指定替换相应的插槽

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <cpn><button slot="center">按钮</button></cpn>

</div>

<!--1.插槽基本使用<slot></slot>-->
<!--2.插槽的默认值<slot><button></button></slot>-->
<!--3.如果有多个值，同时放入组件进行替换时，一起作为替换元素-->

<template id="cpn">
  <div>
    <h2>我是组件</h2>
    <slot name="left"><span>我是左边</span></slot>
    <!--    加入默认值-->
    <slot name="center"><span>我是中间</span></slot>
    <slot name="right"><span>我是右边</span></slot>
    <!--    <button>按钮</button>-->
  </div>
</template>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el:'#app',
    data:{
      message:'你好啊',
    },


    components: {
      cpn:{
        template: '#cpn',
      }
    }

  })
</script>

</body>
</html>

```

## 3. 编译作用域的概念



```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
<div id="app">
  <cpn v-show="isShow"></cpn>

</div>

<!--1.插槽基本使用<slot></slot>-->
<!--2.插槽的默认值<slot><button></button></slot>-->
<!--3.如果有多个值，同时放入组件进行替换时，一起作为替换元素-->

<template id="cpn">
  <div>
    <h2>我是组件</h2>
    <button v-show="isShow"></button>
  </div>
</template>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el:'#app',
    data:{
      message:'你好啊',
      isShow:true
    },


    components: {
      cpn:{
        template: '#cpn',
        data(){
          return {
            isShow:false
          }
        }
      }
    }

  })
</script>

</body>
</html>

```

## 4.作用域插槽

一句话总结就是：

- 父组件替换插槽的标签，但是内容由子组件提供

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<div id="app">
  <cpn></cpn>
  <cpn>
<!--    目的是获取子组件中的pLagnguages-->
    <template slot-scope="slot">
      <span v-for="item in slot.data">{{item}} -</span>
    </template>
  </cpn>
</div>
<template id="cpn">
  <div>
    <slot :data="pLanguages">  这是一个子组件
      <ul>
        <li v-for="item in pLanguages">{{item}}</li>
      </ul>
    </slot>
  </div>
</template>

<script src="../js/vue.js"></script>

<script>
  const app = new Vue({
    el:'#app',
    data:{
      message:'你好啊',
    },
    components: {
      cpn:{
        template: '#cpn',
        data(){
          return {
            pLanguages: ['JavaScript','C++','Java','C#','Python','Go']
          }
        }
      }
    }

  })
</script>
</body>
</html>
```



## 5.ES6导入导出语法

```js
// 1.导入的{}中定义的变量
import {flag, sum} from "./aaa.js";

if (flag) {
  console.log('小明是天才, 哈哈哈');
  console.log(sum(20, 30));
}

// 2.直接导入export定义的变量
import {num1, height} from "./aaa.js";

console.log(num1);
console.log(height);

// 3.导入 export的function/class
import {mul, Person} from "./aaa.js";

console.log(mul(30, 50));

const p = new Person();
p.run()

// 4.导入 export default中的内容
import addr from "./aaa.js";

addr('你好啊');

// 5.统一全部导入
// import {flag, num, num1, height, Person, mul, sum} from "./aaa.js";

import * as aaa from './aaa.js'

console.log(aaa.flag);
console.log(aaa.height);


```

# 五、webpack相关

## 1.webpack安装

- 安装webpack首先需要安装Node.js,Node.js自带了软件包的管理工具

- 查看自己的node版本

  ` node -v` 

- 全局安装webpack(这里我先指定版本号3.6.0，因为vue cli2依赖该版本，可以看到内部的依赖关系)

  `npm install webpack@3.6.0 -g`

- 局部安装webpack(后续才需要)

  - `--save-dev` 是开发时依赖，项目打包后不需要继续使用的。

  ```
  cd 对应目录
  npm install webpack@3.6.0 --save-dev
  ```

- 为什么全局安装后，还需要局部安装呢
  - 在终端直接执行webpack命令，使用的全局安装的webpack
  - 当在package.json中定义了scripts时，其中包含了webpack命令。





## 2.webpack起步

- 我们创建如下文件和文件夹：

- **文件和文件夹解析：**
  - dist文件夹：用于存放之后打包的文件
  - src文件夹：用于存放我们写的源文件
  -  main.js：项目的入口文件。具体内容查看下面详情。
  - mathUtils.js：定义了一些数学工具函数，可以在其他地方引用，并且使用。具体内容查看下面的详情。

- index.html：浏览器打开展示的首页html

- package.json：通过npm init生成的，npm包管理的文件（暂时没有用上，后面才会用上）

- mathUtils.js文件中的代码：

```js
function add(num1,num2){
    return num1+num2
}

function mul(num1,num2){
    return num1 * num2
}

module.exports = {
    add,
    mul
}
```

- main.js文件中的代码：

  ```js
  //1.使用commonjs的模块化规范
  const {add,mul} = require('./mathUtils.js')
  
  console.log(add(20, 30));
  console.log(mul(20, 30));
  
  //2.使用ES6的模块化的规范
  import {name,age,height} from "./info.js";
  
  console.log(name);
  console.log(age);
  console.log(height);
  ```

- 如何打包呢？使用webpack的指令即可

![image-20211123212710362](C:\Users\haosh\AppData\Roaming\Typora\typora-user-images\image-20211123212710362.png)

![image-20211123212716432](C:\Users\haosh\AppData\Roaming\Typora\typora-user-images\image-20211123212716432.png)









# 四、Vue CLI详解





# 五、Vue-router



# 六、Vuex详解



# 七、网络封装



# 八、项目实战



# 九、项目部署



# 十、vuejs原理相关

