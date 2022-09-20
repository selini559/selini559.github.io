# 🌄vue04
## 🏝️1. 监听器watch
### 🏷️1.1 语法
```vue
watch: {
        '被监听的变量(属性)名' (newValue, oldValue) {
          // newValue: 监听的这个变量更改后的值
          // oldValue: 监听的这个变量更改前的值
        }
      }
```
监听器的作用： 监视变量（data，计算属性）。当监听器的变量发生变化时，就会触发当前监听器中设置的逻辑

### 🏷️1.2 例子🌰
```vue
<template>
  <div>
     <input type="text" v-model="str">
  </div>
</template>

<script>
export default {
  name: 'demo-11',
  data () {
    return {
      str: ''
    }
  },
  watch: {
    'str' (newValue, oldValue){
      console.log(newValue, oldValue)
      console.log(this.str)
    }
  }
}
</script>
```
使用后其实会发现，我们最常用的应该是newValue， 而oldValue往往会用在对比新旧数据的差异上，newValue与监听的目标变量其实并无区别

总结发现：只要不进行新旧数据的对比，就可以不传任何参数

### 🏷️1.3 深度监听

监听复杂数据类型时，发现newvalue和oldvalue都是新数据

这是因为复杂数据类型的数据存在堆内存中，而监听的目标则是栈中的堆内存地址

所以说当堆中的数据发生变化时， 不管是newValue栈中的地址还是oldvalue栈中的地址，都指向同一个堆，没有旧数据的记录

这种时候就可以启用深度监听

举个例子🌰

```vue
<template>
  <div>
     <input type="text" v-model="form.name">
  </div>
</template>

<script>
export default {
  name: 'demo-11',
  data () {
    return {
      form: {
        name: ''
      }
    }
  },
  watch: {
    'form': {
      handler (newValue, oldValue){
        console.log(newValue, oldValue)
      },
      deep: true,  // 启动深度监听复杂数据类型
      immediate: true  // 立即执行监听 - 当监听器生成时，会立即执行一次handler中的逻辑
    }
  }
}
</script>
```
### 🏷️1.4 结论
今后如何使用监听器：
1. 如果不做新旧数据的对比，不用传任何参数
2. 如果发现监听器设置后并没有监听到任何数据，转化为深度监听

## 🏝️2. vue组件
### 🏷️2.1 概念
**组件化** ：封装的思想，把页面上`可重用的部分`封装为`组件`，从而方便项目的开发和维护

组件是可复用的VUE实例, 封装标签(HTML), 样式(CSS)和JS，每个组件都是一个独立的个体

### 🏷️2.2 组件的使用
1. 创建组件 - 封装标签+样式+js - 组件都是独立的, 为了复用

2. 注册组件 - 创建后需要注册后再使用

   - 全局注册

     ```js
     // 目标: 全局注册 (一处定义到处使用)
     // 1. 创建组件 - 文件名.vue
     // 2. 引入组件
     import Pannel from './components/Pannel'
     // 3. 全局 - 注册组件
     /*
       语法: 
       Vue.component("组件名", 组件对象)
     */
     Vue.component("PannelG", Pannel)
     ```

   - 局部注册

     ```vue
     <template>
       <div id="app">
         <h3>折叠面板</h3>
         <!-- 组件名当做标签使用 -->
         <!-- <组件名></组件名> -->
         <PannelG></PannelG>
         <PannelL></PannelL>
       </div>
     </template>
     
     <script>
         // 目标: 局部注册 (用的多)
         // 1. 创建组件 - 文件名.vue
         // 2. 引入组件
         import Pannel from './components/Pannel_1'
         export default {
             // 3. 局部 - 注册组件
             /*
                 语法: 
                 components: {
                   "组件名": 组件对象
                 }
             */
             components: {
                 PannelL: Pannel
             },
             /*  
                 当标签名和import引入组件名称相同是可以简写
             */
             components: {
                 Pannel
             }
         }
     </script>
     ```

### 🏷️2.3 CSS中的scoped作用

在style上加入scoped属性, 就会在此组件的标签上加上一个随机生成的data-v-hash开头的属性。保证了必须是当前组件的元素, 才会有这个自定义属性, 才会被这个样式作用到

```vue
<style scoped></style>
```

## 🏝️3. vue组件通信

### 🏷️3.1 父传子

#### 3.1.1 props

**步骤：**

1. 创建组件 components/MyProduct.vue

2. 在父组件中注册MyProduct.vue子组件， 在使用时传入具体的数据

   ```vue
   <template>
     <div>
       <MyProduct></MyProduct>
     </div>
   </template>
   
   <script>
   import MyProduct from './com/myProduct.vue'
   export default {
     name: 'demo-02',
     components: {
       MyProduct
     }
   }
   </script>
   ```

   

3. 子组件内在props属性中定义变量, 用于接收外部传入的值

   ```vue
   <template>
     <div class="my-product">
       <h3>标题: {{ title }}</h3>
       <p>价格: {{ price }}元</p>
       <p>{{ intro }}</p>
     </div>
   </template>
   
   <script>
   export default {
     props: ['title', 'price', 'intro']
   }
   </script>
   ```

   

4. 父组件中的组件标签中传入不同的值

   ```vue
   <MyProduct title="西瓜" price="2" content="5块钱两斤，2块钱一斤"></MyProduct>
   ```

   

**总结：**

父传子的流程

