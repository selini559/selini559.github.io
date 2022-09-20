# 🌄vue02

## 🏝️1. v-on按键修饰符

### 🏷️1.1 语法

-   @keyup.enter - 监测回车按键
-   @keyup.esc - 监测返回按键

### 🏷️1.2 例子🌰

```
<template>
    <div>
      <input type="text" @keydown.enter="enterFn"/>
      <input type="text" @keydown.esc="escFn"/>
      <input type="text" @keydown.enter.esc="allFn"/>
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
    enterFn(event){
      console.log("按下enter", event)
    },
    escFn(event){
      console.log("按下esc", event)
    },
    allFn(event){
      console.log("混合事件", event)
    }
  }
}
</script>
```

## 🏝️2. ❣️v-model❣️

### 🏷️2.1 用法

**v-model="data中定义的变量"**

v-model把value属性和vue数据变量, 双向绑定到一起

0.  数据变化 => 视图自动变化

    2.  视图变化 => 数据自动变化

### 🏷️2.2 例子🌰

#### 2.2.1 普通input框

这里的v-model代替的是input中的value属性

```
<template>
    <div>
       <!-- 1. 普通输入框 -->
      <span>用户名</span>
      <input type="text" v-model="uname" />
      <br />
      <span>密码</span>
      <input type="password" v-model="pwd" />
    </div>
</template>

<script>
export default {
  name: 'demo-04',
  data () {
    return {
      uname: '',
      pwd: ''
    }
  }
}
</script>
```

#### 2.2.2 下拉框

这里的v-model代替的是select中的name属性

```
<template>
    <div>
      <!-- 2. 下拉框 -->
      <select v-model="selectForm" id="">
        <option value="面条">面条</option>
        <option value="大米">大米</option>
        <option value="馒头">馒头</option>
      </select>
      <br />
    </div>
</template>

<script>
export default {
  name: 'demo-04',
  data () {
    return {
      selectForm: ''
    }
  }
}
</script>
```

#### 2.2.3 复选框

这里的v-model代替的是复选框中的value属性，因为复选框的变量可以是多个数据，所以v-model的变量应该为一个数组

```
<template>
    <div>
      <!-- 3. 复选框 -->
      <input type="checkbox" value="吃饭" v-model="hobby"> 吃饭
      <input type="checkbox" value="睡觉" v-model="hobby"> 睡觉
      <input type="checkbox" value="学习" v-model="hobby"> 学习
      <br />
    </div>
</template>

<script>
export default {
  name: 'demo-04',
  data () {
    return {
      hobby: []
    }
  }
}
</script>
```

#### 2.2.4 单选框

这里的v-model代替的是单选框中的name属性，这里v-model中的变量应该是字符串

```
<template>
    <div>
      <!-- 4. 单选框 -->
      <input type="radio" value="男" v-model="sex"> 男
      <input type="radio" value="女" v-model="sex"> 女
      <br />
    </div>
</template>

<script>
export default {
  name: 'demo-04',
  data () {
    return {
      sex: ''
    }
  }
}
</script>
```

#### 2.2.5 多行输入框

这里的v-model将原本写在双标签中的变量转移到了标签内部的v-model指令中，这样文本域的数据写法和input文本框完全一样了

```
<template>
    <div>
      <!-- 5. 多行输入框 -->
      <textarea>文本内容在这里。。。。。。。。。。。。</textarea>
      <textarea v-model="info"></textarea>
    </div>
</template>

<script>
export default {
  name: 'demo-04',
  data () {
    return {
      info: ''
    }
  }
}
</script>
```

### 🏷️2.3 ❣️面试题

**问：** vue双向绑定实现原理

**答：** 当一个Vue实例创建时，Vue会遍历data选项的属性，用`Object.defineProperty`将它们转化为`getter/setter`并且在内部追踪相关依赖，在属性被访问拒绝和修改时通知变化。每个组件实例都有相应的watcher（监听器）程序实例，它会在组件渲染的过程中把属性记录为依赖，之后当依赖项的setter被调用时，会通知watcher重新计算，从而致使它关联的组件得以更新。

