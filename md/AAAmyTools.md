selini 的 <font color='#f80' size='6'>百宝箱</font>

## ✨全选反选

```vue
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
  // 全选、小选互选，使用时修改obj.c属性以及arr数组名称即可
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
  // 反选
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

## ✨增删改查

以todoList为例

```vue
<script>
export default {
  data () {
    return {
      list: JSON.parse(localStorage.getItem('TODO_LIST')) || []
    }
  },
  watch: {
    'list' () {
      localStorage.setItem('TODO_LIST', JSON.stringify(this.list))
    }
  },
  methods: { 
    // 添加任务
    addTaskFn(task) {
      // 判断内容不能为空
      if (this.task.trim().length <= 0) {
        alert('输入内容不能为空!')
        return
      }
        
      // 向任务列表添加新任务
      let tempObj = {
        id: this.list.length === 0 ? 100 : (this.list[this.list.length - 1].id + 1),
        name: task,
        isDone: false
      }
      this.list.push(tempObj)
        
      // 添加完成后，清空输入框内容
      this.task = ''
    },
      
    // 删除任务
    delTaskFn(taskId){
      let delIndex = this.list.findIndex(obj => obj.id === taskId)
      this.list.splice(delIndex, 1)
    },
    // 删除任务(方法二)
    delTaskFn2(taskId){
      this.list = this.list.filter(obj => obj.id !== taskId)
    }
      
    // 清空已完成
    clearAllFn() {
      this.list = this.list.filter(obj => obj.isDone === false)
    }
  }
}
</script>
```



## ✨ajax请求

**main.js**

```js
// 全局引入axios
import axios from 'axios'
// 请求默认根路径
axios.defaults.baseURL = 'https://192.168.1'
// 自定义vue实例的内部方法
Vue.prototype.$axios = axios
```

**父组件**

```vue
<script>  
  // 在初始化结束阶段发送请求
  created () {
    this.getShopcarList()
  },
  // 封装请求方法
  methods: {
    getShopcarList() {
      this.$axios({
        method: 'GET',
        url: '/api/get'
      }).then(res => {
        console.log(res.data)
        this.list = res.data.data
      }).catch(err => {
        console.log(err)
      })
    }
  }
</script>
```

## ✨路由

**main.js**

```js
// 1. 通过npm i vue-router@3.5.1 安装依赖， 注意：vue2的项目一定在安装的过程中要输入版本号

// 2. 引入路由
import VueRouter from 'vue-router'

// 3. Vue.use() 静态方法来使用路由
Vue.use(VueRouter)
// 3.1 额外配置，隐藏编程式导航重复跳转时，控制台的警告
// 解决vue路由重复导航错误
const originalPush = VueRouter.prototype.push
// 修改原型对象中的push方法
VueRouter.prototype.push = function push(location) {
  return originalPush.call(this, location).catch(err => err)
}

// 4. 创建路由规则数组
// 4.1 引入组件
import Find from './views/find.vue'
import My from './views/my.vue'
import Part from './views/part.vue'
// 4.2 创建数组
/* 注意：
  1. 尽量保持path路由与组件名称一致
  2. 路由规则数组的变量名要求固定写出routes，因为在实例化路由的过程当中，需要使用routes这个变量名进行解构赋值
*/
let routes = [
  {
    path: '/find', // 路由 设置路由时，一定要加/
    component: Find, // 绑定对应组件 组件实例对象
  },
  {
    path: '/my',
    component: My
  },
  {
    path: '/part',
    component: Part
  }
]

// 5. 生成路由对象（传入配置对象）
// 注意：3. 生成路由对象的变量名 router，固定
const router = new VueRouter({
  routes, 
})

// 6. 挂载到vue实例化对象上
new Vue({
  router
})
```

**APP.vue**

```vue
<!-- 7. 通过在组件中使用 <router-view></router-view> 标签来装载需要切换的路由组件内容，其使用效果与 动态组件<component>标签一致 -->
<div class="top">
  <!-- 动态组件用 component 标签来切换 -->
  <!-- 路由则使用 router-view 来进行切换 -->
  <router-view></router-view>
</div>
```

