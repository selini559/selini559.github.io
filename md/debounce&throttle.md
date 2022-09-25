# 🌄手把手教会你防抖与节流

## 🏝️前言

防抖和节流作为面试的常问点之一，也作为项目开发中常需要考虑的问题，你还不知道防抖节流是什么吗？

不用担心，今天这篇文章教会你JS中的防抖与节流

曾看到一个对于防抖节流非常贴切的形容，相信大部分人都玩过王者或者联盟吧，这个形容就和它们有关

大家可以把防抖理解为回城，把节流理解为技能冷却

不太玩游戏的朋友也不用担心理解不了，下面我们就来详细解说

## 🏝️防抖

### 🏷️防抖是什么

我们先从防抖开始讲解，防抖是什么呢？为什么说可以把它理解为游戏里的回城呢？

在游戏里回城时间需要8秒，当你按下回城按钮，你需要等待8秒后才能成功回城，但如果你中途不停重新触发回城，这个8秒的倒计时就会不断的中断重计时、中断重计时...

直到某一次，你点下了回城，然后站在原地不动，在这8秒的倒计时内，回城没有被一次次触发，那么这个倒计时就不会中断，8秒结束后就可以成功回到泉水了

其实防抖的原理就和这个差不多，**在n秒后执行该事件，若在n秒内被重复触发，则重新计时**

### 🌰例子来啦

那现在我们先来手写一个防抖函数，然后再根据代码逐行解释

```html
<body>
  <div class="out">
    <div class="box">0</div>
    <button>点我加1</button>
  </div>
</body>
<script>
  const btn = document.querySelector('button')
  const box = document.querySelector('.box')
  let i = 1
  const addFn = function() {
    console.log(this)
    this.innerHTML = i++
  }

  // 防抖
  const debounce = (fn, ms = 0) => {
    let timer
    return function() {
      clearTimeout(timer)
      timer = setTimeout(() => {
        fn.call(this)
      }, ms);
    }
  }

  btn.addEventListener('click', debounce(addFn, 1000).bind(box))
</script>
```

代码写好了，我们来看看实现效果

![防抖.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/64fd92e677fd44b1a3518332d01e31ff~tplv-k3u1fbpfcp-watermark.image?)

可以看出，当我们不停点击按钮时，数字并没有加1，然而当某一次点击停下超过1秒了,期间没有再次点击，数字才会成功加1

这也正体现了防抖的在n秒后执行该事件，若在n秒内被重复触发，则重新计时这一原理

### 🏷️详解

我们再来对script中每一行代码都是什么意思进行解释：

```js
  // 获取按钮和显示框
  const btn = document.querySelector('button')
  const box = document.querySelector('.box')
  // 定义变量i,存放数字
  let i = 1
  // 让数字加1的函数
  const addFn = function() {
    // 我们要让this指向box盒子，让box里的数字变化
    // 在控制台打印this，方便我们观察this指向的元素是否正确
    console.log(this)
    // 执行一次数字加1
    this.innerHTML = i++
  }
```

这几行代码较为简单，下面开始**防抖部分**

```js
  // 定义防抖函数debounce
  // 传入的参数fn是实现数字加1的函数，ms是防抖的倒计时n秒，可以给它一个默认值0
  const debounce = (fn, ms = 0) => {
    // 声明一个定时器标记timer
    let timer
    // 直接将function作为返回值返回
    return function() {
      // 每点击一次按钮，就会触发一次防抖函数,那么当防抖函数被触发了，我们第一件事应该是关闭定时器停止倒计时
      // 可以联想一下玩游戏回城时，回城过程中重新触发了回城，那上一次的回城倒计时应该先停止，再重新开始倒计时
      clearTimeout(timer)
      // 这里就是重新开启定时器，再次1000ms倒计时
      // 只要我们不停点击按钮，就会不停触发防抖函数，1000ms倒计时还没结束就又会清除计时器重新赋值
      // 直到某一次1000ms内都没有再次点击，才能成功执行计时器，数字加1
      timer = setTimeout(() => {
        // 使用call()改变this指向，不改this指向的话，这里的this就不指向box了，addFn函数的this.innerHTML就不会执行
        fn.call(this)
      }, ms);
    }
  }
  
  // 给按钮btn绑定点击事件，每点击一次就去执行调用防抖debounce函数
  // 传入实参为addFn数字加1的函数，以及1000ms即1s的计时时间
  // bind也是用来改变this指向的，让this指向的是显示数字的box盒子
  btn.addEventListener('click', debounce(addFn, 1000).bind(box))
```

