---
title: 关于 Css3 Flex 浅析
date: 2018-08-28 11:25:41
categories: css
tags:
- css3
- flex
author: kun
---


布局的传统解决方案，基于盒状模型，依赖 display属性 + position属性 + float属性。它对于那些特殊布局非常不方便，比如，[垂直居中](https://css-tricks.com/centering-css-complete-guide/)就不容易实现。

## W3C提出的一种新的方案
### Flex布局，可以简便、完整、响应式地实现各种页面布局。

<img src="./c01.png">

<!-- more -->

## 浏览器支持
<img class="br10" src="./c101.jpg">


# Flex

Flexible Box的缩写，意为"弹性布局"，
用来为盒状模型提供最大的灵活性。


**任何一个容器都可以指定为Flex布局。**

```css
    .box{
        display: flex;
    }
```

### 「inline-flex」 与 inline-block 

```css
.flex,
    .inline-flex{
        width:100px;
        height:50px;
        border:1px solid #000;
    }
    .flex{
        display:flex;
    }
    .inline-flex{
        display:inline-flex;
    }
```

[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo1.html)


### Webkit内核的浏览器，必须加上`-webkit`前缀。

```css
    .box{
        display: -webkit-flex; /* Safari */
        display: flex;
    }
```

>  注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。


* 采用Flex布局的元素，称为Flex容器，简称"容器"
* 它的所有子元素自动成为容器成员，称为Flex项目，简称"项目"

---

<img class="br10" src="./css09.png">


> flex布局发生在`父容器`和`子容器`之间。父容器需要有flex的环境(display:flex;)，子容器才能根据自身的属性来布局，简单的说，就是瓜分父容器的空间。相反就是说如果父容器没有flex的环境，那么子容器就无法使用flex的规则来划分父容器的空间。


* 水平的主轴main axis和垂直的交叉轴（cross axis）
* 主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end
* 交叉轴的开始位置叫做cross start，结束位置叫做cross end
* 项目默认沿主轴排列
* 单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size

---

## 容器的属性 &#91;**6个**&#93;
---
* <span class="green">flex-direction</span>
* <span class="green">flex-wrap</span>
* <span class="green3">flex-flow</span>
* <span class="blue">justify-content</span>
* <span class="blue">align-items</span>
* <span class="yellow">align-content</span>


## (A1) flex-direction 
### 「容器属性」决定主轴的方向（即项目的排列方向）

```css
    .box {
        flex-direction: row | row-reverse | column | column-reverse;
    }
```

* row（默认值）：主轴为水平方向，起点在左端。
* row-reverse：主轴为水平方向，起点在右端。
* column：主轴为垂直方向，起点在上沿。
* column-reverse：主轴为垂直方向，起点在下沿。

---

<img class="br10" src="./css12.png">

### Flex-direction Demo

---

```css
    .box {
        flex-direction: row | row-reverse | column | column-reverse;
    }
```

[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo2.html)


## (A2) flex-wrap 
###「容器属性」定义如果一条轴线排不下，如何换行 

[默认情况下，项目都排在一条轴线上]

可取**3**个值

```css
    .box{
        flex-wrap: nowrap | wrap | wrap-reverse;
    }
```

<img class="br10" src="./c03.png">

### （1）nowrap（默认）：不换行

---

<img class="br10"  src="./c04.png">

### (2）wrap：换行，第一行在上方

---

<img class="br10"  src="./c05.jpg">

### (3) wrap-reverse：换行，第一行在下方

---

<img class="br10"  src="./c06.jpg">

[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo7.html)  

```css
    .nowrap{
        flex-wrap:nowrap;
    }
    .wrap{
        flex-wrap:wrap;
    }
    .wrap-reverse{
        flex-wrap:wrap-reverse;
    }
```

## (A3) flex-flow 

### 「容器属性」是flex-direction和flex-wrap的简写形式

[默认值为**row** **nowrap**]

```css
    .box{
        flex-flow: flex-direction || flex-wrap;
    }
```

## (A4) justify-content 
### 「容器属性」定义了项目在主轴上的对齐方式

```css
    .box {
        justify-content: flex-start | flex-end | center | space-between | space-around;
    }
```

## 它可能取**5**个值，具体对齐方式与**轴的方向**有关

---

* flex-start（默认值）：左对齐
* flex-end：右对齐
* center： 居中
* space-between：两端对齐，项目之间的间隔都相等
* space-around：每个项目两侧的间隔相等，所以项目之间的间隔比项目与边框的间隔大一倍

## [下面假设主轴**从左到右**]

<img class="br10" src="./c07.png">

[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo3.html)  

```css
    .flex-start{
        justify-content:flex-start;
    }
    .flex-end{
        justify-content:flex-end;
    }
    .center{
        justify-content:center;
    }
    .space-between{
        justify-content:space-between;
    }
    .space-around{
        justify-content:space-around;
    }
```

[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo3.html)

## (A5) align-items 
### 「容器属性」定义项目在交叉轴上如何对齐

```css
    .box {
            align-items: flex-start | flex-end | center | baseline | stretch;
        }
```

## 它可能取**5**个值，具体对齐方式与**交叉轴**有关

---

* flex-start：交叉轴的起点对齐
* flex-end：交叉轴的终点对齐
* center：交叉轴的中点对齐
* baseline: 项目的第一行文字的基线对齐
* stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度

## [下面假设交叉轴**从上到下**]

<img class="br10" src="./c08.png">

```css
    .box {
            align-items: flex-start | flex-end | center | stretch | baseline;
        }
```

[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo4.html)  


## (A6) align-content 
### 「容器属性」定义了多根轴线的对齐方式

---

##### **[如果项目只有一根轴线，该属性不起作用]** 

```css
    .box {
           align-content: flex-start | flex-end | center | space-between | space-around | stretch;
        }
```

## 它可能取**6**个值

* flex-start：与交叉轴的起点对齐
* flex-end：与交叉轴的终点对齐
* center：与交叉轴的中点对齐
* space-between：与交叉轴两端对齐，轴线之间的间隔平均分布
* space-around：每根轴线两侧的间隔都相等,所以轴线之间的间隔比轴线与边框的间隔大一倍
* stretch（默认值）：轴线占满整个交叉轴

### <span class="text-danger">如果项目只有一根轴线，该属性不起作用</span>

---

<img class="br10" src="./c09.png">

```css
    .box {
        align-content: flex-start | flex-end | center | space-between | space-around | stretch;
    }
```

[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo6.html)  

##项目的属性 &#91;**6个**&#93;

---

* <span class="blue">order</span>
* <span class="green2">flex-grow</span>
* <span class="green2">flex-basis</span>
* <span class="green2">flex-shrink</span>
* <span class="text-success">flex</span>
* <span class="yellow">align-self</span>

## (B1) order 
### 「项目属性」定义项目的排列顺序

---
```css
    .item {
            order: 1;
        }
```

### [**数值越小,排列越靠前，默认为0**]

---

<img class="br10" src="./css34.png">

### order Demo

---
[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo8.html)

```css
    .order1{
            order:1;
            background:#c00;
        }
        .order2{
            order:2;
            background:#069;
        }
        .order3{
            order:3;
            background:#095;
        }
```

[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo8.html)


## (B2) flex-grow 

### 「项目属性」定义项目的放大比例

---

#### [**默认为0,即如果存在剩余空间，也不瓜分**]

```css
.   item {
        flex-grow: 0; /* default 0 */
    }
```

### flex-grow Demo
---

<div class="columns-2">
    <p style="font-size: 18px;text-align:left;">如果所有项目的flex-grow属性都为1，<br>则它们将等分剩余空间（如果有的话）</p>
    <p style="font-size: 18px;text-align:left;">如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍</p>
</div>
<pre>
    <code class="css pl10">
    .item {
        flex-grow: 0; /* default 0 */
    }
    </code>
</pre>
---

[demo](https://codepen.io/Frank_/pen/EmEPQm?editors=1100)

[slide]
##(B3) flex-basis 
###「项目属性」定义了在分配多余空间之前，项目占据的主轴空间（main size）

### [**浏览器根据这个属性，计算主轴是否有多余空间**]
---

#### [**它的默认值为auto，即项目的本来大小**]
```css
    .item {
        flex-basis: 1 | auto; /* default auto */
    }
```

### flex-basis Demo
---
#### [**我们通过案例来解释**]
```css
    .item {
        flex-basis: 1 | auto; /* default auto */
    }
```
---
[demo](https://codepen.io/Frank_/pen/VbXjxm?editors=1100)

> 上面讲的<span class="green">flex-grow</span>、<span class="green">flex-basis</span>都是剩余空间的分配。但是，你有没有想过还有没有其他的情况呢？可以发现，上面讲的例子item1 item2 item3的宽度总和都是`没有超过`父容器的宽度的。 那如果三个子容器的`宽度和超过`父容器的宽度呢？那还有剩余空间可以分配吗，此时浏览器又是怎么处理呢？请看下面：

## (B4) flex-shrink 
### 「项目属性」定义了项目的缩小比例，默认为1
---
#### [**即如果空间不足，该项目将缩小**]
```css
    .item {
        flex-shrink: 1; /* default 1 */
    }
```

### flex-shrink Demo
---
#### [**不太好理解 我们通过案例来解释**]
```css
    .item {
        flex-grow: 1; /* default 0 */
    }
```

---
[demo](https://codepen.io/Frank_/pen/LydNrv?editors=1100)


## (B5) flex 
### 「项目属性」简写，默认值为: **0 1 auto**
###  <span class="green">flex-grow</span>,<span class="green">flex-shrink</span> 和 <span class="green">flex-basis</span>
###  [**后两个属性可选**]
---
```css
    .item {
        flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
    }
```

### 该属性有两个快捷值
---
```css
    .item {
        flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
    }
```

* <span class="yellow">auto</span> <span class="green">(1 1 auto)</span>
* <span class="yellow">none</span> <span class="green">(0 0 auto)</span>

### flex Demo
---
#### [**建议优先使用这个属性,因为浏览器会推算相关值**]
```css
    .item {
        flex: <'flex-grow'> <'flex-shrink'> <'flex-basis'>
    }
    .item1{
        flex:1 2 200px;
        background:#c00;
    }
    .item2{
        flex:2 1 100px;
        background:#069;
    }
```

[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo9.html)


## (B6) align-self 
### 「项目属性」允许单个项目有与其他项目不一样的对齐方式
###  [**可覆盖align-items属性**]
---

```html
默认值为 auto, 表示继承父元素的align-items属性

如果没有父元素，则等同于stretch
```
```css
    .item {
        align-self: auto | flex-start | flex-end | center | baseline | stretch;
    }
```

### <span class="text-danger">可取6个值，除了auto，其他都与align-items属性完全一致</span>
```css
    .item {
        align-self: auto | flex-start | flex-end | center | baseline | stretch;
    }
```

[slide]
<img class="br10" src="./css46.png">

### align-self Demo
---
#### [**建议优先使用这个属性,因为浏览器会推算相关值**]
```css
    .item2{
        align-self:baseline;
        line-height: 30px;
        background:#095;
    }
```

[demo](http://www.oxxostudio.tw/demo/201501/css-flexbox-demo5.html)


> 容器的属性 &#91;6个&#93;

* flex-direction
* flex-wrap
* flex-flow
* justify-content
* align-items
* align-content

> 项目的属性 &#91;6个&#93; 

* order
* flex-grow
* flex-basis
* flex-shrink
* flex
* align-self

</br>

#### 参考资料

+ http://www.oxxostudio.tw/articles/201501/css-flexbox.html
+ http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html
+ https://css-tricks.com/snippets/css/a-guide-to-flexbox/
+ https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Using_CSS_flexible_boxes


</br>

> 声明:本资料仅供学习交流，严禁使用于任何商业用途! 相关资料参考自[mdn](https://developer.mozilla.org/en/)等开发者网站或技术大牛[阮一峰](http://www.ruanyifeng.com/blog/)、[oxxo](http://www.oxxostudio.tw/articles/201405/about-me.html)等博客内容。 如需转载，转载请注明出处。

<br/>
### 完.