![Video_2022-07-02_203708.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/04400f651a6d446087b9c7aae56a3680~tplv-k3u1fbpfcp-watermark.image?)

怎样实现一个旋转的彩色3D方块呢，可以根据css的空间转换特性，利用transform实现元素在空间中的平移、旋转、缩放，再为盒子添加transform-style: preserve-3d属性后可以将盒子里的内容立体呈现，最后加上动画效果让其循环旋转，这样就制作成功了。

## 基础知识
空间：是从坐标轴角度定义的。x轴与y轴构成了平面，再加上z轴就构成了3D立体空间

![x，y轴.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c3a9e3c6c3e84242a9cc1116f4633d8f~tplv-k3u1fbpfcp-watermark.image?)
![x，y，z，轴.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e22f97fe0a854078bfb343ca31e72e5a~tplv-k3u1fbpfcp-watermark.image?)

    这里的各轴的正值朝向分别为：x轴向右，y轴向下，z轴向前

空间位移：使用translate实现元素在空间中的位移

```css
        div {
        /* X轴位移 */
        transform: translateX(100px);
        /* Y轴位移 */
        transform: translateY(100px);
        /* Z轴位移 */
        transform: translateZ(100px);
        /* 多重位移 */
        transform: translate3d(100px, 100px, 100px);
      }
```
空间旋转：使用rotate实现元素在空间中的旋转

```css
        div {
        /* X轴旋转 */
        transform: rotateX(45deg);
        /* Y轴旋转 */
        transform: rotateY(45deg);
        /* Z轴旋转 */
        transform: rotateZ(45deg);
        /* 自定义旋转轴向，这里的是x、y轴对角线旋转 */
        transform: rotate3d(1, 1, 0, 45deg);
      }
```
    判断旋转方向: 左手握住旋转轴, 拇指指向正值方向, 手指弯曲方向为旋转正值方向


![左手法则.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/781cc6d6e1634685b96399664a66b1b1~tplv-k3u1fbpfcp-watermark.image?)

透视（视距）：使用perspective属性实现透视效果

```css
body {
        /* 因为浏览器是一个平面，所以无法直观的展示Z轴的位移，加上视距（透视）perspective后，
        可以有近大远小的效果，perspective的取值一般在800px-1200px */
        perspective: 800px;
      }
```
立体呈现：使用transform-style: preserve-3d呈现立体图形

```css
div {
        width: 200px;
        height: 200px;
        transform-style: preserve-3d;
      }
```
动画效果：先用@keyframes定义动画，再在要使用动画效果的元素里用animation调用以定义的动画。

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/523dbec34c1e4a09a3824721833a69db~tplv-k3u1fbpfcp-watermark.image?)

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/828a6325f529446aaf91455e0e3ddd24~tplv-k3u1fbpfcp-watermark.image?)
## 基础思路
先构造方块的六个面，分别命名为xRight,xLeft,yBottom,yTop,zBefore,zAfter，把它们定位到同一个位置；首先操作x轴上的两个面，让它们分别向x轴的两边移动到与中间的面接壤，然后再对两个面进行翻转，让其垂直于x轴；y轴上的两个面与x轴的同理，先向上下移动到接壤位置，再翻转到垂直于y轴；z轴则是向前后移动，不用进行翻转。

好的，现在理论存在，开始实践！

## 步骤
第一步：构造出方块的六个面，并把它们全都定位到初始位置，再为body设置黑色的背景，这样会让我们的盒子看着更好看一些。

```html
<body>
    <div class="box">
      <div class="xRight"></div>
      <div class="xLeft"></div>
      <div class="yBottom"></div>
      <div class="yTop"></div>
      <div class="zBefore"></div>
      <div class="zAfter"></div>
    </div>
  </body>
```

```css
<style>
      body {
        perspective: 1200px;
        background-color: #000;
      }
      .box {
        position: relative;
        width: 200px;
        height: 200px;
        margin: 150px auto;
        background-color: #fff;
        transform-style: preserve-3d;
        animation: move 5s linear infinite;
      }
      .box > div {
        position: absolute;
        top: 0;
        left: 0;
        width: 200px;
        height: 200px;
      }
    </style>
```

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ed69f9ce17dd4f11aca53fcedb1c293d~tplv-k3u1fbpfcp-watermark.image?)
第二步：操作x轴上的两个面，先给它们设置不同的背景颜色，并让背景色有一定的透明度（这也是为了方便观察我们旋转的方块），先对这两个面沿x轴进行移动，需要移动本身宽度的一半，因为进行翻转时是以当前面的中心来翻转的，所以当前面的中心与原位置面的左右边齐平就行；再让两个面沿着y轴进行旋转。

