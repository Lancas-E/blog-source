---
title: 可视化排版模型
date: 2020-03-26 17:00:28
categories: CSS
---

可视化排版模型([Visual formatting model](https://www.w3.org/TR/CSS2/visuren.html))，描述浏览器(常见的可视化媒体)处理文档树([document tree](https://www.w3.org/TR/CSS2/conform.html#doctree))的过程。CSS盒模型与布局都是服务于可视化排版模型的，之前已经介绍过了，本文主要补充一些展示区域的相关问题。

formatting的翻译问题: 通常会翻译为“格式化”，但是CSS中主要表示：如何将内容展示、排布在画布([canvas](https://www.w3.org/TR/CSS2/intro.html#the-canvas))上，采用“排版”更加直观。

在[CSS布局](/blog/layout)中，盒子的主要排布规则是normal flow，更具体的讲，normal flow中的盒子还处于相应的formatting context(排版区域)中，有Block/Inline formatting contexts(BFC/IFC)。这主要是为了解决盒子在流中的一些边界问题，例如BFC主要控制块级区域中margin、浮动的界限；IFC主要控制行内元素的展示、行盒的显示规则。

<!-- more -->

#### Block formatting contexts
创建BFC有如下方法：
- root元素(\<html>)
- float
- 绝对定位(position:absolute/fixed)
- display: inline-block/table-cell/flex/grid/flow-root...
- overflow 不为visible

需要将浮动元素包裹(浮动元素默认会脱离文档流)，需要对内部的margin设定边界(相邻的子元素margin会垂直叠加，导致溢出包含块)时，或者内部有其特殊的布局(table/flex/grid)，总之需要一块相对独立的区域时，BFC给其内部的子元素设定了边界，将它们包裹起来，避免一些副作用溢出此区域。
比较好的、无副作用的创建方法是display: flow-root，也具有说明性，表示此包含块为“文档流的根”，即那些可能乱跑的float、margin的边界。


#### Inline formatting contexts
只包含行内级盒子(inline-level boxes)的块包含盒子(block container box)，会创建IFC。例如：
``` html
<p>
    Several <EM>emphasized words</EM> appear<STRONG>in this</STRONG> sentence, dear.
</p>
```
子元素生成一个个行内盒(inline box)，从左到右从上到下，依次排布，IFC中每一行被称为一个line box。
line box的宽度由包含块的宽度和同一行的float元素来决定，其高度是此行内最高的元素的顶端到最低元素的底端。当一行内所有行内盒宽度之和小于line box的宽度时，它们水平方向的排布受到text-align的控制；当某个行内盒的高度小于line box的高度时，它在垂直方向的排布受到vertical-align的控制。(垂直布局有时效果不尽如人意，这与inline box的高度、line box的高度以及它们的对齐方式有关，[这篇文章](http://iamvdo.me/en/blog/css-font-metrics-line-height-and-vertical-align)论述的非常好。)