## 🏝️3. v-model 的修饰符

### 🏷️3.1 语法

**v-model.修饰符="vue数据变量"**

-   **.number**(常用) - 它可以以parseFloat的方式将输入框的内容转化为数字，与parseFloat最大的区别：如果开头就不是数字，.number会失效，而parseFloat则会转化为NaN
-   **.trim**(常用) - 它可以将输入框中v-model绑定的字符串实时的去除前后空格
-   **.lazy** - 在change时触发而非input时（一切可以触发change事件的情况，如失焦）

### 🏷️3.2 例子🌰

输入电话号码时会自动清除非数字及以后部分

输入用户名时会自动忽略空格

输入用户名2时data中的数据不会实时更新，而是在失焦或按下enter键时更新

```
<template>
    <div>
      <span>电话号码</span>
      <input type="text" v-model.number="phone">

      <span>用户名</span>
      <input type="text" v-model.trim="username">

      <span>用户名2</span>
      <input type="text" v-model.lazy="username2">
    </div>
</template>

<script>
export default {
  name: 'demo-04',
  data () {
    return {
      phone: '',
      username: '',
      username2: ''
    }
  },
  methods: {
  }
}
</script>
```

## 🏝️4. v-text和v-html

### 🏷️4.1 语法

-   v-text="vue数据变量"

    v-text和innerText 添加的字符串文本是一样的效果

-   v-html="vue数据变量"

    v-html和innerHTML 添加的标签字符串文本的处理方式完全一样

### 🏷️4.2 例子🌰

**注意： v-text或v-html会覆盖标签内的所有子元素**

```
<template>
    <div>
      <div>插值表达式：{{ msg }}</div>

      <!-- 只要使用了v-text， v-html 就不可以给当前的标签设置任何子元素 -->
      <div v-text="msg"></div>
      <div v-html="msg"></div>
    </div>
</template>

<script>
export default {
  name: 'demo-04',
  data () {
    return {
      msg: `<span style="color: red;">hello world</span>`
    }
  },
  methods: {
  }
}
</script>
```

## 🏝️5. v-show和v-if

### 🏷️5.1 语法

-   v-show="vue变量"
-   v-if="vue变量"

变量应该是boolean值，还可以判断当前变量隐式转化为boolean值的状态

> v-show 是采用display:none的方式进行显示和隐藏的，其实不管怎么说这个元素还是在dom树上
>
> v-if 是采用删除、添加dom元素来进行显示和隐藏的， 隐藏时其实是将当前的元素从dom上直接删除

**注意：** 一般情况下使用v-show来进行显示隐藏的元素都是静态元素(它内部没有动态的变量控制)，除此以外均建议使 用v-if来进行显示和隐藏

### 🏷️5.2 例子🌰

flag为true时，这两个标签均能显示在页面上；为false时不显示

```
<template>
    <div>
       <h1 v-show="flag">v-show的特点</h1>
       <h1 v-if="flag">v-if的特点</h1>
    </div>
</template>

<script>
export default {
  name: 'demo-04',
  data () {
    return {
      flag: false
    }
  }
}
</script>
```

当flag为false时，v-show 是采用display:none的方式进行显示和隐藏的，而v-if是将当前的元素从dom上直接删除


![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bb83e5ed7aa94462962c1cd858a2a94d~tplv-k3u1fbpfcp-watermark.image?)

### 🏷️5.3 v-else-if和v-else

if判断它有 else if 还有 else 与之形成组合，v-if也有 v-else-if 和 v-else 与之配合，他们之间的使用方式与表现结果是完全一样的

**注意：** 它们的使用有特定顺序，有连续性

举个例子🌰