```css
      .xRight {
        transform: translateX(100px) rotateY(90deg);
        background-color: rgba(255, 192, 203, 0.5);
      }
      .xLeft {
        transform: translateX(-100px) rotateY(90deg);
        background-color: rgba(238, 130, 238, 0.5);
      }
```
![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b78c0b2ff3cb443d8df6ff234b669d34~tplv-k3u1fbpfcp-watermark.image?)

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9835def432a646519a3b50e2f291ed77~tplv-k3u1fbpfcp-watermark.image?)
![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/41ce4c2b927d49b1aa99dc11f33def82~tplv-k3u1fbpfcp-watermark.image?)

第三步：操作y轴上的两个面，先给它们设置不同的背景颜色，并让背景色有一定的透明度（同上），先对这两个面沿y轴进行移动，同样需要移动本身高度的一半，因为进行翻转时是以当前面的中心来翻转的，所以当前面的中心与原位置面的上下边齐平就行；再让两个面沿着x轴进行旋转。

```css
      .yBottom {
        transform: translateY(100px) rotateX(90deg);
        background-color: rgba(135, 207, 235, 0.5);
      }
      .yTop {
        transform: translateY(-100px) rotateX(90deg);
        background-color: rgba(47, 47, 187, 0.5);
      }
```
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58b40a43fd034b81a443059f5ae447b0~tplv-k3u1fbpfcp-watermark.image?)
![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2ba9b5e7bdbb47df8a536f9a2237b71e~tplv-k3u1fbpfcp-watermark.image?)
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/623e66caf61342d992a33e30f0ef2dea~tplv-k3u1fbpfcp-watermark.image?)

第四步：操作z轴上的两个面，同样先给它们设置不同的背景颜色，并让背景色有一定的透明度（同上），然后对这两个面沿z轴进行移动，同样需要移动本身宽度的一半即可，这两个面就是正对我们的，就不用进行旋转了；当这一步完成后，一个完整的3D方块就呈现在我们面前了。

```css
      .zBefore {
        transform: translateZ(100px);
        background-color: rgba(144, 238, 144, 0.5);
      }
      .zAfter {
        transform: translateZ(-100px);
        background-color: rgba(0, 100, 0, 0.5);
      }
```
![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7726755deb6248a3a8050785ffb5b4f7~tplv-k3u1fbpfcp-watermark.image?)
![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b5d8b6791a0745a8906b14d7f355b087~tplv-k3u1fbpfcp-watermark.image?)

对了，要记得把原本方便观察的白色背景去掉啊。

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/a02c061f369445e29c20c470fa391373~tplv-k3u1fbpfcp-watermark.image?)

第五步：这时一个彩色的3D方块已经出现在我们的屏幕上了，要让它旋转起来，只需要最后给它加一个动画效果就好啦。

定义一个动画效果：

```css
      @keyframes move {
        0% {
          transform: rotate3d(0, 0, 0, 0);
        }
        100% {
          transform: rotate3d(1, 1, 0, 360deg);
        }
      }
```
在父盒子里调用定义的动画，设置动画一次的完成时间为5s,旋转速度为匀速，并让其无限循环：

```css
.box {
        position: relative;
        width: 200px;
        height: 200px;
        margin: 150px auto;
        transform-style: preserve-3d;
        animation: move 5s linear infinite;
      }
```
## 完整代码
最后来看一下完整代码吧：

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <style>
      body {
        perspective: 1200px;
        background-color: #000;
      }
      .box {
        position: relative;
        width: 200px;
        height: 200px;
        margin: 150px auto;
        transform-style: preserve-3d;
        animation: move 5s linear infinite;
      }
      .box > div {
        position: absolute;
        top: 0;
        left: 0;
        width: 200px;
        height: 200px;
      }
      .xRight {
        transform: translateX(100px) rotateY(90deg);
        background-color: rgba(255, 192, 203, 0.5);
      }
      .xLeft {
        transform: translateX(-100px) rotateY(90deg);
        background-color: rgba(238, 130, 238, 0.5);
      }
      .yBottom {
        transform: translateY(100px) rotateX(90deg);
        background-color: rgba(135, 207, 235, 0.5);
      }
      .yTop {
        transform: translateY(-100px) rotateX(90deg);
        background-color: rgba(47, 47, 187, 0.5);
      }
      .zBefore {
        transform: translateZ(100px);
        background-color: rgba(144, 238, 144, 0.5);
      }
      .zAfter {
        transform: translateZ(-100px);
        background-color: rgba(0, 100, 0, 0.5);
      }
      @keyframes move {
        0% {
          transform: rotate3d(0, 0, 0, 0);
        }
        100% {
          transform: rotate3d(1, 1, 0, 360deg);
        }
      }
    </style>
  </head>
  <body>
    <div class="box">
      <div class="xRight"></div>
      <div class="xLeft"></div>
      <div class="yBottom"></div>
      <div class="yTop"></div>
      <div class="zBefore"></div>
      <div class="zAfter"></div>
    </div>
  </body>
</html>

```
## 结语
学习完一个知识点后掌握它最好的办法就是实践，画出这个旋转方块后我对新知识的掌握程度又多了很多啦。