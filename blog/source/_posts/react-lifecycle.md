---
title: React组件生命周期
date: 2019-04-08 15:16:39
tags:
- react
---
React v16.3之前的生命周期函数如下：
{% asset_img react-lifecycle-before-16.png lifecyccle1 %}
React v16.3引入了两个新的生命周期函数：
- getDerivedStateFromProps
- getSnapshotBeforeUpdate
{% asset_img react-lifecycle-after-16.3.png lifecyccle1 %}
<!-- more -->
(在React v16.4中，getDerivedStateFromProps可以被setState和forceUpdate所触发)

render之前的生命周期在React采用[Fiber架构](https://zhuanlan.zhihu.com/p/26027085)之后，调用次数变得不可控，在React v16.3中被加以UNSAFE_前缀。并且很多时候我们对组件的控制并不需要达到如此细的颗粒度。相反由于给了太多选择，开发者也有了更多实现方式和更多犯错可能。