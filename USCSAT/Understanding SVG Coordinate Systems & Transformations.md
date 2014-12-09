#Understanding SVG Coordinate Systems & Transformations (Part 1) – The viewport, viewBox, & preserveAspectRatio
#理解SVG坐标系和变换（第一部分）-视口,`viewbox`和`preserveAspectRatio`

SVG elements aren't governed by a CSS box model like HTML elements are. This makes positioning and transforming these elements trickier and may seem—at first glance—less intuitive. However, once you understand how SVG coordinate systems and transformations work, manipulating SVGs becomes a lot easier and makes a lot more sense. In this article we're going to go over three of the most important SVG attributes that control SVG coordinate systems: `viewport`, `viewBox`, and `preserveAspectRatio`.

SVG元素不像HTML元素一样由CSS盒模型管理。这使得我们可以更加灵活定位和变换这些元素-也许一眼看上去不太直观。然而，一旦你理解了SVG坐标系和变换，操纵SVG会非常简单并且很有意义。本篇文章中我们将讨论控制SVG坐标系的最重要的三个属性：`viewport`， `viewBox`， 和 `preserveAspectRatio`。

This is the first in a series of three articles covering the topic of coordinate systems and transformations in SVG.

这是本系列三篇文章中的第一篇，这篇文章讨论SVG中的坐标系和变换。