### 🏷️this指向补充

因为代码里用到了两个改变this指向的函数call()和bind()，那这里就顺便补充一下它们的用法

**call()**
> 语法：function.call(this指向的目标, 指定的参数列表)
>
> call()方法接受的是*一个参数列表*

**bind()**
> 语法： function.bind(this指向的目标, 指定的参数列表)
>
> bind()方法创建一个新的函数，这个函数里面的this指向我们传入的第一个参数；bind不是立即执行的,需要手动调用

到这里防抖就差不多啦😊,接下来我们再来谈谈节流吧

## 🏝️节流

### 🏷️节流是什么

我们在开头说防抖是回城，节流是技能冷却，那这又是个什么意思呢？

好的，现在思绪进入游戏中，假如一开局手残，不小心点了个闪现😈，那在接下来120s的冷却时间内都不能再次触发闪现，在冷却时间内不管你怎么点，闪现都只触发那一次，除非等到120s结束，才能再次使用

延申到节流的概念，节流是n秒内只执行一次，若在n秒内重复触发，只有一次生效

其实实现节流有两种方式，一种是和防抖一样使用定时器，另一种就是时间戳；上边刚用过定时器，这里就用时间戳来实现吧

### 🌰例子来啦

那下面上代码：

```html
<body>
  <div class="out">
    <div class="box">0</div>
    <button>点我加1</button>
  </div>
</body>
<script>
  const btn = document.querySelector('button')
  const box = document.querySelector('.box')
  let i = 1
  const addFn = function() {
    console.log(this)
    this.innerHTML = i++
  }

  // 节流
  const throttle = (fn, ms = 0) => {
    let pre = 0
    return function() {
      let now = Date.now()
      if (now - pre >= ms) {
        fn.apply(this)
        pre = Date.now()
      }
    }
  }

  btn.addEventListener('click', throttle(addFn, 1000).bind(box))
</script>
```
好的，再来看看实现的效果：

![节流.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/247c47280cea49dab7b2a7e7d413c922~tplv-k3u1fbpfcp-watermark.image?)

从实现效果上可以看出，节流与防抖不同的是，当我们不停点击按钮时，它是有节奏地加1的，是每隔一个时间段执行一次加1，而不是等点击结束再去计算时间

### 🏷️详解

这个代码除了节流throttle函数部分与上一个代码不同，其余相同，就不进行解释了，这里主要说说**节流部分**的代码

```js
  // 定义节流函数throttle
  // 传入的参数fn是实现数字加1的函数，ms是时间段n秒，n秒内只执行一次数字加1
  const throttle = (fn, ms = 0) => {
    // 定义时间戳起点
    let pre = 0
    return function() {
      // 鼠标一点击按钮，就记录下当前的时间戳
      let now = Date.now()
      // 当时间戳now与时间戳起点的时间间隔大于ms时，执行回调函数
      if (now - pre >= ms) {
        // 绑定this，确保this的指向正确
        fn.apply(this)
        // 将当前时间记录下来，作为下一次计时的起点
        pre = Date.now()
      }
    }
  }
  
  // 给按钮btn绑定点击事件，每搁1000ms调用一次addFn函数，让数字加1
  // 同时使用bind()函数让this指向box
  btn.addEventListener('click', throttle(addFn, 1000).bind(box))
```

### 🏷️this指向再补充

在上边的防抖代码里我们使用了call()和bind()这两个改变this指向的方法，在节流的代码里我们又使用另一种改变this指向的方法apply()

就再对apply()进行一个补充说明吧

**apply()**
> 语法：function.call(this指向的目标, 数组参数)
>
> 虽然这个函数的语法与 `call()`几乎相同，但根本区别在于，`call()` 接受一个**参数列表**，而 `apply()` 接受一个**参数的单数组**。

## 🏝️结语

这次对JS中防抖和节流的总结与补充差不多就到这里啦，要是大家能在这篇文章里有所收获的话那可再好不过啦😊

要是有什么错误的话也欢迎指出哦，大家一起进步🍻