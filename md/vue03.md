# 🌄vue03

## 🏝️1. 动态class

### 🏷️1.1 语法

-   :class="{ 类名: 布尔值(可以是表达式的返回值) }"

    通过布尔值来判断前面的类名是否生效，也就是通过一个布尔值来做某个类名的开关

-   :class="[ 带有类名字符串的变量 ]"

    可以通过改变这个变量的值，来实现切换不同的类名，也就是通过改变变量中的类名，来切换样式表中的不同的类的样式

如果有一个样式在使用场景中只需要它生效或者不生效，此时选择语法1

如果有一个样式在使用场景中需要实时的变化，此时选择语法2

### 🏷️1.2 例子🌰

```
<template>
  <div>
     <p :class="{red_str: bool}">动态class1</p>  // 红色
     <p :class="[changeClass]">动态class2</p>  // 红色
  </div>
</template>

<script>
export default {
  name: 'demo-05',
  data () {
    return {
      bool: true,
      changeClass: 'red_str'
    }
  }
}
</script>

<style scoped>
  .red_str{
    color: red;
  }
</style>
```

## 🏝️2. 动态style

### 🏷️2.1 语法

-   :style="{ css样式属性名: 携带当前样式的样式值的变量 }"

    通过一个变量来控制当前显示样式的状态

-   :style="[ 带有属性键值对的对象 ]"

    通过这个对象中的值来变化各种样式属性

如果仅需要修改某一个’特定‘ 样式的属性内容，选择语法1

如果需要修改或切换不同的样式种类时， 选择语法2

**注意：** 如果出现多个单词短横线链接的样式属性名时，需要转化为驼峰式命名来设置

### 🏷️2.2 例子🌰

```
<template>
  <div>
     <p :style="{ color: styleColor }">动态style</p>
     <p :style="[ styleObj ]">动态style</p>
  </div>
</template>

<script>
export default {
  name: 'demo-05',
  data () {
    return {
      styleColor: 'pink',
      styleObj: {
        color: 'green',
        backgroundColor: '#ce8'
      }
    }
  }
}
</script>
```

## 🏝️3. ❣️过滤器filter

### 🏷️3.1 语法

0.  全局过滤器（定义在全局，所有的组件都可以使用）

    Vue.filter(

    参数1 - "自定义过滤器名称",

    参数2 - (需要过滤的值-必填, 过滤时传过来的自定义参数-选填) => {

    return '返回处理后的数据'

    })

    **注意：** filter是Vue构造函数的静态方法

0.  局部过滤器(定义在组件中，只有当前的组件才可以使用)

    filters: {

    '自定义过滤器名称' (需要过滤的值-必填, 过滤时传过来的自定义参数-选填) {

    return '返回处理后的数据'

    }

    }

    **注意：** 和data同级的地方有一个属性，叫做filters

**过滤器的作用：** 在不改变data中数据的基础上，在页面上展示不同于数据的内容效果

**过滤器的使用：** 在插值表达式中，通过 ‘|’ 来连接变量和过滤器 --> {{ 变量 | 过滤器(传入自定义的参数) }}

### 🏷️3.2 例子🌰

```
<template>
  <div>
    <div>{{ str | reverseG('&') }}</div>
    <div>{{ str | toUp }}</div>

    <!-- 多个过滤器:vue变量 | 过滤器1 | 过滤器2 -->
    <div>{{ str | toUp | reverseG }}</div>

  </div>
</template>

<script>
export default {
  data () {
    return {
      str: 'hello world'
    }
  },
  filters: {
    // 让字符串所有单词大写
    toUp(value) {
      return value.toUpperCase()
    }
  },
  methods: {
    consoleStr() {
      console.log(this.str)
    }
  }
}
</script>
```

全局过滤器，写在入口文件main.js中

```
// 全局颠倒字符串的过滤器
Vue.filter('reverseG', (value, icon) => {
  // 可以在join中自定义连接符号
  // icon || '' 的意思是如果传了链接符号，那么展示链接符号，如果没传链接符号则不需要拼接符号
  return value.split('').reverse().join(icon || '')
})
```

## 🏝️4. ❣️计算属性computed

### 🏷️4.1 语法

```
computed: {
    '自定义的计算属性名称' () {
         return '计算后返回的值'
        }
   }
```

### 🏷️4.2 例子🌰

**计算属性的使用：** 与data中的变量的使用方式是一样的

**注意事项：** data中的变量与计算属性的名称不可以相同

**计算属性的优缺点：**

-   优点：因为缓存机制，所以不会重复的进行计算，页面效率高
-   缺点：因为缓存机制，计算属性会消耗内存

```
<template>
  <div>
     <div>a: {{ a }}</div>
     <div>b: {{ b }}</div>
     <div>c = a + b : {{ c }}</div>
     <div>c = a + b : {{ c }}</div>
     <div>c = a + b : {{ c }}</div>
     <div>c = a + b : (function) {{ sum() }}</div>
     <div>c = a + b : (function) {{ sum() }}</div>
     <div>c = a + b : (function) {{ sum() }}</div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      a: 10,
      b: 10
    }
  },
  computed: {
    // 计算属性的单引号可加可不加，没有任何影响，只是加上后可以方便自己区分属性和方法
    'c' () {
      console.log('计算属性')
      return this.a + this.b
    }
  },
  methods: {
    sum () {
      console.log('方法')
      return this.a + this.b
    }
  }
}
</script>
```

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0aac77a6a2334d0d96558f7d48e18a7e~tplv-k3u1fbpfcp-watermark.image?)

**计算属性的特点：** 计算属性具有缓存结果的特点，计算属性基于它的依赖项（计算属性中所使用的其他变量）进行计算的结果会缓存起来，只要依赖项的值不变，那么下次使用计算属性时不必进行计算，只会返回缓存中的结果，对于代码效率来说是比较高的

### 🏷️4.3 计算属性完整写法

计算属性完整写法的语法：

```
    computed: {
      "属性名": {
        // 设置 - 当计算属性绑定在某个表单控件的v-model上时，当主动的触发了这个计算属性的变化时，就会执行set方法来改变该方法做所做的业务逻辑
        // set属性拥有非常大的局限性，并不是在各个环境下都可以正常使用的
        set(值 - 计算属性的当前值 == this.属性名){
          // 去修改其他的变量
        },
        
        // 获取 - 获取其他依赖项对计算属性的影响
        get() {
          return "值"
        }
      }
    }
```

多用于复选框的全选同步和反选，例子🌰如下：

```
<template>
  <div>
    <span>全选:</span>
    <input type="checkbox" v-model="isAll"/>
    <button @click="btn">反选</button>
    <ul>
      <li v-for="(obj, index) in arr" :key="index">
        <input type="checkbox" v-model="obj.c"/>
        <span>{{ obj.name }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      arr: [
        {
          name: "猪八戒",
          c: false,
        },
        {
          name: "孙悟空",
          c: false,
        },
        {
          name: "唐僧",
          c: false,
        },
        {
          name: "白龙马",
          c: false,
        }
      ]
    }
  },
  computed: {
    'isAll': {
      set(value) {
        this.arr.forEach(obj => {
          obj.c = value
        })
      },
      get () {
        let flag = this.arr.every(obj => obj.c)
        return flag
      }
    }
  },
  methods: {
    btn () {
      this.arr.forEach(obj => {
        obj.c = !obj.c
      })
    }
  }
}
</script>
```