1. 子组件内, props定义变量, 在子组件使用变量
2. 父组件内, 使用子组件, 属性方式给props变量传值

#### 3.1.2 动态属性传值

```vue
<template>
  <div>
    <MyProduct :title="title" :price="price" :content="content"></MyProduct>
  </div>
</template>

<script>
import MyProduct from './com/myProduct.vue'
export default {
  name: 'demo-02',
  components: {
    MyProduct
  },
  data () {
    return {
      title: '葡萄',
      price: '5',
      content: '买一送一，童叟无欺'
    }
  }
</script>
```

### 🏷️3.2 ❣️单向数据流

**概念：**从父到子的数据流向，叫做单项数据流

**在vue中需要遵循单向数据流原则：**

1. 子组件原则上不允许更新父组件传递过来的参数

2. 如果修改的是父组件传递过来的对象的属性时是可以进行修改的

**原因：**

- 其实不允许子组件修改父组件传递过来参数的部分，是这些参数的栈内存中的数据
- 但是我们可以越过栈内存，通过点语法的形式直接修改引用数据类型存储在堆内存中的真实数据

**子组件修改父组件传过来对象属性的方式：**

在子组件的data中，拷贝一个父组件传过来的对象，通过大家都有相同的堆地址，来间接地修改父组件中的对象参数

例子🌰

父：

```vue
<template>
  <div>
    <MyProduct v-for="(obj, index) in arr"
    :key="index"
    :title="obj.title"
    :price="obj.price"
    :content="obj.content"
    :obj="obj"
    ></MyProduct>
  </div>
</template>

<script>
import MyProduct from './com/myProduct.vue'
export default {
  name: 'demo-02',
  components: {
    MyProduct
  },
  data () {
    return {
      title: '葡萄',
      price: '5',
      content: '买一送一，童叟无欺',
      arr: [
        {title: '柠檬', price: '3', content: '两个5块了啊'},
        {title: '冬枣', price: '8', content: '全场八折，全场八折'},
        {title: '蜜桔', price: '6', content: '骨折价，走过路过不要错过'}
      ]
    }
  }
}
</script>
```

子：

```vue
<template>
  <div class="my-product">
    <h3>标题: {{ title }}</h3>
    <p>价格: {{ price }} 元</p>
    <p>描述: {{ content }}</p>

    <button @click="objClone.price--">拼刀刀，砍一刀</button>
  </div>
</template>

<script>
export default {
  name: 'myProduct',
  props: ['title', 'price', 'intro'],
  data () {
    return {
      objClone: this.obj
    }
  }
}
</script>

<style>
.my-product {
  width: 400px;
  padding: 20px;
  border: 2px solid #000;
  border-radius: 5px;
  margin: 10px;
}
</style>
```

### 🏷️3.3 子向父 - $emit

子传父的步骤：

1. 子组件需要主动的触发一个自定义的事件(这个自定义事件是装载在父组件中子组件标签上的)

​     this.$emit('自定义事件名', 希望传递给父组件的参数)

2. 在父组件的子组件标签中定义这个自定义事件以及绑定一个方法

    <子组件 @自定义事件名="在methods自定方法" />

   通过以上2步操作，就可以让子组件来使用父组件绑定的方法

例子🌰

父：

```vue
<template>
  <div>
    <MyProduct v-for="(obj, index) in arr"
    :key="index"
    :title="obj.title"
    :price="obj.price"
    :content="obj.content"
    :obj="obj"
    @subPrice="subPriceFn"
    ></MyProduct>
  </div>
</template>

<script>
import MyProduct from './com/myProduct.vue'
export default {
  name: 'demo-02',
  components: {
    MyProduct
  },
  data () {
    return {
      arr: [
        {title: '柠檬', price: '3', content: '两个5块了啊'},
        {title: '冬枣', price: '8', content: '全场八折，全场八折'},
        {title: '蜜桔', price: '6', content: '骨折价，走过路过不要错过'}
      ]
    }
  },
  methods: {
    subPriceFn (title) {
      console.log(title)
      this.arr.forEach(item => {
        if (item.title === title) {
          item.price--
        }
      })
    }
  }
}
</script>
```

子：

```vue
<template>
  <div class="my-product">
    <h3>标题: {{ title }}</h3>
    <p>价格: {{ price }} 元</p>
    <p>描述: {{ content }}</p>

    <button @click="objClone.price--">拼刀刀，砍一刀</button>
    <button @click="btn">拼刀刀，砍一刀</button>
  </div>
</template>

<script>
export default {
  name: 'myProduct',
  props: ['title', 'price', 'intro'],
  methods: {
    btn () {
      this.$emit('subPrice', this.title)
    }
  }
}
</script>

<style>
.my-product {
  width: 400px;
  padding: 20px;
  border: 2px solid #000;
  border-radius: 5px;
  margin: 10px;
}
</style>
```

### 🏷️3.1 props的进阶写法：

props也可以作为一个对象，并且可以指定数据类型，必要性，默认值

举个例子🌰

```vue
<script>
export default {
  name: 'myProduct',
  props: {
    title: {
      type: String,
      default: ''
    },
    price: {
      type: Number,
      default: 0
    },
    content: {
      type: String,
      default: ''
    },
    // 对象的默认值
    obj: {
      type: Object,
      default: () => ({})
    },
    // 数组的默认值
    arr: {
      type: Array,
      default: () => []
    }
  }
</script>
```

