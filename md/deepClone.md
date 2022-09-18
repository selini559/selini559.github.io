## 🏝️前言

在上一篇数组去重的文章里，使用删除元素实现数组去重时，有提到过concat()这个方法，却并没有说它的具体作用，这就和今天的浅拷贝有关了

在这之前，我们把一个变量值给另一个变量时使用的是赋值操作，赋值之后两个变量其中一个的值更改也不会影响到另一个变量

但是为什么数组赋值之后，对新数组进行去重，原来的数组也会随着新数组一块变化呢？

### 🏷️赋值操作

首先我们要知道赋值操作赋的是什么值

基本数据类型赋值传递的是存放在栈内的数据，而引用类型赋值传递的是他们存放在栈内的地址，它们的数据存放在这个地址指向的堆内存里

所以引用类型赋值传递的是存在栈内的地址，当对新对象进行数据的修改时，改变的是这个地址指向的堆内存里的数据

因为新旧对象使用的是相同的地址，地址指向的数据改变之后，旧对象的值也就随之改变了

![赋值 (1).png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ea374bf80b074af886bc5f056611b9f9~tplv-k3u1fbpfcp-watermark.image?)

但是我们一般是不想让原对象的数据改变的，那要怎么解决这个问题呢，这时候就用到了深浅拷贝

## 🌄浅拷贝

那先来说浅拷贝

浅拷贝创建一个新的对象，只拷贝一层，即拷贝对象里第一层基本数据类型的值和引用类型的地址

![浅拷贝.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58a46d1816504d12aff85b7d03e96b42~tplv-k3u1fbpfcp-watermark.image?)

但是深层次的数据还是会互相影响

如果修改新对象里第一层基本数据类型的值，不会对旧对象产生影响，但如果修改第一层的引用类型的值，仍会对旧对象产生影响

因为新旧对象虽然不再使用同一地址，但第一层的引用类型的地址仍是相同的

**举个栗子**🌰

```js
let obj_old = {
    name: 'Tom',
    age: 15,
    favorite: {
        food: 'bread',
        drink: 'milk'
    }
}
// Object.assign()是一种浅拷贝的方法
let obj_new = Object.assign({}, obj_old)
console.log(obj_old === obj_new)
console.log(obj_old.name === obj_new.name)
console.log(obj_old.favorite === obj_new.favorite)
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ef28246a52c9440485ea9b4fb16d53f4~tplv-k3u1fbpfcp-watermark.image?)

这里的例子我们使用了浅拷贝，然后我们来对比新旧对象

> obj_old === obj_new是false，这说明新旧对象的地址已经不一样了

> obj_old.name === obj_new.name是true，这个是基本数据类型的值是相同的，没有问题

> obj_old.favorite === obj_new.favorite也是true，这里的favorite也是对象，但是他们比较出来的结果不是false而是true，说明这个对象的地址已经是相同的了，它们共享同一块内存空间

再来对新对象里的数据进行修改

修改新对象第一层的基本数据类型时，新旧对象互不影响
```js
obj_new.name = 'Jerry'
console.log(obj_old)
console.log(obj_new)
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c9e4dbeb50fb45c793e946388b330f42~tplv-k3u1fbpfcp-watermark.image?)

修改新对象第一层的引用数据类型时，也就是修改obj_new第一层的favorite对象里的属性值时，obj_old里的favorite相应的属性值也随之改变了，新旧对象相互影响

