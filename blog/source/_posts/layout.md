---
title: CSS布局
date: 2018-03-23 17:56:05
categories: CSS
tags:
- css 
- layout 
---

了解了盒子模型(box-model)，我们还需要知道这些盒子按照什么规则出现在视口([viewport](https://developer.mozilla.org/en-US/docs/Web/CSS/Viewport_concepts))中。在Overview: CSS中将构建页面比作现实中的搭积木，盒子作为积木，而layout是积木摆放规则。现实中还存在着“重力”，CSS中的书写模式writing-mode这一属性可以进行类比, 默认值writing-mode: horizontal-tb，表示从左到右、从上到下的书写方式，本文即基于此默认值。

#### 正常文档流(normal flow)

正常文档流即是默认情况下(不对元素的CSS另作设置)，元素按照在文档中出现的顺序放置，块级元素垂直组织，而行内元素水平组织。每个块级元素会在上一个元素下面另起一行，它们会被margin分隔，相邻的块级盒子垂直方向上会产生折叠([margin collapsing](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing))；行内元素不会另起一行；只要在其父级块级元素的宽度内有足够的空间，它们与其他行内元素处在同一行。如果空间不够，溢出的文本或元素将移到新的一行。

<!-- more -->
 
#### 浮动(float)

浮动最初被设计出来，是为了在页面中更好的显示图片，实现报纸中文字环绕图片那样的效果。当然浮动也可以被用于其他情况，例如分列展示等。
当给一个元素设置了浮动(如float: left)，则这个元素不影响其父级元素中块级元素的换行、不参与父级元素的高度计算，以其原先在文档中的位置为锚点向左移动。此时元素的显示类型表现为可以设置宽高，参与行内排列，内部产生新的normal flow(BFC)，类似display: inline-block。

#### 定位(position)

除了流式布局，有时相对于参照给出定位更方便布局。
- **static** 是position的默认值，代表元素按照normal flow中计算出的位置布局；
- **relative** 元素以normal flow中计算出的位置为锚点(以下称为初始点)，计算偏移值(top/bottom/left/right)偏移后得到位置，其他元素不受影响，如同此元素仍处于锚点的位置；
- **absolute** 初始点以最近的定位元素为边界，设置偏移值(默认以初始点取得偏移值)，元素被移出normal flow(正常流中其他元素表现如同此元素不存在)；
- **fixed** 初始点以视口为边界(或者最近的transform, perspective, filter属性不为none的祖先元素)，设置偏移值，元素被移出normal flow；
- **sticky** 混合了relative与fixed定位的功能，初始点相对于最近的可滚动祖先元素(overflow不为visible)，设置偏移值，滚动距离小于偏移值时表现为relative定位，达到偏移值时，相对于其父元素fixed。

#### 弹性布局(flex)和网格布局(grid)

很多设计中常见的如水平均分、垂直居中实现起来比较麻烦，经常需要考虑inline/block盒子问题，而float、position也经常影响文档流。设置display: flex;可以进行[弹性布局](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Flexbox);
如果使用网格化设计页面，设置display: grid;可以采用[网格布局](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout)的CSS对应实现；
这两种布局非常强大，可以满足绝大多数页面布局需求，当然也需要掌握更多属性。
