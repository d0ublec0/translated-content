---
title: 基本的光线投射
slug: Web/API/Canvas_API/A_basic_ray-caster
tags:
  - Canvas
  - 图形
  - 网页
translation_of: Web/API/Canvas_API/A_basic_ray-caster
---
{{CanvasSidebar}}

本篇文章介绍了一个有趣的现实模拟的例子，其模型思想是光线投影 (ray-casting),它使用了{{HTMLElement("canvas")}}元素来进行 3D 渲染

{{EmbedGHLiveSample("canvas-raycaster/index.html", 900, 300)}}

**[在新页面查看演示。](https://mdn.github.io/canvas-raycaster/)**

### 为什么？

在我高兴地发现我已经[了解](https://www.whatwg.org/specs/web-apps/current-work/#dynamic)的漂亮的\<canvas>元素不仅即将支持 Firefox，而且已经支持当前版本的 Safari 后，我尝试着做了这个小实验。

在 MDN 中，我发现 canvas [概述](/zh-CN/docs/Web/API/Canvas_API)和[教程](/zh-CN/docs/Web/API/Canvas_API/Tutorial)是非常完美的，但是还没有人写关于动画的东西，于是我想尝试一个我之前做过的光线投影的动画，看看能从我们期待的 JavaScript 控制像素缓冲区中得到什么样的现象。

### 怎么做？

基本思想是对任意延迟的帧速率使用 {{domxref("window.setInterval","setInterval()")}}。每一个间隔后都会调用一个更新函数来重绘画布显示当前视图。我知道我可以从一个简单的例子开始，但我相信 canvas 教程会有，我想看看我能否做到。

所以，每次更新，射线发射器会检测你最近是否按下任何按键，如果你是闲置状态，会不通过投射来保存计算结果。如果你有按键按下，画布会清空，绘制背景和前景，更新相机的位置或方向，光线被抛弃。当光线与墙壁相交时，他们呈现出一种垂直的帆布条，其颜色和墙壁颜色相匹配，根据离墙壁的距离混合不同深度的颜色。帆布条的高度也会根据相机到墙壁的距离进行调节，并且被绘制在水平线居中位置。

我最后的那段代码是从一本比较老的 Andre 所著的《Windows 游戏编程大师技巧》 (ISBN: 0672305070) 中经过反复合并以及一个 [java raycaster](https://web.archive.org/web/20100511081744/http://www.shinelife.co.uk/java-maze) 网站上得到的，并且对我有用的地方都进行了重命名，这些必要的修改能让它更好的运行。

### 结果

Safari2.0.1 中的画布执行的非常好。使用块效应因子来渲染 8 像素宽的条纹，我可以在我的 Apple mini 中以 24fps 的帧率运行 320\*240 的窗口。Firefox1.5 Beta1 更快；同样帧率和窗口大小的情况下，我可以运行 4 像素宽的。不是 ID 软件系列的一个新成员，它是一个完美的解释型环境，并且我不需要担心内存分配、视频模式或者编码在汇编或者其他内部的例程。代码会通过使用预计算的数组查找来尝试高效的运行，但是我没有做更多优化，所以这可能还会有更快的实现方法。

此外，它在尝试任何类型的游戏引擎方面留下了很多希望 - 没有条纹的墙、没有精灵、没有门，甚至没有任何传送器到达另一层。但是我相信所有那些东西可以慢慢添加。canvas API 支持图像的像素复制，所以添加纹理看起来也是可行的。我会把它们留在另一篇文章里，它可能是由别人写的。(笑

### 光线发射

已经有好心人手动复制我的文件，你可以在[这里](https://mdn.github.io/canvas-raycaster/)看一下，为了满足极客自己动手的想法，我已经放出了独立的源码文件列表（见下文）。

下面这些可能是你想要的，启动 Safari 1.3+或是 Firefox 1.5+或者是其他支持 canvas 的浏览器来体验吧！

[input.js](https://github.com/mdn/canvas-raycaster/blob/master/input.js) | [Level.js](https://github.com/mdn/canvas-raycaster/blob/master/Level.js) | [Player.js](https://github.com/mdn/canvas-raycaster/blob/master/Player.js) | [RayCaster.html](https://github.com/mdn/canvas-raycaster/blob/master/index.html) | [RayCaster.js](https://github.com/mdn/canvas-raycaster/blob/master/RayCaster.js) | [trace.css](https://github.com/mdn/canvas-raycaster/blob/master/trace.css) | [trace.js](https://github.com/mdn/canvas-raycaster/blob/master/trace.js)

### 参见

- [Canvas 教程](/zh-CN/docs/Web/API/Canvas_API/Tutorial)