上一次用css画了一个彩色方块，又想画一个更有意思的方块，于是我想到了色子，六个面，不同的点数，画一个这个应该会挺有意思的。
## 理论知识准备
要写色子每个面上的点，就需要用到一个新的知识点，flex弹性盒子布局。接下来就是知识点输出：

-   flex属性：让多个元素一行排列，顶端对齐；多个块级元素之间没有缝隙；不会脱标，占据位置。
>display: flex;  将当前元素添加flex属性，转换为弹性容器，子元素成为弹性盒子，可以对弹性容器里的弹性盒子进行弹性布局。

-   justify-content  主轴对齐方式，默认从左到右排列
> -   justify-content: flex-start;  默认值，起点到终点
> -   justify-content: flex-end;  终点到起点
> -   justify-content: center;  沿主轴居中排列
> -   justify-content: space-between;  第一个元素在起点，最后一个元素在终点，剩余空间均匀分布在弹性盒子之间
> -   justify-content: space-around;  沿主轴均匀排列，父元素剩余空间均分在弹性盒子两侧，整体效果，两边窄，中间宽
> -   justify-content: space-evenly;  沿主轴均匀排列，弹性盒子的间距以及与容器的间距相等

-   align-items  侧轴对齐方式
> -   align-items: strench;  默认值，当弹性盒子没有高度时，拉伸成父盒子高度
> -   align-items: flex-start;  沿着侧轴方向，从起点到终点排列
> -   align-items: flex-end;  沿着侧轴方向，从终点到起点排列
> -   align-items: center;  沿着侧轴方向居中排列

-   flex-direction  改变主轴方向
> -   flex-direction: row;  默认主轴方向，从左到右
> -   flex-direction: row-reverse;  改变主轴方向为从右到左
> -   flex-direction: column;  改变主轴方向为从上到下
> -   flex-direction: column-reverse;  改变主轴方向为从下到上

-   flex注意点：
> -   当块级元素作为弹性盒子（子元素），没有设置宽度时，宽度由父级100%变成由实际内容撑开
> -   当行内元素作为弹性盒子（子元素），可以直接设置宽高
> -   当行内元素作为弹性容器（父元素），可以直接设置宽高

理论知识已经准备好了，接下来就开始画出我们的色子。
## 一点
先在html里写出一点的色子结构。我们在每一个面和点的命名时，可以写两个类名，一个用于单独修改自身样式，一个用于样式复用。

```html
      <!-- 点数为1的布局 -->
      <div class="pointOne side">
        <div class="row circle"></div>
      </div>
```
使用less写出样式，给父盒子flex属性后，再让中间的圆点水平垂直居中。

```css
// 一点
// 每一个面的样式，复用
.side {
  width: 200px;
  height: 200px;
  margin: 100px auto;
  padding: 10px;
  background-color: #fff;
  border-radius: 20px;
  box-shadow: 0 0 5px 8px #f6f6f6 inset;
}
// 点的样式，复用
.circle {
  width: 40px;
  height: 40px;
  background-color: #333;
  border-radius: 50%;
}
.pointOne {
  display: flex;
  justify-content: center;
  align-items: center;
}
```
色子的一点样式就出来了

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d882e3baa304402e9cc747311871559b~tplv-k3u1fbpfcp-watermark.image?)

## 两点
先在html里写出两点的色子结构

```html
<!-- 点数为2的布局 -->
      <div class="pointTwo side">
        <div class="row1 circle"></div>
        <div class="row2 circle"></div>
      </div>
```
用less写出样式让两个点沿主轴两端排列，再给第一个点侧轴起始位置，第二个点侧轴末尾位置。

```less
// 点数为2的布局
.pointTwo {
  display: flex;
  justify-content: space-between;

  .row1 {
    align-self: flex-start;
  }
  .row2 {
    align-self: flex-end;
  }
}
```
色子的两点样式就出来了

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5b7d50d56f70418ca3a42772578ad248~tplv-k3u1fbpfcp-watermark.image?)

## 三点
先在html里写出三点的色子结构

```html
<!-- 点数为3的布局 -->
      <div class="pointThree side">
        <div class="row1 circle"></div>
        <div class="row2 circle"></div>
        <div class="row3 circle"></div>
      </div>
```
用less写出样式让三个点沿主轴均匀排列，再让三个点在侧轴上也均匀排列。

