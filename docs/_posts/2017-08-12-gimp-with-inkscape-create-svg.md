---
layout: post
title: "用gimp和inkscape把图片转成矢量图"
date: 2017-08-09 23:32:01 +08:00
description: 结合使用gimp的path技巧和inkscape的trace技巧可以从图片创作矢量图。
share: true
tags: gimp inkscape 图像处理
---

# 用gimp和inkscape把图片转成矢量图

在 linux 中可以结合使用 gimp 和 inkscape 来实现
从一幅图片中创作出一幅矢量图。

基本思路是
 * 先将图片进行降噪、滤波、平滑、边缘增强等处理，使得
 * 希望提取矢量图的关键部位尽量变得简洁明快，以接近矢量图的特征。
 * 然后把图片按色彩进行分割，使得只需要几种色彩或者几个灰度级来表现图片。
 * 接下来开始细致地整理边缘和轮廓，使得内容的线条特征突出。
 * 最后做成矢量图，并进行局部调整。

需要用到的 gimp 的关键技巧有 select 和 path ，
而需要用到的 inkscape 的关键技巧有 trace bitmap 。

1. 从图片中裁出感兴趣的区域。

![svg-demo1]({{ site.baseurl | prepend:site.url}}/images/svg1-s.jpg){: .center-image }*iPad mini landscape*

2. 经 Gaussian Blur、Despeckle、Sharpen后，使用 Color Levels 调节成色彩分明、主题明确的图像。

![svg-demo2]({{ site.baseurl | prepend:site.url}}/images/svg2-s.jpg){: .center-image }*iPad mini landscape*

3. 使用 select 工具加 brush 工具刷掉多余的内容。

![svg-demo3]({{ site.baseurl | prepend:site.url}}/images/svg3-s.jpg){: .center-image }*iPad mini landscape*

4. 增加一个纯白色图层放到最底下；
5. 给图像增加 alpha 通道，使用魔棒及 select 工具把背景选中，删除，
6. 同时为选中区域的边缘创建一个path，即选中 path 工具，在图上任意处点击一下，然后右击菜单中选择 select > to path
7. 使用 path 工具的 stroke 功能补充描画一下这个 path。如果图像的轮廓分明，这个具有技巧性的一步也可以不用做。

![svg-demo4]({{ site.baseurl | prepend:site.url}}/images/svg4-s.jpg){: .center-image }*iPad mini landscape*

8. 导出图片。
9. 使用 inkscape 导入图片。
10. 全选图片，使用 trace bitmap 工具，得到一个矢量图。
11. 选择得到的矢量图，并把它拖开就能看到它底下的原图，这时选中这个原图。
12. 使用 Ctrl-z 使得被拖开的矢量图回到原位置，然后按下 delete 键，删除原图，于是只剩下了矢量图。

![svg-demo5]({{ site.baseurl | prepend:site.url}}/images/svg-s.png){: .center-image }*iPad mini landscape*

如果没有获得原图的色彩，而只抽取了轮廓，那么底下的原图也可以不用删除，这样就能得到原图的色彩了。

可以在 inkscape 中使用原图进行多次不同的 trace bitmap，从而得到不同的内容，这些内容可以叠加在一起形成更接近原图特征的矢量图。

![svg-demo6]({{ site.baseurl | prepend:site.url}}/images/svg2-s.png){: .center-image }*iPad mini landscape*

