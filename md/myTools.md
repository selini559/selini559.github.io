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

