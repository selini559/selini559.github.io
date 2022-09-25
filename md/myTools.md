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

