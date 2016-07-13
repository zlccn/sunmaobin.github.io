---

title: HTML解惑-浏览器渲染流程
date: 20160701031143
categories: [WEB]
tags: [html]

---

浏览器如何展示页面的？

## 一、浏览器工作流程

### 1、加载

根据请求的URL进行域名解析，向服务器发起请求，接收文件（HTML、JS、CSS、图象等）。

### 2、解析

对加载到的资源（HTML、JS、CSS等）进行语法解析，建立相应的内部数据结构（比如HTML的DOM树，JS的（对象）属性表，CSS的样式规则等等）

### 3、渲染

构建渲染树，对各个元素进行位置计算、样式计算等等，然后根据渲染树对页面进行渲染（可以理解为“画”元素）

> 这几个过程不是完全孤立的，会有交叉，比如HTML加载后就会进行解析，然后拉取HTML中指定的CSS、JS等。


其中，仅针对浏览器拿到资源后的渲染这一部分，可以包含两部分流程。

## 二、渲染流程

### 1、排版

根据文档流，加上浮动、定位等属性，确定各个盒子的位置还有尺寸。

### 2、绘制

将css的属性例如字体、背景色、圆角等等按照给定的方式呈现出来。


**注意：**这里涉及到2个性能优化的概念：

1. Repaint：重绘
1. Reflow：重新渲染

## 三、性能优化之Repaint和Reflow

### 1、Repaint

对页面进行重绘，这时候不会更改页面布局，性能变化没那么明显。

比如：修改 `font-color`、`text-align` 等修改

### 2、Reflow

对页面进行重新渲染，这个是要包含 `Repaint`。也就是页面布局不仅要重新调整，样式也要重新调整。

对于引发这种重新渲染的情况，主要有：

* 新增/删除HTML节点、修改容器尺寸等
* 查询一些尺寸，如：`clientHeight`、`clientWidth`等，因为计算尺寸的时候要重新渲染一次才能得到结果，这是浏览器的计算原理。

## 四、参考

* [http://www.zhihu.com/question/20117417](http://www.zhihu.com/question/20117417)
* [http://harttle.com/2015/08/11/reflow-repaint.html](http://harttle.com/2015/08/11/reflow-repaint.html) 