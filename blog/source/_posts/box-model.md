---
title: 盒模型
date: 2018-03-16 00:20:27
categories: CSS
tags:
- css 
- box-model 
---

在 CSS 中，**所有的元素** 都被一个个的“盒子（box）”包围着，div、span这些元素都会生成至少一个盒子。理解这些“盒子”的基本原理，是我们使用CSS实现准确布局、处理元素排列的关键。


盒子的 **内部** 和 **外部** 的显示类型：

- 内部：控制盒子内部元素的布局(layout)，通常是正常文档流(normal flow)；也可以是table、flex、grid等特殊layout形式；

- 外部：控制盒子本身在外部layout中应该如何定位，normal flow中通常分为块级盒子(block-level box)和行内级盒子(inline-level box)。

内外显示类型通常由盒子的[display](https://drafts.csswg.org/css-display/#the-display-properties)属性决定。处于特殊layout中的盒子，如table、flex等格式化上下文(formatting contexts)中，按照相应的规则布局；也可以通过调整position、float属性影响盒子的内外显示类型。


> the inner display type, which defines (if it is a non-replaced element) the kind of formatting context it generates, dictating how its descendant boxes are laid out. (The inner display of a replaced element is outside the scope of CSS.)
the outer display type, which dictates how the [principal box](https://developer.mozilla.org/en-US/docs/Web/CSS/Visual_formatting_model#Box_generation) itself participates in flow layout.

<!-- more -->

**在normal flow中**
- 块级盒子会*占据*父元素水平方向的全部宽度（不论实际宽度如何），使得上下的其他盒子发生换行，块级盒子可以被指定宽高，外边距(margin)会增加实际占位范围，相邻的块级盒子垂直方向上会产生折叠(margin collapsing)；

- 行内级盒子通常出现在块级盒子中，会根据实际内容决定自身宽高，垂直方向的变化（设置边距、边界）无法影响其他盒子的布局。

对于脱离正常文档流的盒子，或是处于特殊formatting contexts中的盒子，通常称可以指定宽高的盒子为“块级盒子”，不能则称为“行内级盒子”，此时它们的具体宽高、位置的计算**不完全等同**于normal flow中的块、行内级盒子。

### 匿名盒子
本文开头提到，**所有的元素**均被盒子所包裹，那些看似没被标签包围的内容通常会根据所在格式化上下文生成匿名盒子(anonymous box)。
``` html
<div class="example-1">
    I am wrapped in an anonymous box 
    <p>I am in the paragraph</p>
    I am wrapped in an anonymous box.
</div>
<!-- p元素上下生成两个匿名块级盒子  -->

<div class="example-2">
    I am wrapped in an anonymous box 
    <span>I am in the inline-box</span>
    I am wrapped in an anonymous box.
</div>
<!-- span元素前后生成两个匿名行内级盒子  -->
```
块包含盒子只包含行内级盒子，或者只包含块级盒子。同时存在块级和行内级时，会生成匿名的块级盒子来包裹行内级盒子
匿名盒子无法被CSS选择器选中，只能继承父元素的可继承样式。

一个常见问题：
``` html
<div class="example-3">
    <span>I am in the inline-box</span> <span>I am in the inline-box</span>
    <span>I am in the inline-box</span>
</div>
```
若干inline-box在一行时，它们之间会出现空隙。这是由于我们在写html文档时，通常每个span标签前后是有换行符（或是空格）的，而这些空内容也生成了匿名inline-box，虽然内容为空，但仍然占用了一定宽度，因此出现空隙。<br/>
我们无法选中这些匿名盒子进行操作，但是因为它们会继承父元素样式，可以设置.example-3字体大小为0，再设置span为原先的字体大小。这是基于匿名盒子机制的处理办法。