* Understanding SVG Coordinate Systems & Transformations (Part 1) – The viewport, `viewBox`, & `preserveAspectRatio`
* [Understanding SVG Coordinate Systems & Transformations (Part 2) – The `transform` Attribute](http://sarasoueidan.com/blog/svg-transformations)
* [Understanding SVG Coordinate Systems & Transformations (Part 3) – Establishing New Viewports](http://sarasoueidan.com/blog/nesting-svgs)

* 理解SVG坐标系和变换（第一部分）-viewport，`viewBox`，和`preserveAspectRatio`
* [理解SVG坐标系和变换（第二部分）-`transform`属性](http://sarasoueidan.com/blog/svg-transformations)
* [理解SVG坐标系和变换（第三部分）-建立新视口](http://sarasoueidan.com/blog/nesting-svgs)

For the sake of visualizing the concepts and explanations in the article even further, I created an interactive demo that allows you to play with the values of the `viewBox` and `preserveAspectRatio` attributes.

为了使文中的内容和解释更形象化，我创建了一个互动演示，你可以任意改变`viewBox` 和 `preserveAspectRatio`的值。

<a class="button" href="/demos/interactive-svg-coordinate-system/index.html">Check the interactive demo out.</a>

<a class="button" href="/demos/interactive-svg-coordinate-system/index.html">查看互动演示</a>

*The demo is the cherry on top of the cake, so do make sure you come back to read the article if you check it out before you do!*

*这个例子只是主要内容的一小部分，所以看完请回来继续阅读这篇文章*

##The SVG Canvas
##SVG画布

The **canvas** is the space or area where the SVG content is drawn. Conceptually, this canvas is infinite in both dimensions. The SVG can therefore be of any size. However, it is rendered on the screen relative to a **finite region** known as the viewport. Areas of the SVG that lie beyond the boundaries of the viewport are clipped off and not visible.

**canvas**是绘制SVG内容的一块空间或区域。理论上，画布在所有维度上都是无限的。所以SVG可以是任意尺寸。然而，SVG通过**有限区域**展现在屏幕上，这个区域叫做`viewport`。SVG中超出视口边界的区域会被裁切并且隐藏。

##The Viewport
##视口

The viewport is the viewing area where the SVG will be visible. You can think of the viewport as a window through which you can see a particular scene. The scene may be entirely or partially visible through that window.

视口是一块SVG可见的区域。你可以把视口当做一个窗户，透过这个窗户可以看到特定的景象，景象也许完整，也许只有一部分。

The SVG viewport is similar to the viewport of the browser you're viewing this page through. A web page can be of any size; it can be wider than the viewport's width, and is in most cases also longer than the viewport's length. However, only portions of a web page are visible through the viewport at a time.

SVG的视口类似访问当前页面的浏览器视口。网页可以是任何尺寸；它可以大于视口宽度，并且在大多数情况下都比视口高度要高。然而，每个时刻只有一部分网页内容是透过视口可见的。

*Whether or not the entire SVG canvas or part of it is visible depends on the *size of that canvas\** and *the value of the `preserveAspectRatio`attribute*. You don't have to worry about these now; we'll talk about them further in more detail.*

*整个SVG画布可见还是部分可见取决于这个*canvas\*的尺寸*以及*`preserveAspectRatio`属性值*。你现在不需要担心这些；我们之后会讨论更多的细节。*

You specify the size of the viewport using the `width` and `height `attributes on the outermost `<svg>` element.

你可以在最外层`<svg>`元素上使用`width`和`height`属性声明视口尺寸。

	<!-- the viewport will be 800px by 600px -->
	<svg width="800" height="600">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

In SVG, values can be set with or without a unit identifier. A unitless value is said to be specified in user space using user units. If a value is specified in user units, then the value is assumed to be equivalent to the same number of "px" units. This means that the viewport in the above example will be rendered as a 800px by 600px viewport.

在SVG中，值可以带单位也不可以不带。一个不带单位的值可以在用户空间中通过用户单位声明。如果值通过用户单位声明，那么这个值的数值被认为和"px"单位的数值一样。这意味着上述例子将被渲染为800px*600px的视口。

You can also specify values using units. The supported length unit identifiers in SVG are: `em`, `ex`, `px`, `pt`, `pc`, `cm`, `mm`, `in`, and percentages.

你也可以使用单位来声明值。SVG支持的长度单位有：`em`，`ex`，`px`，`pt`，`pc`，`cm`，`mm`，`in`和百分比。

Once the width and height of the outermost SVG element are set, the browser establishes an initial viewport coordinate system and an initial user coordinate system.

一旦你设定最外层SVG元素的宽高，浏览器会建立初始视口坐标系和初始用户坐标系。

###The initial coordinate system
###初始坐标系

The initial **viewport coordinate system** is a coordinate system established on the viewport, with the origin at the top left corner of the viewport at point (0, 0), the positive x-axis pointing towards the right, the positive y-axis pointing down, and one unit in the initial coordinate system equals one "pixel" in the viewport. This coordinate system is similar to the coordinate system established on an HTML element with a CSS box model.

初始**视口坐标系**是一个建立在视口上的坐标系。原点(0,0)在视口的左上角，X轴正向指向右，y轴正向指向下，初始坐标系中的一个单位等于视口中的一个"像素"。这个坐标系统类似于通过CSS盒模型在HTML元素上建立的坐标系。

The initial **user coordinate system** is the coordinate system established on the SVG canvas. This coordinate system is initially identical to the viewport coordinate system—it has its origin at the top left corner of the viewport with the positive x-axis pointing towards the right, the positive y-axis pointing down. Using the `viewBox` attribute, the initial user coordinate system—also known as **the current coordinate system**, or **user space in use**—can be modified so that it is not identical to the viewport coordinate system anymore. We'll talk about modifying it in the next section.

初始**用户坐标系**是建立在SVG画布上的坐标系。这个坐标系一开始和视口坐标系完全一样-它自己的原点位于视口左上角，x轴正向指向右，y轴正向指向下。使用`viewBox`属性，初始用户坐标系统-也称**当前坐标系**，或**使用中的用户空间**-可以变成与视口坐标系不一样的坐标系。我们在一下节中讨论如何改变坐标系。

For now, we won't specify a `viewBox` attribute value. The user coordinate system of the SVG canvas is identical to that of the viewport.

到现在为止，我们还没有声明`viewBox`属性值。SVG画布的用户坐标系统和视口坐标系统完全一样。

In the following image, the viewport coordinate system "ruler" is grey, and that of the user coordinate system (the `viewBox`) is blue. Since they are both identical at this point, the two coordinate systems overlap.

下图中，视口坐标系的"标尺"是灰色的，用户坐标系（`viewBox`）的是蓝色的。由于它们在这个时候完全相同，所以两个坐标系统重合了。

![](svg/initial-coordinate-systems.jpg)

The parrot in the above SVG has a bounding box that is 200 units (200 pixels in this case) in width and 300 units in height. The parrot is drawn on the canvas based on the initial coordinate system.

上面SVG中的鹦鹉的外框边界是200个单位（这个例子中是200个像素）宽和300个单位高。鹦鹉基于初始坐标系在画布中绘制。

*A new user space (i.e., a new current coordinate system) can also be established by specifying **transformations** using the `transform` attribute on a container element or graphics element. We'll talk about transformations in the second part of this article, and then in more details in the third and last part.*

*新用户空间（即，新当前坐标系）也可以通过在容器元素或图形元素上使用`transform `属性来声明**变换**。我们将在这篇文章的第二部分讨论关于变换的内容，更多细节在第三部分和最后部分中讨论。*

##`viewBox`

I like to think of the `viewBox` as the "real" coordinate system. After all, it is the coordinate system used to draw the SVG graphics onto the canvas. This coordinate system can be smaller or bigger than the viewport, and it can be fully or partially visible inside the viewport too.

我喜欢把`viewBox`理解为“真实”坐标系。首先，它是用来把SVG图形绘制到画布上的坐标系。这个坐标系可以大于视口也可以小于视口，在视口中可以整体可见或部分可见。

In the previous section, this coordinate system—the user coordinate system—was identical to the viewport coordinate system. The reason for that is that we did not specify it to be otherwise. That's why all the positioning and drawing seemed to be done relative to the viewport coordinate system. Because once we created a viewport coordinate system (using `width` and `height`), the browser created a default user coordinate system that is identical to it.

在之前的章节里，这个坐标系-用户坐标系-和视口坐标系完全一样。因为我们没有把它声明成其他坐标系。这就是为什么所有的定位和绘制看起来是基于视口坐标系的。因为我们一旦创建视口坐标系（使用`width`和`height`），浏览器默认创建一个完全相同的用户坐标系。

You specify your own user coordinate system using the `viewBox` attribute. If the user coordinate system you choose has the same aspect ratio (ratio of height to width) as the viewport coordinate system, it will stretch to fill the viewport area (we'll talk examples in a minute). However, if your user coordinate system does not have the same aspect ratio, you can use the `preserveAspectRatio`attribute to specify whether or not the entire system will be visible inside the viewport or not, and you can also use it to specify how it is positioned inside the viewport. We'll get into details and lots of examples for this case in the next section. In this section, we'll stick to examples where the aspect ratio of the `viewBox` matches that of the viewport—in these examples, `preserveAspectRatio` has no effect.

你可以使用`viewBox`属性声明自己的用户坐标系。如果你选择的用户坐标系统和视口坐标系统宽高比（高比宽）相同，它会延伸来适应整个视口区域（一分钟内我们就来讲个例子）。然而，如果你的用户坐标系宽高比不同，你可以用`preserveAspectRatio`属性来声明整个系统在视口内是否可见，你也可以用它来声明在视口中如何定位。我们会在下个章节里讨论这一情况的细节和例子。在这一章里，我们只讨论`viewBox`的宽高比符合视口的情况-在这些例子中，`preserveAspectRatio`不产生影响。

Before we get into the examples, we'll go over the syntax of `viewBox`.

在我们讨论这些例子前，我们回顾一下`viewBox`的语法。

###The `viewBox` syntax
###`viewBox`语法

The `viewBox attribute` takes four parameters as a value: `<min-x>, <min-y>, width` and `height`.

`viewBox`属性接收四个参数值，包括：`<min-x>, <min-y>, width` 和 `height`。

	viewBox = <min-x> <min-y> <width> <height>

The` <min-x>` and `<min-y>` values determine the upper left corner of the viewbox, and the `width` and `height` determine the width and height of that viewport. Note here that the width and height of the viewport need not be the same as the width and height set on the parent `<svg>` element. A negative value for `<width>` or `<height>` is invalid. A value of zero disables rendering of the element.

`<min-x>` 和 `<min-y>` 值决定viewbox的左上角，`width`和`height`决定视口的宽高。这里要注意视口的宽高不一定和父`<svg>`元素的宽高一样。`<width>`和`<height>`值为负数是不合法的。值为0的话会禁止元素的渲染。

*Note that the width of the viewport can also be set in CSS to any value. For example, setting `width: 100%` will make the SVG viewport fluid in a document. Whatever value of the `viewBox`, it will then be mapped to the computed width of the outer SVG element.*

*注意视口的宽度也可以在CSS中设置为任何值。例如：设置`width:100%`会让SVG视口在文档中自适应。无论`viewBox`的值是多少，它会映射为外层SVG元素计算出的宽度值。*

An example of setting `viewBox` would look like the following:

设置`viewBox`的例子如下：

	<!-- The viewbox in this example is equal to the viewport, but it can be different -->
	<svg width="800" height="600" viewbox="0 0 800 600">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

If you've read about the `viewBox` somewhere before, you may have come across a few definitions saying that you can use the `viewBox` attribute to transform the SVG graphic by scaling or translating it. This is true. I'm going to go further and say that you can even crop the SVG graphic using `viewBox`.

如果你之前在其他地方看到过`viewBox`，你也许会看到一些解释说你可以用`viewBox`属性通过缩放或者变化使SVG图形变换。这是真的。我将深入探究并且告诉你甚至可以使用`viewBox`来切割SVG图形。

The best way to understand the `viewBox` and differentiate it from the viewport is by visualizing it. So let's start with some examples. We'll start with examples where th aspect ratio of the viewbox is the same as the aspect ratio of the viewport, so we won't need to dig into `preserveAspectRatio` yet.

理解`viewBox`和视口之间差异最好的方法是亲身观察。所以让我们看一些例子。我们将从viewbox和viewport的宽高比相同的例子开始，所以我们还不需要深入了解`preserveAspectRatio`。

###`viewBox` with aspect ratio equal to the viewport's aspect ratio
###与viewport宽高比相同的`viewBox`

We'll start with a simple example. The `viewbox` in this example will be half the size of the viewport. We won't change the origin of the viewbox in this one, so both `<min-x>` and `<min-y>` will be set to zero. The width and height of the viewbox will be half the width and height of the viewport. This means that we're preserving the aspect ratio.

我们从一个简单的例子开始。这个例子中的`viewbox`的尺寸是视口尺寸的一半。在这个例子中我们不改变viewbox的原点，所以`<min-x>`和`<min-y>`都设置成0。viewbox的宽高是viewport宽高的一半。这意味着我们保持宽高比。

	<svg width="800" height="600" viewbox="0 0 400 300">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

So, what does `viewbox="0 0 400 300"` exactly do?
所以，`viewbox="0 0 400 300"`到底有什么用呢？

* It specifies a specific region of the canvas spanning from a top left point at (0, 0) to a point at (400, 300).
* The SVG graphic is then **cropped** to that region.
* The region is **scaled up** (in a zoom-in-like effect) to fill the entire viewport.
* The user coordinate system is mapped to the viewport coordinate system so that—in this case—one user unit is equal to two viewport units.

* 它声明了一个特定的区域，canvas横跨左上角的点(0,0)到点(400,300)。
* SVG图像被这个区域**裁切**。
* 区域被**拉伸**（类似缩放效果）来充满整个视口。
* 用户坐标系被映射到视口坐标系-在这种情况下-一个用户单位等于两个视口单位。

The following image shows the result of applying the above viewbox to the `<svg>` canvas in our example. The grey units represent the viewport coordinate system, and the blue coordinate system represents the user coordinate system established by the `viewBox`.

下面的图片展示了在我们例子中把上面的viewbox应用到`<svg>` 画布中的效果。灰色单位代表视口坐标系，蓝色坐标系代表`viewbox`建立的用户坐标系。

![](svg/viewbox-400-300-crop.jpg)

Anything you draw on th SVG canvas will be drawn relative to the new user coordinate system.

任何在SVG画布中画的内容都会被对应到新的用户坐标系中。

*I like to visualize the SVG canvas with a `viewBox` the same way as Google maps. You can zoom in to a specific region or area in Google maps; that area will be the only area visible, scaled up, inside the viewport of the browser. However, you know that the rest of the map is still there, but it's not visible because it extends beyond the boundaries of the viewport—it's being clipped out.*

*我喜欢像Google地图一样通过`viewBox`把SVG画布形象化。在Google地图中你可以在特定区域缩放；这个区域是唯一可见的，并且在浏览器视口中按比例增加。然而，你知道地图的剩余部分还在那里，但是不可见因为它超出视口的边界-被裁切了。*

Now let's try changing the `<min-x>` and `<min-y>` values. We'll set both to `100`. They can be any number you want. The width and height ratio will also be the same as width and height ratio of the viewport.

现在让我们试着改变`<min-x>`和`<min-y>`的值。都设置为`100`。你可以设置成任何你想要的值。宽高比还是和视口的宽高比一样。


	<svg width="800" height="600" viewbox="100 100 200 150">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

The effect of applying `viewBox="100 100 200 150"` is also a crop effect like the one in the previous example. The graphic is cropped and scaled up to fill the entire viewport area.

添加`viewBox="100 100 200 150"`的效果和之前例子中一样都是裁切的效果。图形被裁切然后拉伸来充满整个视口区域。

![](svg/viewbox-200-150-crop.jpg)

Again, the user coordinate system is mapped to the viewport coordinate system—200 user units are mapped to 800 viewport units so that every user unit is equal to four viewport units. This results in a zoom-in effect like the one you can see in the above screenshot.

再一次，用户坐标系被映射到视口坐标系-200用户单位映射为800视口单位因此每个用户单位等于四个视口单位。结果像你看到的那样是放大的效果。

Also note, at this point, that specifying non-zero values for the `<min-x>` and `<min-y>` values has a transformation effect on the graphic; more specifically, it is as though the SVG canvas was translated by 100 units to the top and 100 units to the left (`transform="translate(-100 -100)"`).

另外注意，在这个时候，为`<min-x>`和`<min-y>`声明非0的值对图形有变换的效果；更加特别的是，SVG 画布看起来向上拉伸100个单位，向左拉伸100个单位（`transform="translate(-100 -100)"`）。

Indeed, as the specification states, **"the effect of the `viewBox` attribute is that the user agent automatically supplies the appropriate transformation matrix to map the specified rectangle in user space to the bounds of a designated region (often, the viewport)"**.

的确，作为规范说明，**“`viewBox`属性的影响在于用户代理自动添加适当的变换矩阵来把用户空间中具体的矩形映射到指定区域的边界（通常是视口）”**。

This is just a fancy way of saying what we already mentioned before: the graphic is cropped and then **scaled** to fit into the viewport. The spec then goes on to add a note: **"in some cases the user agent will need to supply a translate transformation in addition to a scale transformation. For example, on an outermost svg element, a translate transformation will be needed if the viewBox attributes specifies values other than zero for `<min-x>` or `<min-y>`.)"**

这是一个很棒的说明我们之前已经提到的内容的方法：图形被裁切然后被**缩放**以适应视口。这个说明随后增加了一个注释：**“在一些情况下用户代理在缩放变换之外需要增加一个移动变换。例如，在最外层的svg元素上，如果viewBox属性对`<min-x>`和`<min-y>`声明非0值得那么就需要移动变换。”**

To demonstrate the translation transformation even better, let's try applying negative values (-100) to `<min-x>` and `<min-y>`. The translation effect would be then similar to `transform="translate(100 100)"`; meaning that the graphic will be translated to the bottom and to the right after being cropped and scaled. If were to revisit the second to last example with a crop size of 400 by 300, and then add the new negative `<min-x>` and `<min-y>` values, this would be our new code:

为了更好演示移动变换，让我们试着给`<min-x>`和`<min-y>`添加-100。移动效果类似`transform="translate(100 100)"`；这意味着图形会在切割和缩放后移动到右下方。回顾倒数第二个裁切尺寸为400*300的例子，添加新的无效`<min-x>`和`<min-y>`值，新的代码如下：

	<svg width="800" height="600" viewbox="-100 -100 300 200">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

The result of applying the above `viewBox` transformation to the graphic is shown in the following image:

给图形添加上述`viewBox` transformation的结果如下图所示：

![](svg/viewbox-400-300-crop-translate.jpg)

Note that, unlike the `transform` attribute, the automatic transformation that is created due to a `viewBox` does not affect the `x, y, width` and `height` attributes on the element with the `viewBox` attribute. Thus, in the example above which shows an `svg` element which has attributes `width, height` and `viewBox`, the `width` and `height` attributes represent values in the coordinate system that exists before the `viewBox` transformation is applied. You can see this in the above examples as the initial (grey) viewport coordinate system remains unaffected even after using the `viewBox` attribute on the `<svg>`.

注意，与`transform`属性不同，因为viewBox自动添加的tranfomation不会影响有`vewBox`属性的元素的`x`,`y`,宽和高等属性。因此，在上述例子中展示的带有`width`,`height`和`viewBox`属性的`svg`元素，`width`和`height`属性代表添加`viewBox` 变换之前的坐标系中的值。在上述例子中你可以看到初始（灰色）viewport坐标系甚至在`<svg>`上使用了`viewBox`属性后仍然没有影响。

On the other hand, like the `transform` attribute, it does establish a new coordinate system for all other attributes and for descendant elements. You can also see that in the above examples as the user coordinate system established is a new one—it does not remain as the initial user coordinate system which was identical to the viewport coordinate system before the `viewBox` was used. And any descendants of the `<svg>` will be positioned and sized in the **new** user coordinate system, not the initial one.

另一方面，像`tranform`属性一样，它给所有其他属性和后代元素建立了一个新的坐标系。你还可以看到在上述例子中，用户坐标系是新建立的-它不是保持像初始用户坐标系和使用`viewBox`前的视口坐标系一样。任何`<svg>`后代会在这个**新**的用户坐标系中定位和确定尺寸，而不是初始坐标系。

Our last `viewBox` example is similar to the previous ones, but instead of cropping the canvas, we're going to extend it inside the viewport and see how it affects the graphic. We're going to specify a viewbox with a width and height that are larger than those of the viewport, while also maintaining the aspect ratio of the viewport. We'll deal with different aspect ratios in the next section.

最后一个`viewBox`的例子和前一个类似，但是它不是切割画布，我们将在viewport里扩展它并看它如何影响图形。我们将声明一个宽高比视口大的viewBox，并依然保持viewport的宽高比。我们在下一章里讨论不同的宽高比。

In this example, we'll make the viewbox 1.5 times the size of the viewport.

在这个例子中，我们将viewbox的尺寸设为viewport的1.5倍。

	<svg width="800" height="600" viewbox="0 0 1200 900">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

What will happen now is that the user coordinate system is going to be scaled up to 1200x900. It will then be mapped to the viewport coordinate system so that every 1 unit in the user coordinate system is equal to `viewport-width / viewBox-width` horizontally, and `viewport-height / viewBox-height` units vertically in the viewport coordinate system. This means that, in this case, every one x-unit in the user coordinate system is equal to 0.66 x-units in the viewport coordinate system, and every one user y-unit is mapped to 0.66 viewport y-units.

现在用户坐标系会被放大到1200*900。它会被映射到视口坐标系，用户坐标系中的每一个单位水平方向上等于视口坐标系中的`viewport-width / viewBox-width`，竖直方向上等于`viewport-height / viewBox-height`。这意味着，在这种情况下，每一个用户坐标系中的x-units等于viewport坐标系中的0.66个x-units，每个用户y-unit映射成0.66的viewport y-units。

Of course, the best way to understand this is to visualize the result. The viewbox is scaled so that it fits inside the viewport as shown in the following image. And because the graphic is drawn on the canvas based on the new user coordinate system, not the viewport coordinate system, it will look smaller inside the viewport.

当然，理解这些最好的方法是把结果视觉化。viewBox被缩放到适应下图所示的viewport。因为图形在画布里基于新的用户坐标系绘制的，而不是视口坐标系，它看起来比视口小。

![](svg/viewbox-1200-900.jpg)

So far, all of our examples have been in conformity with the viewport's height to width aspect ratio. But what happens if the height and width specified in the `viewBox` have a different aspect ratio than that of the viewport's? For example, suppose we set the dimensions of the viewbox to be 1000x500. The aspect ratio of height to width is no longer the same as that of the viewport. The result of using `viewBox = "0 0 1000 500"` in our example looks like the following:

到目前为止，我们所有的例子的宽高比都和视口一致。但是如果`viewBox`中声明的宽高比和视口中的不一样会发生什么呢？例如，试想我们把视口的尺寸设为1000*500。宽高比不再和视口的一样。在例子中使用`viewBox="0 0 1000 500"`的结果如下图：

![](svg/viewbox-1000-500.jpg)

The user coordinate system and hence the graphic is positioned inside the viewport so that:

* The entire viewbox fits inside the viewport.
* The aspect ratio of the viewbox is preserved. The viewbox was not stretched to cover the viewport area.
* THe viewbox is centered inside the viewport both vertically and horizontally.

用户坐标系。因此图形在视口中定位：

* 整个viewbox适应视口。
* 保持viewbox的宽高比。viewbox没有被拉伸来覆盖视口区域。
* viewbox在视口中水平垂直居中。

This is the default behavior. What controls this behavior? And what if we want to change the position of the viewbox inside the viewport? This is where the `preserveAspectRatio` attribute comes in.

这是默认表现。那用什么控制表现呢？如果我们想改变视口中viewbox的位置呢？这就需要用到`preserveAspectRatio`属性了。

##The `preserveAspectRatio` Attribute
##`preserveAspectRatio`属性

The `preserveAspectRatio` attribute is used to force a uniform scaling for the purposes of preserving the aspect ratio of a graphic.

`preserveAspectRatio`属性强制统一缩放比来保持图形的宽高比。

If you define a user coordinate system with an aspect ratio different from that of the viewport's, and if the browser were to stretch the viewbox to fit into the viewport as we've seen in previous examples, the difference in aspect ratios will cause the graphic to be distorted in either direction. So if the viewbox in the last example were to be stretched to fill the viewport in both directions, the graphic would look like so:

如果你用不同于视口的宽高比定义用户坐标系，如果像我们在之前的例子中看到的那样浏览器拉伸viewbox来适应视口，宽高比的不同会导致图形在某些方向上扭曲。所以如果上一个例子中的viewbox被拉伸以在所有方向上适应视口，图形看起来如下：

![](svg/viewbox-1000-500-stretched.jpg)

The distortion is also clearly visible (and unwanted, of course) when using a viewbox value of `0 0 200 300`, which would be smaller than the dimensions of the viewport. I chose this value in particular so that the viewbox matches the size of the bounding box of the parrot. If the browser were to stretch the graphic to fill the entire viewport, it would look like the so:

当给viewbox设置`0 0 200 300`的值时扭曲显而易见（显然这很不理想），这个值小于视口尺寸。我故意选择这个尺寸从而让viewbox匹配鹦鹉边界盒子的尺寸。如果浏览器拉伸图像来适应整个视口，看起来会像下面这样：

![](svg/viewbox-200-300-stretched.jpg)

The `preserveAspectRatio` attribute allows you to force uniform scaling of the viewbox, while maintaining the aspect ratio, and it allows you to specify how to position the viewbox inside the viewport if you don't want it to be centered by default.

`preserveAspectRatio`属性让你可以在保持宽高比的情况下强制统一viewbox的缩放比，并且如果不想用默认居中你可以声明viewbox在视口中的位置。

###The `preserveAspectRatio` syntax
###`preserveAspectRatio`语法

The official syntax for `preserveAspectRatio` is:
`preserveAspectRatio`的官方语法是：

	preserveAspectRatio = defer? <align> <meetOrSlice>?

It is usable on any element that establishes a new viewport (we'll get into these in the next parts of the series).

它在任何建立新viewport的元素上都有效（我们会在这个系列的下一部分讨论这个问题）。

The `defer` argument is optional, and is used only when you're applying `preserveAspectRatio` to an `<image>`. It is ignored when used on any other element. Since `<image>` it outside the scope of this article, we'll skip the `defer` option for now.

`defer`声明是可选的，并且只有当你在`<image>`上添加`preserveAspectRatio`才被用到。用在任何其他元素上时它都会被忽略。`<images>`本身不在这篇文章的讨论范围，我们暂时跳过`defer`这个选项。

The `align` parameter indicates whether to force uniform scaling and, if so, the alignment method to use in case the aspect ratio of the `viewBox` doesn't match the aspect ratio of the viewport.

`align`参数声明是否强制统一放缩，如果是，对齐方法会在`viewBox`的宽高比不符合viewport的宽高比的情况下生效。

If the `align` value is set to `none`, for example:

如果`align`值设为`none`，例如：

	preserveAspectRatio = "none"

The graphic will be scaled to fit inside the viewport without maintaining the aspect ratio, just like we saw in the last two examples.

图形不在保持宽高比而会缩放来适应视口，像我们在上面两个例子中看到的那样。

All other values of `preserveAspectRatio` force uniform scaling while preserving the viewbox's aspect ratio, and specify how to align the viewbox inside the viewport. We'll get into the values of `align` shortly.

其他所有`preserveAspectRatio`值都在保持viewbox的宽高比的情况下强制拉伸，并且指定在视口内如何对齐viewbox。我们会简短介绍`align`的值。

The last argument, `meetOrSlice` is also optional, and it defaults to `meet`. This argument specifies whether or not the entire `viewBox`should be visible inside the viewport. If provided, it is separated from the `align` parameter by one or more spaces. For example:

最后一个属性，`meetOrSlice`也是可选的，默认值为`meet`。这个属性声明整个`viewBox`在视口中是否可见。如果是，它和`align`参数通过一个或多个空格分隔。例如：

	preserveAspectRatio = "xMinYMin slice"

These values may seem foreign at first. To make understanding them easier and make them more familiar, you can think of the `meetOrSlice` value as being similar to the `background-size` values `contain` and `cover`; they work pretty much the same. `meet` is similar to `contain`, and `slice` is similar to `cover`. Here are the definitions and meaning of each value:

这些值第一眼看起来也许很陌生。为了让它们更易于理解和熟悉，你可以把`meetOrSlice`的值类比于`background-size`的`contain`和`cover`值;它们非常类似。`meet`类似于`contain`，`slice`类似于`cover`。下面是每个值的定义和含义：

####*meet (The default value)*
####*meet（默认值）*

Scale the graphic as much as possible while maintaining the following two criteria:

基于以下两条准侧尽可能缩放元素：

* aspect ratio is preserved
* the entire `viewBox` is visible within the viewport

* 保持宽高比
* 整个`viewBox`在视口中可见

In this case, if the aspect ratio of the graphic does not match the viewport, some of the viewport will extend beyond the bounds of the `viewBox` (i.e., the area into which the `viewBox` will draw will be smaller than the viewport). (See the last example of The viewBox section.) In this case, the boundaries of the `viewBox` are contained inside the viewport such that the boundaries *meet*.

在这个情况下，如果图形的宽高比不符合视口，一些视口会超出`viewBox`的边界（即`viewBox`绘制的区域会小于视口）。（在viewBox一节查看最后的例子。）在这个情况下，`viewBox`的边界被包含在viewport中使得边界*满足*。

*This value is similar to `background-size: contain`. The background image is scaled as much as possible while preserving its aspect ratio and making sure it fits entirely into the background painting area. If the aspect ratio of the background is not the same as that of the element it is being applied to, parts of the background painting area will not be covered by the background image.*

*这个值类似于`background-size: contain`。背景图片在保持宽高比的情况下尽可能缩放并确保它适合背景绘制区域。如果背景的长宽比和应用的元素的长宽比不一样，部分背景绘制区域会没有背景图片覆盖。*

####slice
####薄片

Scale the graphic so that the `viewBox` covers the entire viewport area, while maintaining its aspect ratio. The `viewBox` is scaled **just enough** to cover the viewport area (in both dimensions), but it is not scaled any more than needed to achieve that. In other words, it is scaled to the smallest size such that the width and height of the viewBox can completely cover the viewport.

在保持宽高比的情况下，缩放图形直到`viewBox`覆盖了整个视口区域。`viewBox`被缩放到**正好**覆盖视口区域（在两个维度上），但是它不会缩放任何超出这个范围的部分。换而言之，它缩放到viewBox的宽高可以正好完全覆盖视口。

In this case, if the aspect ratio of the viewBox does not match the viewport, some of the viewBox will extend beyond the bounds of the viewport (i.e., the area into which the viewBox will draw is larger than the viewport). This will result in part of the `viewBox` being *sliced off*.

在这种情况下，如果viewBox的宽高比不适合视口，一部分viewBox会扩展超过视口边界（即，viewBox绘制的区域会比视口大）。这会导致部分`viewBox`被切片。

*You can think of this as being similar to background-size: cover. In the case of a background image, the image is scaled while preserving its intrinsic aspect ratio (if any), to the smallest size such that both its width and its height can completely cover the background positioning area.*

*你可以把这个类比为background-size: cover。在背景图片的情况中，图片在保持本身宽高比（如何）的情况下缩放到宽高可以完全覆盖背景定位区域的最小尺寸。*

So, `meetOrSlice` is used to specify whether or not the `viewBox` will be completely contained inside the viewport, or if it should be scaled as much as needed to cover the entire viewport, even if this means that a part of the viewbox will be "sliced off".

所以，`meetOrSlice`被用来声明`viewBox`是否会被完全包含在视口中，或者它是否应该尽可能缩放来覆盖整个视口，甚至意味着部分的viewbox会被“切片”。

For example, if we were to apply `viewBox` size of 200x300, and using both the `meet` and `slice` values, keeping the `align` value set to the default by the browser, the result for each value will look like the following:

例如，如果我们声明`viewBox`的尺寸为200*300，并且使用了`meet`和`slice`值，保持`align`值为浏览器默认，每个值的结果会看起来如下：

![](svg/viewbox-200-300-meet-vs-slice.jpg)

The `align` parameter takes one of nine values, or the `none` value. Any value other than `none` is used to uniformly scale the image preserving its aspect ratio, **and** it is also used to align the `viewBox` inside the viewport.

`align`参数使用9个值中的一个或者为`none`。任何除`none`之外的值都用来保持宽高比缩放图片，**并且**还用来在视口中对齐`viewBox`。

The `align` values works similar to the way `background-position` works when used with percentage values. You can think of the viewBox as being the background image. The way the positioning with `align` differs from `background-position` is that instead of positioning a specific point of the viewbox over a corresponding point of the viewport, it aligns specific "axes" of the viewBox with corresponding "axes" of the viewport.

当使用百分比值时，`align`值类似于`background-position`。你可以把viewBox当做背景图像。通过`align`定位和`background-position`的不同在于，不同于通过一个与视口相关的点来声明一个特定的viewbox值，它把具体的viewBox“轴”和对应的视口的“轴”对齐。

In order to understand the meaning of each of the `align` values, we're going to first introduce each of the "axes".

为了理解每个`align`值的含义，我们将首先介绍每一个“轴”。

Remember the `<min-x>` and `<min-y>` values of the `viewBox`? We're going to use each of these to define the "min-x" axis and "min-y" axis on the `viewBox`. Additionally, we're going to define two axes "max-x" and "max-y", which will be positioned at `<min-x> + <width>` and `<min-y> + <height>`, respectively. And last but not least, we'll define two axes "mid-x" and "mid-y", which are positioned at `<min-x> + (<width>/2)` and `<min-y> + (<height>/2)`, respectively.

还记得viewBox的`<min-x>`和`<min-y>`值吗？我们将使用它们来定义`viewBox`中的"min-x"和"min-y"轴。另外，我们将定义两个轴“max-x”和”max-y“，各自通过`<min-x> + <width>` 和 `<min-y> + <height>`来定位。最后，我们定义两个轴"mid-x"和"mid-y"，根据`<min-x> + (<width>/2)` 和 `<min-y> + (<height>/2)`来定位。

Did that make things more confusing? If so, have a look at the following image to see what each of those axes represents. In the image, both `<min-x>` and `<min-y>` are set to their default 0 values. The `viewBox` is set to `viewBox = "0 0 300 300"`.

这样做是不是让事情更复杂了呢？如果是这样，让我们看一下下面的图片来看一下每个轴代表了什么。在这张图片中，`<min-x>`和 `<min-y>`值都设置为0。`viewBox`被设置为`viewBox = "0 0 300 300"`。

![](svg/viewbox-x-y-axes.jpg)

The dashed grey lines in the above image represent the mid-x and mid-y axes of the viewport. We're going to use those to align the mid-x and mid-y of axes of the `viewBox` for some values. For the viewport, the min-x value is equal to 0, the min-y value is also 0, the max-x value is equal to the width of the `viewBox`, the max-y value is equal to its height, and the mid-x and mid-y represent the middle values of the width and height, respectively.

上面图片中的灰色虚线代表视口的mid-x和mid-y轴。我们将对它们赋一些值来对齐`viewBox`的mid-x和mid-y轴。对于视口，min-x的值等于0，min-y值也等于0，max-x值等于`viewBox`的宽度，max-y的值等于高度，mid-x和mid-y代表了宽度和高度的中间值。

The alignment values are:
对齐的取值包括：

**none**

Do not force uniform scaling. Scale the graphic content of the given element non-uniformly (without preserving aspect ratio) if necessary such that the element's bounding box exactly matches the viewport rectangle.

不强制统一缩放。如果必要的话，在不统一（即不保持宽高比）的情况下缩放给定元素的图像内容直到元素的边界盒完全匹配是视口矩形。

*In other words, the `viewBox` is stretched or shrunk as necssary so that it fills the entire viewport exactly, disregarding the aspect ratio. The graphic may be distorted.*

*换句话说，如果有必要的话`viewBox`被拉伸或缩放来完全适应整个视口，不管宽高比。图形也许会扭曲。*

(Note: if `<align>` is none, then the optional `<meetOrSlice>` value is ignored.)
（注意：如果`<align>`的值是none，可选的`<meetOrSlice>`值无效。）

####*xMinYMin*

Force uniform scaling.

Align the `<min-x>` of the element's `viewBox` with the smallest X value of the viewport.

Align the `<min-y>` of the element's `viewBox` with the smallest Y value of the viewport.

*Think of this as being similar to `backrgound-position: 0% 0%;`.*

####*xMinYMin*

强制统一缩放

视口X轴的最小值对齐元素`viewBox`的`<min-x>`。

视口Y轴的最小值对齐元素viewBox的`<min-y>`。

*把这个类比为`backrgound-position: 0% 0%;`。*

####*xMinYMid*

Force uniform scaling.

Align the `<min-x>` of the element's `viewBox` with the smallest X value of the viewport.

Align the midpoint Y value of the element's `viewBox` with the midpoint Y value of the viewport.

*Think of this as being similar to `backrgound-position: 0% 50%;`.*

####*xMinYMid*
强制统一缩放。

视口X轴的最小值对齐元素`viewBox`的`<min-x>`。

视口Y轴的中间值来对齐元素的viewBox的中间值。

*把这个类比为`backrgound-position: 0% 50%;`。*

####*xMinYMax*
Force uniform scaling.

Align the `<min-x>` of the element's `viewBox` with the smallest X value of the viewport.

Align the `<min-y>+<height>` of the element's `viewBox` with the maximum Y value of the viewport.

*Think of this as being similar to `backrgound-position: 0% 100%;`.*

####*xMinYMax*
强制统一缩放。

视口X轴的最小值对齐元素`viewBox`的`<min-x>`。

视口X轴的最大值对齐元素的`viewBox`的`<min-y>+<height>`。

*把这个类比为`backrgound-position: 0% 100%;`。*

####*xMidYMin*
Force uniform scaling.

Align the midpoint X value of the element's `viewBox` with the midpoint X value of the viewport.

Align the `<min-y>` of the element's `viewBox` with the smallest Y value of the viewport.

*Think of this as being similar to `backrgound-position: 50% 0%;`.*

####*xMidYMin*
强制统一缩放。

视口X轴的中间值对齐元素的`viewBox`的X轴中间值。

视口Y轴的中间值对齐元素的`viewBox`的 `<min-y>`。

*把这个类比为`backrgound-position: 50% 0%;`。*

####*xMidYMid (The default value)*

Force uniform scaling.

Align the midpoint X value of the element's `viewBox` with the midpoint X value of the viewport.

Align the midpoint Y value of the element's `viewBox` with the midpoint Y value of the viewport.

*Think of this as being similar to `backrgound-position: 50% 50%;`.*

####*xMidYMid (默认值)*

强制统一缩放。

视口X轴的中间值对齐元素的`viewBox`的X轴中间值。

视口Y轴的中间值对齐元素的`viewBox`的Y轴中间值。

*把这个类比为`backrgound-position: 50% 50%;`。*

####*xMidYMax*

Force uniform scaling.

Align the midpoint X value of the element's `viewBox` with the midpoint X value of the viewport.

Align the `<min-y>+<height>` of the element's `viewBox` with the maximum Y value of the viewport.

*Think of this as being similar to `backrgound-position: 50% 100%;`.*

####*xMidYMax*
强制统一缩放。

视口X轴的中间值对齐元素的`viewBox`的X轴中间值。

视口Y轴的最大值对齐元素的`viewBox`的`<min-y>+<height>`。

*把这个类比为`backrgound-position: 50% 100%;`。*

####*xMaxYMin*
Force uniform scaling.

Align the `<min-x>+<width>` of the element's `viewBox` with the maximum X value of the viewport.

Align the `<min-y>` of the element's `viewBox` with the smallest Y value of the viewport.

*Think of this as being similar to `backrgound-position: 100% 0%;`.*

####*xMaxYMin*

强制统一缩放。

视口X轴的最大值对齐元素的`viewBox`的 `<min-x>+<width>`。

视口Y轴的最小值对齐元素的`viewBox`的`<min-y>`。

*把这个类比为`backrgound-position: 100% 0%;`。*


####*xMaxYMid*
Force uniform scaling.

Align the `<min-x>+<width>` of the element's `viewBox` with the maximum X value of the viewport.

Align the midpoint Y value of the element's `viewBox` with the midpoint Y value of the viewport.

*Think of this as being similar to `backrgound-position: 100% 50%;`.*

####*xMaxYMid*
强制统一缩放。

视口X轴的最大值对齐元素的`viewBox`的 `<min-x>+<width>`。

视口Y轴的中间值对齐元素的`viewBox`的Y轴中间值
。

*把这个类比为`backrgound-position: 100% 50%;`。*

####*xMaxYMax*

Force uniform scaling.

Align the `<min-x>+<width>` of the element's `viewBox` with the maximum X value of the viewport.

Align the `<min-y>+<height>` of the element's `viewBox` with the maximum Y value of the viewport.

*Think of this as being similar to `backrgound-position: 100% 100%;`.*

####*xMaxYMax*
强制统一缩放。

视口X轴的最大值对齐元素的`viewBox`的 `<min-x>+<width>`。

视口Y轴的最大值对齐元素的`viewBox`的 `<min-y>+<height>`。

*把这个类比为`backrgound-position: 100% 100%;`。*

So, using the `align` and `meetOrSlice` values of the `preserveAspectRatio` attribute, you can specify whether or not to scale the `viewBox` uniformly, how to align it inside the viewport, and whether or not it should be entirely visible inside the viewport.

所以，通过使用`preserveAspectRatio`属性的`align`和`meetOrSlice`值，你可以声明是否统一缩放`viewBox`，是否和视口对齐，在视口中是否整个可见。

Sometimes, and depending on the size of the `viewBox`, some values may have similar results. For example, in the `viewBox="0 0 200 300"` example from earlier, some alignments are identical using different `align` values. The value of `meetOrSlice` is set to `meet`in this case so that the entire `viewBox` is contained inside the viewport.

有时候，取决于`viewBox`的尺寸，一些值可能会导致相似的结果，例如在早先`viewBox="0 0 200 300"`的例子中，一些对齐完全用了不同的`align`值。这时候就要设置`meetOrSlice`的值为`meet`来保证`viewBox`包含在viewport内。

![](svg/viewbox-meet-align-same.jpg)

If we were to change the `meetOrSlice` value to `slice`, we'd get different results for different values. Notice how the viewBox is stretched so that it covers the entire viewport. The x-axis is stretched so that the 200 units cover the viewport's 800 units. In order for this to happen, and to maintain the aspect ratio of the viewbox, the y-axis gets "sliced off" at the bottom, but you can image it extending below the viewport's height.

如果我们把`meetOrSlice`的值改成`slice`，不同的值我们将得到不同的结果。注意viewBox是如何拉伸来覆盖整个视口的。x轴被拉伸到用200单位来覆盖视口800单位。为了达到这个目的，并且保持viewbox的宽高比，y轴在底部被“裁切”，但是你可以想象它在视口中高度上的延伸。

![](svg/viewbox-slice-align-same.jpg)

Of course, different `viewBox` values will also look different from the 200x300 we're using here. For the sake of brevity, I won't get into more examples, and I'll leave you to play with an interactive demo I created to help you better visualize how the `viewBox` and different `preserveAspectRatio` values work together when different values are used. You can check the interactive demo out by visiting the link in the next section.

当然，不同的`viewBox`值看起来不同于我们这里用的200*300。为了保持简洁，我们不再列举更多的例子，你可以看我创建的一些互动演示来帮助你更好地形象化理解`viewBox`和`preserveAspectRatio`在不同值下的效果。你可以在一下节中查看互动演示例子的链接。

But before we move to that, I just want to note that the mid-x, mid-y, max-x, and max-y values change if the values of the `<min-x>` and `<min-y>` change. You can play with the interactive demo and change these values to see how the axes and thus the alignment of the viewBox changes accordingly.

但是在这之前，我想要提醒你注意如果`<min-x>` 和 `<min-y>`值改变，那么mid-x, mid-y, max-x, 和 max-y的值也会发生改变。你可以在互动演示中改变这些值来查看轴以及相关联的`viewBox`的对齐方式的改变。

The following image shows the effect of using `viewBox = "100 0 200 300"` on the position of the alignment axes. We're using the same example as earlier, but instead of having the `<min-x>` value be set to zero, we're setting it to 100. You can set them to any number value you want. Notice how the min-x, mid-x, and max-x axes change. The `preserveAspectRatio` used here is the default `xMinYMin meet`, which means that the mid-* axes are aligned with the middle axes of the viewport.

下面图片展示了定位轴的位置为`viewBox = "100 0 200 300"`时的效果。和之前用一样的例子，但是我们把`<min-x>`的值设为100而不是之前的0。你可以设置成任何你想要的值。注意min-x, mid-x, 和 max-x轴是如何变化的。这里使用的`preserveAspectRatio`值为默认的`xMinYMin meet`，意味着mid-*轴和视口轴的中间对齐。

![](svg/viewbox-axes-changed-min-x-min-y.jpg)

##The Interactive Demo
##互动演示

The best way to understand how the viewport, `viewBox`, and different `preserveAspectRatio` values work and interact together is by visualizing them.

要理解viewport, `viewBox`, 以及不同的`preserveAspectRatio`值是如何工作的最好方法是可视化的演示。

For that purpose, I created a simple interactive demo that allows you to change the values of these attributes and see the result of the new values live.

出于这个目的，我创建了一个简单的互动演示，你可以改变这些属性的值来查看新值导致的结果。

![](svg/viewbox-demo-screenshot.jpg)

<a class="button" href="http://sarasoueidan.com/demos/interactive-svg-coordinate-system/index.html">Check the interactive demo out.</a>

I hope you found this article useful in understanding the SVG viewport, `viewBox`, and `preserveAspectRatio` concepts. If you'd like to learn more about SVG coordinate systems, like nesting coordinate systems, establishing new ones, and transformations in SVG, stay tuned for the remaining parts of this series. You can subscribe to the RSS (link below) or follow me on Twitter to stay updated. Thank you very much for reading!

我希望这篇文章在帮助你理解SVG viewport, `viewBox`, 和 `preserveAspectRatio` 内容时有作用。如果你想要了解更多关于SVG坐标系的内容，例如嵌套坐标系，建立一个新的坐标系以及SVG中的变换，继续阅读这一系列接下来的部分。你可以通过RSS订阅（链接在下面）或者在Twitter上关注来获取最新信息。感谢你的阅读！