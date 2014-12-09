##7.1介绍

对于所有的媒体，`SVG canvas`定义了“一块SVG内容渲染区域。”canvas在空间的每个维度上都是无穷，但是渲染发生在canvas中有限的矩形内。这个有限的矩形区域叫做`SVG viewport`。对于[visual media](http://www.w3.org/TR/2008/REC-CSS2-20080411/media.html#visual-media-group)SVG viewport是一个用户可以看到SVG内容的可视区域。

SVG viewport的尺寸（即，它的宽和高）由SVG文档片段和它的父元素(real or implicit)之间权衡决定。一旦谈判过程结束，SVG用户代理提供如下信息：

* 一个代表viewport宽度的数（通常为整数）单位为"像素"。
* 一个代表viewport高度的数（通常为整数）单位为"像素"。
* （推荐但不是必须）一个真实的数值指明一个“像素”在真实世界单位中的尺寸，比如毫米。（即，一个px单元[在CSS2中定义](http://www.w3.org/TR/2008/REC-CSS2-20080411/syndata.html#length-units)）

使用上述信息，SVG用户代理决定`viewport`，初始`viewport坐标系`和初始`用户坐标系`，两个坐标系是相同的。两个坐标系的原点都和viewport的原点匹配（对于根viewport，viewport原点在左上角），初始坐标系中的一个单元等于viewport中的一个“像素”。（查看[初始坐标系](http://www.w3.org/TR/SVG/coords.html#InitialCoordinateSystem)）。viewport坐标系也叫做`viewport space`同时用户坐标系也叫`user space`。

SVG中的长度可以声明为：
*（如果没有提供单位符号）用户空间中的值-例如，“15”
* (如果提供了单位符号)长度表示绝对或相对单位量度-例如，“15mm”或“5em”

支持的长度单位符号有：em, ex, px, pt, pc, cm, mm, in, 和百分数。

新用户空间（即，新当前坐标系）可以通过`transformation matrices`或简单的变换操作例如旋转，倾斜，拉伸和移动的形式申明`transformations`在SVG文档片段的任何地方建立。通过[坐标系变换](http://www.w3.org/TR/SVG/coords.html#EstablishingANewUserSpace)建立新用户坐标系是2D图形基本操作代表常用的控制图形对象尺寸，位置，旋转和拉伸的方法。

也可以建立新viewport。通过[建立新的视口](http://www.w3.org/TR/SVG/coords.html#EstablishingANewViewport)，你可以重定义百分比单位的意义并且提供一个新的参考矩形来把一个图形“适应”到一个特定矩形区域。（“适应”代表给定的图形通过特定变换使得它在用户空间里的边界框完全对齐给定viewport的边界。）

##初始viewport

SVG用户代理和父级用户代理协商来决定在哪个视口中SVG用户代理可以渲染文档。在一些情况中，SVG内容