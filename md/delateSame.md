在这里写两个简单的去重算法，分别使用JS中的数组添加元素的方法和删除元素的方法，写两个不同的去重算法，一个通过给新数组全部原数组数据再删除重复数据来去重，一个通过向新数组中添加元素来生成一个没有重复元素的新数组。
## 删除元素去重
在js里删除数组元素有哪些方法呢，array.pop(),arr.shift(),还有一个比较重要比较常用的是arr.splice()

```js
array.pop() // pop删除数组最后一个元素，返回值是被删元素
arr.shift() // shift删除数组的第一个元素，返回值是被删元素
arr.splice() // splice(要删除元素的下标值，要删除的元素个数)
             // 如果splice后只跟一个参数，那么会从当前下标的元素删到结尾
```
首先我们来理清逻辑
1. 创建一个新数组，把原数组的数据复制到新数组里。
这里需要注意，如果直接使用let newArr = arr这样的赋值操作的话，是引用了原数组而不是复制，引用数组的话，我们在修改新数组里的数据时，原数组的数据会跟着变化。我们一般是不能让原数组数据发生改变的，这里可以调用concat()方法只复制数组数据过去。
3. 定义外层循环，循环次数小于数组长度，以此取到数组每一个元素，每取到一个元素就与内层循环取到的每一个都进行比较。
4. 定义内层循环，循环次数小于新数组长度，遍历取到新数组当前的所有元素。
再将它们与外层循环一次取到的一个元素进行比较，并且内层取到的元素下标与外层取到的元素的下标不能相同，因为下标相同就代表两个元素是相同的，而这个相同的不能删掉，应该从下一个相同的元素开始删。这里删除数组元素就使用arr.splice()，当匹配到相同元素时，删除该元素。

代码如下

```js
<script>
      let arr = [4, 5, 3, 7, 4, 8, 4, 5]
      let newArr = arr.concat()
      console.log(`去重之前新数组：${newArr}`)
      for (let i = 0; i < newArr.length; i++) {
        for (let j = 0; j < newArr.length; j++) {
          if (newArr[i] === newArr[j] && i !== j) {
            newArr.splice(j, 1)
          }
        }
      }
      console.log(`去重之后原数组：${arr}`)

      console.log(`去重之后新数组：${newArr}`)
    </script>
```
去重之后的结果如下

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e55a6651686346b5ae117e52b169f2ef~tplv-k3u1fbpfcp-watermark.image?)

## 添加元素去重
在js里添加元素的方法有arr.push()和arr.unshift()

```js
arr.push() // 将元素追加到数组最后面去，如果要添加多个元素，那么多个元素之间用逗号隔开
           // arr.push()能得到一个返回值，返回值就是添加元素后数组的长度
arr.unshift() // 将元素添加到数组最前面
```

仍然是先来理清逻辑
1. 声明一个新的数组来跟原数组进行比较，声明的这个新数组为空，通过后边的比较来给它添加元素。
2. 同上，定义双重循环，拿外层循环的每一个元素，去跟内层循环里面的每一个元素进行比较。
3. 在内层循环里，如果外层循环取到的值在内层循环里没有相同的，就把该元素插入到新数组；如果外层循环取到的值与内层循环的某一个元素相同，就代表新的数组里面有这个元素，就不用插入该元素了，直接跳出该次循环。
4. 在这里我们会使用到一个开关的概念，只有当某种条件达到过后，就会改变开关的值，才会放行。可以声明一个flag为false，如果找到相同元素，flag变为true,跳出循环；如果内层循环全部结束过后，flag的值还是false，就证明里层循环全部过程都没有找到外层相同的元素。

代码如下

```js
<script>
      let arr = [4, 5, 3, 7, 4, 8, 4, 5]
      let newArr = []
      for (let i = 0; i < arr.length; i++) {
        let flag = false
        for (let j = 0; j < newArr.length; j++) {
          if (arr[i] === newArr[j]) {
            flag = true
            break
          }
        }
        if (flag === false) {
          newArr.push(arr[i])
        }
      }

      console.log(`去重之后原数组：${arr}`)
      console.log(`去重之后新数组：${newArr}`)
    </script>
```
去重之后的结果如下

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/6240f6db2bc7463abddaf1c6a2f008aa~tplv-k3u1fbpfcp-watermark.image?)

## 结语
这里只是写了两种原生js的去重算法，一种通过删除元素来去重，一种通过添加元素来达到去重效果，就可以顺便巩固一下数组的删除元素和添加元素的方法，js其实提供的有去重的方法 new Set(arr)，平时我们直接调用即可