```less
// 点数为3的布局
.pointThree {
  display: flex;
  justify-content: space-between;

  .row1 {
    align-self: flex-start;
  }
  .row2 {
    align-self: center;
  }
  .row3 {
    align-self: flex-end;
  }
}
```
色子的三点样式就出来了

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b5b594ddcb3548f599fb97e5a08ee6f1~tplv-k3u1fbpfcp-watermark.image?)
## 四点
先在html里写出四点的色子结构，由于四点与前三个样式有一定区别，这里我们可以写两个横向的盒子，一个盒子里装两个点，方便我们书写样式。

```html
<!-- 点数为4的布局 -->
      <div class="pointFour side">
        <div class="row1">
          <div class="column circle"></div>
          <div class="column circle"></div>
        </div>
        <div class="row2">
          <div class="column circle"></div>
          <div class="column circle"></div>
        </div>
      </div>
```
用less写出四点的样式，首先我们给横向的盒子父级100%的宽度，然后再让盒子里的两个点位于盒子两端；这一步结束后还没有达到四点的样式效果，这时我们在表示这个面的盒子里加一个flex属性，再改变主轴方向，让两个横向盒子也排列于盒子上下两端。
```less
// 点数为4的布局
.pointFour {
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  .row1,
  .row2 {
    display: flex;
    justify-content: space-between;
    width: 100%;
  }
}
```
色子的四点样式就出来了

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/470da0a76f1748eea3d8d06eb7b947ba~tplv-k3u1fbpfcp-watermark.image?)
## 五点
先在html里写出五点的色子结构，和四点结构的思路差不多，给每一行的点都包裹一个横向的盒子，那么在五点结构里就需要三个横向的盒子，结构如下。

```html
<!-- 点数为5的布局 -->
      <div class="pointFive side">
        <div class="row1">
          <div class="column circle"></div>
          <div class="column circle"></div>
        </div>
        <div class="row2">
          <div class="column circle"></div>
        </div>
        <div class="row3">
          <div class="column circle"></div>
          <div class="column circle"></div>
        </div>
      </div>
```
用less写出五点样式的思路也和四点样式的思路差不多，给第一行和第三行里的点一个space-between让其两端排列，给第二行里的点沿主轴居中；再改变主轴方向，让三个横向盒子竖着均匀排列。

```less
// 点数为5的布局
.pointFive {
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  .row1,
  .row2,
  .row3 {
    display: flex;
    justify-content: space-between;
    width: 100%;
  }

  .row2 {
    justify-content: center;
  }
}
```
色子的五点样式就出来了

![image.png](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b64de52e831040a897e291db63a916c4~tplv-k3u1fbpfcp-watermark.image?)
## 六点
先在html里写出六点的色子结构，这个的结构和五点的结构只有一个差别，就是第二行包裹了两个点，其他的结构都是一样的。

```html
<!-- 点数为6的布局 -->
      <div class="pointSix side">
        <div class="row1">
          <div class="column circle"></div>
          <div class="column circle"></div>
        </div>
        <div class="row2">
          <div class="column circle"></div>
          <div class="column circle"></div>
        </div>
        <div class="row3">
          <div class="column circle"></div>
          <div class="column circle"></div>
        </div>
      </div>
```
用less写出样式让三个点沿主轴均匀排列，再让三个点在侧轴上也均匀排列。

```less
// 点数为6的布局
.pointSix {
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  .row1,
  .row2,
  .row3 {
    display: flex;
    justify-content: space-between;
    width: 100%;
  }
```
色子的六点样式就出来了

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/33859fa33d6847ebb8d229632ded468c~tplv-k3u1fbpfcp-watermark.image?)

## 立方体色子

接下来我们就要把这六个面拼成一个立方体，这才有一个色子的样子嘛。

这里的拼接方式和上一篇文章的彩色方块的拼接方式相同，就不过多赘述了；只需分清色子各个面的朝向，按照一点在前的角度来观察的话，应该是一点在前，六点在后，两点在左，五点在右，三点在下，四点在上；按照这个顺序来移动和旋转色子的每个面。

拼接完成后记得给色子加一个动画效果，这样才能完整地观察到色子的每个面，动画效果的添加也与上一篇文章相同。

最后来看看完成后的效果：

![Video_2022-07-13_104953.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e4f895bb71134ae0a4ab986a49466873~tplv-k3u1fbpfcp-watermark.image?)