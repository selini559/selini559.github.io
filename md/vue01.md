# 🌄vue01

## 🏝️一、vue概念

### 🏷️1. 渐进式框架

渐进式：逐渐使用，集成更多功能

想用什么就添加什么，不必全部使用

## 🏝️二、脚手架项目创建

### 🏷️1. **@vue/cli**脚手架

#### 1.1 安装脚手架

全局安装（推荐使用镜像安装）

```
npm install -g @vue/cli
```

安装成功后查看版本

```
vue -V
```

#### 1.2 创建项目

vuecli-demo是项目名，命名时不能有大写字母，中文和特殊符号

```
vue create vuecli-demo
```

创建成功后项目目录

主要文件

> node_modules - 第三方包 可以通过npm install下载，一般不会做为拷贝对象 public/index.html – 浏览器运行的网页 src/main.js – webpack打包的入口js文件 src/App.vue – vue项目入口vue页面 package.json – 依赖包列表文件

#### 1.3 eslint

**作用：代码规范**

举个例子🌰：声明了一个变量却没有使用则会报错

**解决方法**：

- 手动解决掉错误

- 暂时关闭eslint检查 - 在vue.config.js中配置后重启服务
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6e024bd14cc1405f9e02c93ce36e3027~tplv-k3u1fbpfcp-watermark.image?)
- 单行注释

    ```
    // 1. 下一行不进行监测
    // eslint-disable-next-line
    let a = 123
    
    // 2. 同一行不进行监测
    let a = 123 // eslint-disable-line
    ```

- 多行注释

    ```
    /* eslint-disable */
    let a = 123
    /* eslint-enable */
    ```

## 🏝️三、❣️VUE❣️

### 🏷️1. 插值表达式

#### 1.1 语法

相当于原生js里的修改标签内容

```
<h1>{{ 表达式( > < >= == === ! && || 三目运算 变量 ) }}</h1>
```

#### 1.2 例子🌰

```
<div>{{ 1 + 1 }}</div>
<div>{{ 1 === 2 }}</div>
```

页面显示


![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/17a5f536669e4b959231281d8fdaed9c~tplv-k3u1fbpfcp-watermark.image?)

#### 1.3 变量

一个vue文件中声明的变量需要放置在data函数的return对象上

```
<script>
export default {
  name: 'demo-01',
  data () {
    return {
      msg: '插值表达式',
      obj: {
        name: '张三',
        age: 10
      }
    }
  }
}
</script>
```

再把值赋到标签

```
<div>{{ msg }}</div>
<div>{{ obj.name }}</div>
<div>{{ obj.age >= 18 ? '成年' : '未成年' }}</div>
```

页面显示

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d74bdf9674b84ddd87e70bda0a9ca29c~tplv-k3u1fbpfcp-watermark.image?)
#### 1.4 引入

vue文件写好后，要想显示在浏览器上，还需要引入到**APP.vue**文件里


![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4ee996279e674c0f960f6474a5ebec18~tplv-k3u1fbpfcp-watermark.image?)

**引入步骤**：

> 0.  通过import ‘引入’ 组件,并为组件起一个自定义名称
> 0.  通过components属性进行组件的 ‘注册’
> 0.  在template标签内，以标签的形式继续 ‘使用’

### 🏷️2. ❣️vue的MVVM设计模式❣️

当我们在浏览器修改了data中的某个数据时， vue可以帮助我们在数据修改的同时，页面上的相应部分也会做出改变


![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d1e44eb92ff0499e9cd33cf3a4728f25~tplv-k3u1fbpfcp-watermark.image?)


![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c4f4b98556a446d8aa3a392e742d8b0e~tplv-k3u1fbpfcp-watermark.image?)

#### 2.1 MVVM是什么

MVVM，一种软件架构模式，决定了写代码的思想和层次

-   M： model数据模型 (data里定义)
-   V： view视图 （html页面）
-   VM： ViewModel视图模型 (vue.js源码)

MVVM通过**数据双向绑定**让数据自动地双向同步 **不再需要操作DOM**

-   V（修改视图） -> M（数据自动同步）
-   M（修改数据） -> V（视图自动同步）

#### 2.2 ❣️重点问题

**问：** 简单描述一下vue的设计模式

**答：**

vue使用的是MVVM设计模式。MVVM是Model-View-ViewModel缩写，也就是把MVC中的Controller演变成ViewModel。

