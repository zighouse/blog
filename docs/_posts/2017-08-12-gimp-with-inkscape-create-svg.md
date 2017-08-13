---
layout: post
title: "用gimp和inkscape把图片转成矢量图"
date: 2017-08-09 23:32:01 +08:00
description: 结合使用gimp的path技巧和inkscape的trace技巧可以从图片创作矢量图。
share: true
tags: 图像处理
---

# 用gimp和inkscape把图片转成矢量图

在 linux 中可以结合使用 gimp 和 inkscape 来实现从一幅图片中创作出一幅矢量图。

一个可行的思路是
 1. 在gimp中将图片进行降噪、滤波、平滑、边缘增强等处理，使得图片的轮廓鲜明，对比强烈。
 2. 调节、压缩色彩的数量，弱化背景突出主题，使图片接近矢量图的线条流畅、色彩明快的特点。
 3. 跟踪、整理轮廓，去掉背景，使之非常接近矢量图。这一步非常关键，常常需要耐心并运用一些技巧进行大量细致的工作。
 4. 在inkscape中跟踪bitmap做成矢量图，可以适当地进行局部调整。

需要用到的 gimp 的关键技巧有 select 和 path ，而需要用到的 inkscape 的关键技巧有 trace bitmap 。下面我通过把之前在手机中拍得的一幅鲜花照片中取出一朵花做成矢量图来简单说明。

使用 gimp 打开照片，从中用矩形选框选中感兴趣的区域，使用 Image > Crop to selection ，然后 File > Export as 保存成另一幅图片，将以此图为基础来制作一幅鲜花的矢量图，真实图片如下：

![svg-demo1]({{ site.baseurl | prepend:site.url}}/images/svg1-s.jpg){: .center-image }*从照片中裁取一朵鲜花*

在 gimp 中全选图片内容，进行一遍 Gaussian Blur、Despeckle、Sharpen。具体地， Filters > Blur > Gaussian blur, Filters > Enhance > Despeckle, Filters > Enhance > Sharpen 。

接下来，使用 Color Levels 调节成色彩分明、主题明确的图像。Colors > Levels ，在弹出来的对话框中调节input levels的区间，可能需要多次类似操作，做成比较满意的效果。

![svg-demo2]({{ site.baseurl | prepend:site.url}}/images/svg2-s.jpg){: .center-image }*图像的预处理后效果*

在 gimp 中使用 select 工具加 brush 工具刷掉多余的内容。当希望擦除无关的复杂内容时，使用颜色拾取器 Color picker 从图中获取适当的颜色，然后使用一个 select 工具选择一片区域，用空气刷在这个区域中把无关内容喷涂覆盖掉。

gimp 中有多个选择工具，在进行选择时配合Ctrl键或Shift键可以实现选区的增加或减少。在 gimp 中使用空气刷等作图工具时，如果在图中选取了一块区域，那么作图的影响范围只局限在选区中。

![svg-demo3]({{ site.baseurl | prepend:site.url}}/images/svg3-s.jpg){: .center-image }*擦除背景突出主题的鲜花效果*

gimp中可以操作图层。导入的照片是没有alpha通道的，可以补充alpha通道，使用alpha通道可以看到下面的图层。

现在我希望把背景处理成空白。增加一个纯白色图层放到主题鲜花的下面。给图像增加 alpha 通道（图层的右键菜单中可以找到 Add alpha Channel）。使用魔棒选择工具选中背景，并删除，会看到白色的背景。使用白色背景有利于看到露删的部分。

在用魔棒选取背景时，可以使用 path 工具描画一遍主题边缘以加强轮廓。把背景选区反选，从而选取了主题。在工具栏中选中 path 工具，在图上任意处点击一下，然后从右击菜单中选择 select > to path，于上就得到了主题轮廓的路径。这时会从工具板上看到 path 的属性，上面有 stroke path 按钮。使用这个按钮以1像素（或者2像素等较少的像素）来描画一遍轮廓路径。对轮廓来一遍描画可以使主题的轮廓更加分明，如果不希望得到这样的适量图效果也可以不用做此操作。

这时就得到了十分接近矢量图效果的图片了，把它按 png 导出，导出前也可以不显示白底图层从而得到透明背景的 png 图片。

![svg-demo4]({{ site.baseurl | prepend:site.url}}/images/svg4-s.jpg){: .center-image }*接近矢量图的图片效果*

使用 inkscape 导入图片，在导入图片的对话框中注意选中 antialias 。

在 inkscape 中全选图片，使用 trace bitmap 工具，得到一个矢量图。 trace bitmap 会有多种参数可以选择，分别得到不同的效果。可以从预览框中看到效果。获得一个矢量图后，选择得到的矢量图，并把它拖开就能看到它底下的原图。可以删除这个底图。删除方法是点击它，然后使用 Ctrl-z 让移动后的矢量图恢复原位，再按下 delete 键。虽然这个底图位于矢量图下方，但仍然是被选中的对象，所以这个 delete 键删除的是选择的底图。

这是按 8 个颜色 trace bitmap 获得的矢量图的效果：
![svg-demo5]({{ site.baseurl | prepend:site.url}}/images/svg-s.png){: .center-image }*8色彩鲜花矢量图效果*

如果在做 trace bitmap 时没有获得原图的色彩，而只抽取了轮廓，那么底下的原图也可以不用删除，这样就能得到原图的色彩了。

可以在 inkscape 中使用原图进行多次不同的 trace bitmap，从而得到不同的内容，这些内容可以叠加在一起形成更接近原图特征的矢量图。

下面是使用两次 trace bitmap 得到的效果，一次是提取轮廓，另一次是提取中心的花蕊，然后删除底图。

![svg-demo6]({{ site.baseurl | prepend:site.url}}/images/svg2-s.png){: .center-image }*鲜花的线条矢量图效果*

