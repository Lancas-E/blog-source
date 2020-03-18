---
title: 盒模型
date: 2020-03-16 00:20:27
categories: CSS
tags:
- css 
- box-model 
---

在 CSS 中，**所有的元素** 都被一个个的“盒子（box）”包围着，理解这些“盒子”的基本原理，是我们使用CSS实现准确布局、处理元素排列的关键。


盒子决定着 **内部** 和 **外部** 的显示类型：

- 内部：控制盒子内部元素的布局(layout)，通常是正常文档流(normal flow)；也可以是table、flex、grid等特殊layout形式

- 外部：控制盒子在外部layout中应该如何定位，通常一个flow中有块级盒子(block-level box)和行内级盒子(inline-level box)；也可以通过一些方法，创建格式化上下文(formatting contexts)，从而影响其与浮动(float)元素的位置

内外显示类型通常由盒子的[display](https://drafts.csswg.org/css-display/#the-display-properties)属性决定


> the inner display type, which defines (if it is a non-replaced element) the kind of formatting context it generates, dictating how its descendant boxes are laid out. (The inner display of a replaced element is outside the scope of CSS.)
the outer display type, which dictates how the principal box itself participates in flow layout.

**在normal flow中**
- 块级盒子会*占据*父元素水平方向的全部宽度（不论实际宽度如何），使得上下的其他盒子发生换行，块级盒子可以被指定宽高，外边距(margin)会增加实际占位范围，并在垂直方向上产生折叠(margin collapsing)

- 行内级盒子会根据实际内容决定自身宽高，垂直方向的变化（设置边距、边界）无法影响其他盒子的布局

{% img box-model /box-model/box-model.png 基础盒模型 %}

标准盒模型中，宽高为Content的宽高，通过设置```box-sizing: border-box;```表示相对边界之间的距离

### 匿名盒子
本文开头提到，所有