Model层代表数据模型，View代表UI组件，ViewModel是View和Model层的桥梁，

数据会绑定到viewModel层并自动将数据渲染到页面中，视图变化的时候会通知viewModel层更新数据。（数据双向绑定）

### 🏷️3. v-bind (动态属性)

#### 3.1 语法

-   语法：`v-bind:属性名="vue变量"`
-   简写：`:属性名="vue变量"`

```
<a v-bind:href="url">百度1</a>
<a :href="url">百度2</a>
```

#### 3.2 动态属性的特例

在使用动态属性渲染图片时，*不可以直接将变量的值设置为路径*

原因： v-bind会把这个路径认为是字符串

解决方案：

- 通过 import 的方式引入图片并且赋值给data中的变量

    ![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4a910f4fddc84db5b33871ee0a3cee6e~tplv-k3u1fbpfcp-watermark.image?)

- 通过 require 的方式引入图片并赋值给data中的变量

    

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8376477891714884a5d1e4728d59524b~tplv-k3u1fbpfcp-watermark.image?)

#### 3.3 ❣️重点问题2

**问：** 以上两种解决方案，你觉得哪一个更好呢？？

**答：** require 的引入方式更为友好。 当一个vue文件被使用时，那么既然是js代码，那么遵循从上往下依次执行，import中引入的图片就会在页面渲染初期被加载，而require引入的图片，只有在使用的时候才会被加载，初次开启页面会显得更加的高效

### 🏷️4. v-on（事件绑定）

#### 4.1 语法

等同于原生js事件绑定的 *dom元素.addEventListener*

-   v-on:事件名="要执行的==少量代码==" *（尽量不要这么写）*
-   v-on:事件名="methods中的函数"
-   v-on:事件名="methods中的函数(实参)"

简写:

-   @事件名="methods中的函数(实参)"

```
<div>当前数字{{ count }}</div>
<button v-on:click='count++'>点击+1</button>
```

#### 4.2 methods中的函数

在methods里定义这个vue文件要用到的方法

举个例子🌰：

```
methods: {
    addFn(){
      this.count+=2
    },
    addFn2(num){
      this.count+=num
    }
  }
```

在标签里写函数名的时候，一定要 **CV** !手写总会有疏忽的时候，CV肯定是不会出错的

```
<button v-on:click='addFn'>点击+2</button>
<button @click='addFn2(3)'>点击+3</button>
```

### 🏷️5. v-on获取事件对象

v-on 获取事件对象 event 即 e

0.  无参数获取事件对象 - 我们的事件对象event默认在第一个形参上

0.  有参数（特指带小括号的方法），这个小括号会覆盖event默认参数，我们可以用$event的实际参数来代替这个事件对象

    **注意事项**：有参数时，一般情况下，我们都将事件对象event放到整个形参的最后一位

```
<button v-on:click='addFn'>点击+2(获取事件对象版本)</button>
<button @click='addFn2(3, $event)'>点击+3(获取事件对象版本)</button>
<a href="http://www.baidu.com" @click="go">百度</a>
```

```
methods: {
    addFn(event){
      this.count+=2
      console.log(event)
    },
    addFn2(num, event){
      this.count+=num
      console.log(event)
    },
    go(event){
      event.preventDefault()
      console.log('阻止a标签跳转')
    }
  }
```

### 🏷️6. v-on修饰符

#### 6.1 语法

v-on:事件名.修饰符="methods里函数"

-   .stop - 阻止事件冒泡
-   .prevent - 阻止默认行为
-   .once - 程序运行期间, 只触发一次事件处理函数

#### 6.2 举个例子🌰

```
<template>
    <div @click="fatherFn()">
      <p @click.stop="sonFn()">点击后阻止冒泡</p>
      <a href="http://www.baidu.com" @click.prevent.stop>百度</a>
      <p @click.once="onceFn()">观察这个点击事件到底执行几次</p>
    </div>
</template>

<script>
export default {
  name: 'demo-04',
  data () {
    return {
    }
  },
  methods: {
    // 父标签的冒泡事件
    fatherFn(){
      console.log('冒泡事件触发了')
    },
    // 子元素的点击事件
    sonFn(){
      console.log('子元素被点击了')
    },
    // 观察该方法的触发次数
    onceFn(){
      console.log('once触发了')
    }
  }
}
</script>
```