```js
obj_new.favorite.food = 'cheese'
console.log(obj_old)
console.log(obj_new)
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2f6eaaed29d74785a3fb2a8e8541f75b~tplv-k3u1fbpfcp-watermark.image?)

### 🏷️浅拷贝的方法

了解过浅拷贝是什么之后，这里就来罗列几个浅拷贝的方法

#### 1. *Object.assign()*

> 语法：Object.assign(target, ...sources)
>
> target
> 目标对象，接收源对象属性的对象，也是修改后的返回值。
> sources
> 源对象，包含将被合并的属性。

代码展示
```js
let obj_old = {
    name: 'Tom',
    age: 15,
    favorite: {
        food: 'bread',
        drink: 'milk'
    }
}
let obj_new = {...obj_old}
console.log(obj_old === obj_new)  // false
console.log(obj_old.name === obj_new.name)  // true
console.log(obj_old.favorite === obj_new.favorite)  // true
```

#### 2. *展开运算符 Spread ...*

> 语法：{...sources}
>
> sources
> 源对象，包含将被合并的属性。

代码展示
```js
let obj_old = {
    name: 'Tom',
    age: 15,
    favorite: {
        food: 'bread',
        drink: 'milk'
    }
}
let obj_new = Object.assign({}, obj_old)
console.log(obj_old === obj_new)  // false
console.log(obj_old.name === obj_new.name)  // true
console.log(obj_old.favorite === obj_new.favorite)  // true
```

#### 3. *Array.prototype.concat()*

> 语法：arr.concat(value0, /* … ,*/ valueN) 
>
> 注：如果省略了所有 `valueN` 参数，则 `concat` 会返回调用此方法的现存数组的一个浅拷贝。

代码展示
```js
let arr_old = [1, 2, {name: 'Tom'}]
let arr_new = arr_old.concat()
console.log(arr_old === arr_new)  // false
console.log(arr_old.name === arr_new.name)  // true
```

#### 4. *Array.prototype.slice()*

> 语法：arr.slice(begin, end) 
>
> 注：如果省略了 `begin`, `end` 参数，则 `slice` 会返回调用此方法的现存数组的一个浅拷贝。

代码展示
```js
let arr_old = [1, 2, {name: 'Tom'}]
let arr_new = arr_old.slice()
console.log(arr_old === arr_new)  // false
console.log(arr_old.name === arr_new.name)  // true
```

## 🌄深拷贝

接下来说深拷贝

深拷贝就是在堆内存中开辟一个新的空间存放新对象，拷贝原对象的所有属性，拷贝前后两个对象互不影响

深拷贝的新旧对象不共享内存

![深拷贝 (1).png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/31a3a9b3bd1440fd9545a821ba43c3ea~tplv-k3u1fbpfcp-watermark.image?)

这时我们去修改新对象中的任意层级的任意属性值，都不会对原对象产生影响，原对象依然保持不变

**举个栗子**🌰

```js
let obj_old = {
  name: 'Tom',
  age: 15,
  hobby: ['eat', 'game'],
  favorite: {
      food: 'bread',
      drink: {
        dname: 'milk',
        color: 'white',
      },
  }
}
let obj_new = _.cloneDeep(obj_old)
console.log(obj_old)
console.log(obj_new)
console.log(obj_old.name === obj_new.name)
console.log(obj_old.favorite === obj_new.favorite)
console.log(obj_old.favorite.drink === obj_new.favorite.drink)
```

这里我们使用了`lodash`工具库提供的`_.cloneDeep`深拷贝方法,来看一下新旧对象的对比

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eb3842905a6a4bf1b42a76d95ae0cf4c~tplv-k3u1fbpfcp-watermark.image?)

可以看见新旧对象所有属性及属性值完全相同

那再来细节对比一下，看看拷贝后对象的地址是否相同

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/16392a4effab427c988ed7fdcfc37f30~tplv-k3u1fbpfcp-watermark.image?)

> obj_old.name === obj_new.name为true，这个是基本数据类型，完全相同，没有问题

> obj_old.favorite === obj_new.favorite，这里为false，到这里就和浅拷贝不同了，浅拷贝到这一层的时候，对象属性的地址是相同的，而深拷贝是完全拷贝出一个新的对象，所以不管是哪一层，对象属性的地址都是不同的

> obj_old.favorite.drink === obj_new.favorite.drink为false，再往深一层仍然是false，即地址不相同

那再来修改一下属性值，看看前后对比

```js
obj_new.name = 'Jerry'
obj_new.hobby[0] = 'sing'
obj_new.favorite.food = 'cheese'
```

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bf27bd505e0746f597269d99c3bb92fa~tplv-k3u1fbpfcp-watermark.image?)

修改属性值之后，新旧对象是互不影响的

### 🏷️深拷贝的方法

那么现在就来罗列几个深拷贝的方法

#### 1. *递归实现*

使用递归实现原对象每一层的拷贝，当遇到基本数据类型时，直接拷贝，遇到引用数据类型时，递归拷贝它的每个属性

代码展示
```js
const obj_old = {
  name: 'Tom',
  age: 15,
  hobby: ['eat', 'game'],
  favorite: {
      food: 'bread',
      drink: {
        dname: 'milk',
        color: 'white',
      },
  }
}
const obj_new = {}

