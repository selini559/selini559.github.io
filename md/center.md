温故而知新，温故而知新，这篇文章来总结一下css中让元素水平垂直居中的7种基本方式，分为知道宽高的情况下的居中方式，和不知道宽高的情况下的居中方式

下面是html的结构，放在这里，下面就不重复放置了

```html
<body>
    <div class="father sizeOfFather">
        <div class="son sizeOfSon">lazy dog</div>
    </div>
</body>
```
这里用sizeOfFather和sizeOfSon设置父元素和子元素的宽高，下面是他们的css样式
```css
<style>
        .sizeOfFather{
            width: 600px;
            height: 600px;
            background-color: #eee;
        }
        .sizeOfSon{
            width: 100px;
            height: 100px;
            background-color: #ae8;
        }
    </style>
```
# 不需要知道元素宽高
## flex
flex布局让元素水平垂直居中应该是最常用，并且最简单粗暴的方式了吧。只需给父元素一个flex布局，并且设置主轴侧轴都居中即可
```css
        .father{
            display: flex;
            justify-content: center;
            align-items: center;
        }
        .son{
        }
```
效果图如下，下边效果相同就不再放图片了

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c427f6a12706468785d910e4d2281506~tplv-k3u1fbpfcp-watermark.image?)
## grid
grid网格布局同样可以实现元素的水平垂直居中，同样的简单粗暴，只需要三行代码。
justify-self和align-self设置单个元素自身在父容器中的对齐位置。
```css
        .father{
            display: grid;
        }
        .son{
            justify-self: center;
            align-self: center;
        }
```
## absolute + transform
使用子绝父相给盒子设置定位，让子元素在父元素的定位为上50%、左50%，当然这样设置之后元素整体不在父元素的正中位置，这时就需要让子元素向上和向左再回移自身宽高的50%
```css
        .father{
            position: relative;
        }
        .son{
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
        }
```
当然如果知道子元素的宽高的话，这里translate的50%也可以直接写宽高的一半
```css
        .father{
            position: relative;
        }
        .son{
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50px, -50px);
        }
```
## absolute + top/right/bottom/left: 0 + margin: auto
使用定位让元素水平垂直居中还可以配合margin: auto来实现，这时我们就需要让子元素在top/right/bottom/left四个方向的定位都为0，这样设置在使用margin: auto时才可以在四个方向上都居中
```css
        .father{
            position: relative;
        }
        .son{
            position: absolute;
            top: 0;
            right: 0;
            bottom: 0;
            left: 0;
            margin: auto;
        }
```
## table-cell
把子元素转换为行内元素，给父元素设置文本居中(text-align: center)和对齐方式居中(vertical-align: middle)即可让子元素水平垂直居中
```css
        .father{
            display: table-cell;
            text-align: center;
            vertical-align: middle;
        }
        .son{
            display: inline-block;
        }
```
# 需要知道元素宽高
## absolute + 负margin
绝对定位的50%并不能让子元素完全居中，在不知道宽高的时候我们可以用transform: translate(-50%, -50%)来实现居中，在知道宽高的情况下我们还可以使用负margin的方法，把子元素往回移动自身宽高的一半
```css
        .father{
            position: relative;
        }
        .son{
            position: absolute;
            top: 50%;
            left: 50%;
            margin-top: -50px;
            margin-left: -50px;
        }
```
当然不止可以设置左边和上边的，右边和下边的同样可以
```css
        .father{
            position: relative;
        }
        .son{
            position: absolute;
            right: 50%;
            bottom: 50%;
            margin-right: -50px;
            margin-bottom: -50px;
        }
```
## absolute + calc
calc()方法可以在声明CSS属性值时执行一些计算，我们在写定位的距离时使用calc()方法就可以直接实现水平垂直居中

但是要注意，在calc()方法里，在+和-运算符左右一定要写空格，不这样的话不能正确解析表达式
```css
        .father{
            position: relative;
        }
        .son{
            position: absolute;
            top: calc(50% - 50px);
            left: calc(50% - 50px);
        }
```
# 总结
目前就写这么多吧，希望自己要常常来回顾，温故而知新