```
<template>
    <div>
      <!-- 
        场景： 通过年龄的不同在页面上展示不同的效果
        1. 小于18岁 => 未成年
        2. 大于等于18岁，小于22岁 => 大学生
        3. 大于等于22岁 => 社畜
      -->
      <div v-if="age < 18">未成年</div>
      <div v-else-if="age >= 18 && age < 22">大学生</div>
      <div v-else>社畜</div>
    </div>
</template>

<script>
export default {
  name: 'demo-04',
  data () {
    return {
      age: 12
    }
  }
}
</script>
```

## 🏝️6. v-for

### 🏷️6.1 语法

语法类比forEach，v-for可以遍历数组 / 对象 / 数字 / 字符串

-   v-for="(值, 索引) in 目标结构"
-   v-for="值 in 目标结构"

**注意：** 循环遍历时，需要给v-for标签上添加一个key属性，用来表现当前循环的每一个元素它的唯一 (一般可以用索引来作为它的key)

### 🏷️6.2 例子🌰

```
<template>
  <div>
    <!-- 数组遍历 -->
    -->
    <ul>
      <li v-for="(value, index) in arr" :key="index">
        {{value}} ------ {{index}}
      </li>
    </ul>
   <!-- 
      当遍历的是一个数组对象，且每一个对象元素中，都有一个属性它的值能够表示当前元素的唯一性，那么就可以在循环遍历的时候不使用index来作为key属性的值，而替换成这个唯一的属性值
    -->
    <ul>
      <li v-for="value in arr_obj" :key="value.id">
        {{value}}
      </li>
    </ul>

    <!-- 对象遍历 -->
    <!-- v-for遍历对象
      当遍历对象时， 第一个参数是对象中每个属性的值，第二个参数是对象中每个属性的键
    -->
    <ul>
      <li v-for="(value, key) in obj" :key="key">
        {{value}} ------ {{key}}
      </li>
    </ul>

    <!-- 遍历数字 -->
    <ul>
      <li v-for="(value, index) in 10" :key="index">
        {{value}} ------ {{index}}
      </li>
    </ul>

    <!-- 遍历字符串 -->
    <ul>
      <li v-for="(value, index) in str" :key="index">
        {{value}} ------ {{index}}
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'demo-01',
  data () {
    return {
      arr: ['月季', '玫瑰', '栀子', '芍药'],
      arr_obj: [
        {name: '张三', age: '20', id: 1},
        {name: '李四', age: '22', id: 2}
      ],
      obj: {
        name: '张三',
        nickname: '法外狂徒',
        lawyer: '罗翔'
      },
      str: 'happy'
    }
  }
}
</script>
```

### 🏷️6.3 与v-if同时使用

当既需要遍历又需要判断时，不要把v-for和v-if一起使用，可以在遍历数组之前进行filter的过滤操作

举个例子🌰

```
<template>
  <div>
    <ul>
      <!-- 错误！ <li v-for="(value, index) in arr" :key="index" v-if="value !== '玫瑰'"> -->
      <li v-for="(value, index) in arr.filter(v => v !== '玫瑰')" :key="index">
        {{value}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'demo-01',
  data () {
    return {
      arr: ['月季', '玫瑰', '栀子', '芍药']
    }
  }
}
</script>
```

### 🏷️6.3 更新监测

0.  当v-for遍历的数组发生变化时，(一定是原数组得发生变化) , 会触发v-for的遍历更新
0.  如果某个数组处理方式不会改变原数组，那么通过赋值的操作来让数组发生变化
0.  如果遍历的数据无法实时响应式，可以使用this.$set()方法来进行强制响应，这一方法其实是应急手段，在迫不得已时（找不到其他解决办法时）再去使用

> this.$set(参数1， 参数2， 参数3)
>
> 参数1： 更新的目标结构 - v-for所遍历的数据
>
> 参数2： 更新数据的位置 - 常常是索引位置
>
> 参数3： 需要更新的值

### 🏷️6.4 v-for 立即更新

v-for的默认行为会尝试**原地修改**元素而不是移动它们，也就是v-for尝试去用原来的dom元素进行修改，能改就不删

举个例子🌰

