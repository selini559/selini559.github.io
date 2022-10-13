# 🌄forEach、map以及for...in、for...of之间的区别

## 🏝️forEach与map的区别

### 🏷️forEach

**语法：**

```
// 回调函数
forEach(callbackFn)
// 箭头函数
forEach((element, index, array) => {})
```

> callbackFn - 为数组中每个元素执行的函数
>
> 函数调用时带有以下参数：
>
> element - 数组中正在处理的当前元素
>
> index - 数组中正在处理的当前元素的索引值
>
> array - forEach方法正在操作的数组

**来个例子**


```js
  const arr= [1, 2, 3]
  function callbackFn (item, index, arr) {
    console.log(item, index, arr)
  }
  arr.forEach(callbackFn)

  console.log('===============================')

  arr.forEach((item, index, arr) => {
    console.log(item, index, arr)
  })
```

![image-20221013200047918](C:\Users\asus\Desktop\blog\docs\md\for\image-20221013200047918.png)

我们使用回调函数和箭头函数的方式实现的效果都是一样的，只不过回调函数是把函数体提取出来单独封装了一个函数

forEach()为每个数组元素执行一次callbackFn函数，它总是返回 undefined值，并且不可链式调用

### 🏷️map

**语法：**

```
// 回调函数
map(callbackFn)
// 箭头函数
map((element, index, array) => {})
```

> callbackFn - 生成新数组元素的函数，使用三个参数：
>
> element - 数组中正在处理的当前元素
>
> index - 数组中正在处理的当前元素的索引
>
> array - map 方法调用的数组

**来个例子**


```js
  const arr= [1, 2, 3]
  function callbackFn (item, index, arr) {
    return item + 1
  }
  const arrMap = arr.map(callbackFn)
  console.log(arrMap)

  console.log('===============================')

  const arrMap2 = arr.map((item, index, arr) => {
    return item + 1
  })
  console.log(arrMap2)
```

![image-20221013201001777](C:\Users\asus\Desktop\blog\docs\md\for\image-20221013201001777.png)

这里同样的使用回调函数和箭头函数的方式实现的效果都是一样的

map()也会给每个元素按顺序执行一次callbackFn函数，每个回调函数的返回值组成一个新数组，需要再创建一个新的数组来接收这些返回值

所以map()方法可以用来创建一个新数组，当我们要对数组的每个元素进行修改而产生新数组时，可以使用map()方法，而非forEach()方法

## 🏝️for...in与for...of的区别

### 🏷️for...in

**语法**

```
for (key in object) {}
```

**来个例子**

```js
  const arr= [
    { a: 1 },
    { b: 2 },
    { c: 3 }
  ]
  for (const key in arr) {
    console.log(key)
    console.log(arr[key])
  }
```

![image-20221013204241241](C:\Users\asus\Desktop\blog\docs\md\for\image-20221013204241241.png)

for...in 语句以任意顺序迭代一个对象的除`Symbol`以外的`可枚举`属性,它遍历获取的是键名，但for...in遍历的是整个原型链，性能非常差

for..in是为遍历对象属性而构建的，不建议与数组一起使用，它最常用的地方应该是用于调试，可以更方便的去检查对象属性

### 🏷️for...of

**语法**

```
for (key of object) {}
```

**来个例子**

```js
  const arr= [
    { a: 1 },
    { b: 2 },
    { c: 3 }
  ]
  for (const key in arr) {
    console.log(key)
    console.log(arr[key])
  }
```

![image-20221013204351724](C:\Users\asus\Desktop\blog\docs\md\for\image-20221013204351724.png)

for...of语句在可迭代对象上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句，它遍历获取的是键值

for...of与for...in不同的是，它只遍历当前对象而不会遍历原型链

for...in主要是为了遍历对象而创建，for...of却可以用来遍历Array,Map,Set,String,TypedArray,arguments等

## 🏝️总结一下

直接借用一下villay大佬的总结吧🍻

**forEach与map的区别**

**foreach**()方法会针对每一个元素执行提供得函数,该方法没有返回值,是否会改变原数组取决与数组元素的类型是基本类型还是引用类型

**map**()方法不会改变原数组的值,返回一个新数组,新数组中的值为原数组调用函数处理之后的值

**for...in与for...of的区别**

for...of遍历获取的是对象的键值, for...in获取的是对象的键名

 for...in会遍历对象的整个原型链, 性能非常差不推荐使用,而for...of只遍历当前对象不会遍历原型链

对于数组的遍历,for...in会返回数组中所有可枚举的属性(包括原型链上可枚举的属性),for...of只返回数组的下标对应的属性值; 

for...in循环主要是为了遍历对象而生,不适用遍历数组; for....of循环可以用来遍历Array,Map,Set,String,TypedArray,arguments等对象