# 维度--事件的属性

## 维度的含义

在GrowingIO系统中，维度是指在分析统计中，用于分解、过滤以及对比指标的角度。

以一个浏览器维度举例：

2018年8月1日，GrowingIO网站首页浏览量为6497次

* 我们可以使用浏览器维度分解这个指标后，看到：
  * Chrome浏览器的浏览量为3543次
  * IE浏览器的浏览量为1321次
* 我们也可以使用浏览器维度做过滤条件，只查看满足 浏览器=Chrome 条件的浏览量为：3543次

## 维度的分类

在事件模型一章中，我们已经介绍过在事件模型中，会包含很多的属性，这些属性就是维度的来源。

GrowingIO将这些维度按照来源的事件类型分为多个类别：

* 访问级维度
* 页面级维度
* 动作级维度
  * 无埋点事件维度
  * 埋点事件维度

## 维度的继承

维度本身具有层级关系，高级别的维度可以用于分解低级别事件定义的指标，举例来说：

`小明 使用 Chrome浏览器 在 2018年8月1日上午11点32分 浏览了 GrowingIO网站首页 点击了一个注册按钮`

在上述的用户行为中，我们可以发现多个层级的维度：

* 访问级维度：浏览器=Chrome
* 页面级维度：域名=www.growingio.com  页面=/
* 动作级维度：元素内容=注册

对于`注册按钮点击量`这个指标，可以被三个维度进行分解、过滤。

对于`GrowingIO网站首页浏览量`这个指标，只能被访问级维度、页面级维度分解、过滤