```
<template>
  <div>
    <ul>
      <li v-for="(obj, index) in arr" :key="obj.id">
        {{ obj.name }}
        <!-- 如果input框没有绑定v-model时，页面中输入的内容只与inputdom元素有关 -->
        <input type="text">
      </li>
    </ul>
    <button @click="btn">下标1位置插入新来的</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      arr: [
        {name: '老大',id: 50},
        {name: '老二',id: 31},
        {name: '老三',id: 10}
      ],
    };
  },
  methods: {
    btn(){
      this.arr.splice(1, 0, {
        id: 19, 
        name: '新来的'
      })
    }
  }
};
</script>
```

## 🏝️7. 虚拟dom

### 🏷️7.1 概念

.vue文件中的template里写的标签, 都是模板(并不是浏览器中看到的真实的dom元素), 都要被vue处理成虚拟DOM**对象**, 才会渲染显示到真实DOM页面上

**虚拟DOM优势：** 虚拟DOM保存在内存中, 只记录dom关键信息, 配合different算法提高DOM更新的性能

### 🏷️7.2 ❣️面试题

**问：** 你对虚拟DOM的理解？

**答：** `虚拟DOM`本质上是`JavaScript`对象，是对`真实DOM`的抽象表现。状态变更时，记录新树和旧树的差异，最后把差异更新到真正的`dom`中

## 🏝️8. diff算法 - 同级比较

### 🏷️8.1 根元素改变

**删除重建**

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/651b22ac7ab348eb98c88088512a9e5f~tplv-k3u1fbpfcp-watermark.image?)

### 🏷️8.2 根元素没变, 属性改变

**元素复用, 只更新属性**

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/454822da1e334dc9841261a82ee74fd9~tplv-k3u1fbpfcp-watermark.image?)

## 🏝️9. diff算法 - 属性key

### 🏷️9.1 没有key

**就地更新**

旧 - 虚拟DOM结构 和 新 - 虚拟DOM结构 对比过程

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/41e03d3c449046fcb8752444b332a903~tplv-k3u1fbpfcp-watermark.image?)

### 🏷️9.2 有key - 值为索引

**就地更新**

因为新旧虚拟DOM对比, key存在就复用此标签更新内容, 如果不存在就直接建立一个新的

0.  v-for先循环产生新的DOM结构, key是连续的, 和数据对应

0.  然后比较新旧DOM结构, 找到区别, 打补丁到页面上

    最后补一个li, 然后从第二个往后, 都要更新内容

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/249ef44f780b4e0d9b3492703cbaecf3~tplv-k3u1fbpfcp-watermark.image?)

### 🏷️9.3 有key - 值为id(不重复的值)

**移动更新**

**注意：** key的值只能是唯一不重复的, 字符串或数值

-   新DOM里数据的key存在, 去旧的虚拟DOM结构里找到key标记的标签, **复用标签**
-   新DOM里数据的key存在, 去旧的虚拟DOM结构里没有找到key标签的标签, **创建/插入**
-   旧DOM结构的key, 在新的DOM结构里没有了, 则 **移除key所在的标签**

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a80be077f0f44a21b3085da607cdffc0~tplv-k3u1fbpfcp-watermark.image?)

**问：** 在实际开发过程中，每次通过v-for进行数据的遍历都得用id吗？

**答：** 数组对象中，有id就用id，没有id则用索引。如果用id页面报错，则换成索引。

### 🏷️9.4 ❣️面试题

**问：** 如何理解Vue中的diff算法？

**答：** 在js中，渲染真是`DOM`的开销是非常大的，比如我们修改了某个数据，如果直接渲染到真实`DOM` ,会引起整个`DOM`树重绘和重排。那么有没有可能实现只更新我们修改的那一小块`DOM`二不要更新整个`DOM`呢?此时我们就需要先根据真实`DOM`生成虚拟`DOM`，当虚拟`DOM`某个节点的数据改变后会生成有一个新的`VNode`，然后新的`VNode`和旧的`VNode`作比较，发现有不一样的地方就直接修改在真实DOM上，然后旧的`VNode`的值为新的`VNode`；（找不同！）