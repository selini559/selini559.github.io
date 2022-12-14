# 🌄vue的生命周期

vue的生命周期是什么？

简单来说，vue的生命周期就是一个vue组件从创建到销毁的全过程，经历了初始化、挂载、更新、最后销毁这四个阶段。

其中包含了8个生命周期钩子，也叫生命周期函数

## 🏝️生命周期图示

从网上找到的有中文注释的图，先简单了解一下，下面详细介绍

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4bf430c5d34a449ab80afd1f975aa2e4~tplv-k3u1fbpfcp-zoom-1.image)

## 🏝️初始化阶段

### 🏷️beforeCreate(初始化前)

此时vue实例刚被创建出来，实例中data和methods里的数据和方法都还没有被初始化，无法访问到

### 🏷️❣️created(初始化后)

实例已经在内存中创建完毕，data、method、coputed这些都创建完成了，此时可以访问到data中的数据、method中的方法、computed中的计算属性等等。但此时还未开始编译模板，所以无法访问到页面上的dom元素。

那么处理静态数据，向后端发送ajax请求，注册全局事件这一些操作则可以在这里进行，created是常用的生命周期函数之一。

## 🏝️挂载阶段

### 🏷️beforeMount(挂载前)

此时模板的编译已经完成，但此时的dom只在内存中，还未挂载到页面上。此时乐意访问数据和方法，仍然不能访问到dom元素，与created能执行的一样

### 🏷️❣️mounted(挂载后)

此时把已编译好的dom挂载到页面上了，已经可以看到渲染好的页面了，那么这个时候我们再去访问dom元素就能成功访问到了，此时就很适合我们去做一些dom操作。

如果在编写代码过程中，不确定是否需要dom操作时，那么把逻辑写在mounted中就行，不会有错。

mounted也是常用的生命周期函数之一。

## 🏝️更新阶段

更新阶段的两个钩子函数只有数据发生改变时才会触发，是不会自己触发的

### 🏷️beforeUpdate(更新前)

此时页面还没有被更新，但数据已经改变了，也就是说，页面中的数据还是旧的，但是data中的数据已经是新的了，例如此时如果访问dom的内容的话还是旧的数据。

### 🏷️updated(更新后)

此时页面中的数据和data中的数据已经保持同步了，都是最新的数据，那么此时如果访问dom的内容就是已经更新后的数据了。

在update阶段做业务操作时，会产生无限的更新循环，所以如果以后需要在数据变化时做业务操作，可以用监听器watch来实现。

## 🏝️销毁阶段

### 🏷️❣️beforeDestroy(销毁前)

此时vue实例进入销毁阶段，但实例中的data、method、指令等都是可用的，一般可以在这里关闭定时器、解绑自定义事件、移除事件监听等。

beforeDestroy也是常用的钩子函数。

### 🏷️destroyed(销毁后)

此时vue实例已销毁，示例中的所有data、method、指令等都不可用了，所有该解绑的解绑，该移除的移除。

至此，一个vue实例的生命周期就走完了，从创建到销毁，他挥一挥衣袖，不带走一丝云彩。

## 🏝️补充：keep-alive相关钩子函数

Vue内置的keep-alive组件, 可以让包裹的组件保存在内存中不被销毁，使用keep-alive组件可以使被缓存的组件不再创建和销毁，而是激活和非激活状态。

当我们遇到一些需要频繁切换的组件时，可以使用keep-alive来避免频繁渲染，这样可以提高组件的性能。

用法：

```
<div>
    <!-- Vue内置keep-alive组件, 把包起来的组件缓存起来 -->
    <keep-alive>
        <component :is="comName"></component>
    </keep-alive>
</div>
```

该组件中有一个动态属性 :is, 与他绑定的变量的值为当前显示组件的组件名称（在components属性中所定义的组件名称）

### 🏷️activated(激活)

activated钩子函数在切换到当前组件时触发，也就是在什么情况下需要请求数据，什么时候直接使用缓存的数据。

在缓存组件中，有些需要进入组件时就执行的代码从created和mounted中转换到activated里。

### 🏷️deactivated(非激活)

deactivated钩子函数，组件变为不可用时触发。

在缓存组件中，如果有计时器定时器需要在页面关闭时主动关闭，需要将关闭的代码从beforeDestroy中转换到deactivated里。