function deepClone(newObj, oldObj){
  for (const key in oldObj) {
    if (oldObj[key] instanceof Object) {
      newObj[key] = {}
      deepClone(newObj[key], oldObj[key])
    } else if (oldObj[key] instanceof Array) {
      newObj[key] = []
      deepClone(newObj[key], oldObj[key])
    } else {
      newObj[key] = oldObj[key]
    }
  }
}

deepClone(obj_new, obj_old)

console.log(obj_old)
console.log(obj_new)
console.log(obj_old.name === obj_new.name)
console.log(obj_old.favorite === obj_new.favorite)
console.log(obj_old.favorite.drink === obj_new.favorite.drink)
```
测试结果

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5358c374bb704714b86d8eab907e8199~tplv-k3u1fbpfcp-watermark.image?)

#### 2. *lodash工具包*

[点这里去lodash的中文文档](https://www.lodashjs.com/)

引入成功后，我们直接使用lodash提供给我们的函数_.cloneDeep就行

代码展示

```js
let obj_old = {
  name: 'Tom',
  age: 15,
  hobby: ['eat', 'game'],
  favorite: {
      food: 'bread',
      drink: {
        dname: 'milk',
        color: 'white',
      },
  }
}
let obj_new = _.cloneDeep(obj_old)

console.log(obj_old)
console.log(obj_new)
console.log(obj_old.name === obj_new.name)
console.log(obj_old.favorite === obj_new.favorite)
console.log(obj_old.favorite.drink === obj_new.favorite.drink)
```
测试结果

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5358c374bb704714b86d8eab907e8199~tplv-k3u1fbpfcp-watermark.image?)

#### 2. *JSON.parse(JSON.stringify(obj))*

`JSON.stringify()` 将JSON格式的对象转为字符串

`JSON.parse()` 将JSON格式的字符串转为对象

代码展示

```js
const obj_old = {
  name: 'Tom',
  age: 15,
  hobby: ['eat', 'game'],
  favorite: {
      food: 'bread',
      drink: {
        dname: 'milk',
        color: 'white',
      },
  }
}
const obj_new = JSON.parse(JSON.stringify(obj_old))

console.log(obj_old)
console.log(obj_new)
console.log(obj_old.name === obj_new.name)
console.log(obj_old.favorite === obj_new.favorite)
console.log(obj_old.favorite.drink === obj_new.favorite.drink)
```
测试结果

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5358c374bb704714b86d8eab907e8199~tplv-k3u1fbpfcp-watermark.image?)

❣️虽然这个方法最简单，代码行数最少，但是它也有一定的缺陷：

1. 拷贝对象的值中如果有‘函数’，‘undefined’，‘symbol’
JSON.stringify()序列化后，键值对丢失

2. 拷贝RegExp会变成空对象{}

3. 对象中含有‘NaN’，‘Infinity’会变成null

4. 拷贝Date会变成字符串

## 🏝️结语

这次的深拷贝浅拷贝的总结就到这里啦，后续发现不足的话会继续补充的