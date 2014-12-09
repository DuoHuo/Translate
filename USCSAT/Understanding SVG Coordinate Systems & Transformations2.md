#Understanding SVG Coordinate Systems & Transformations (Part 2) – The `transform` Attribute
#理解SVG坐标系统和变换（第二部分）- `transform`属性

SVG elements can be transformed by scaling, translating, skewing, and rotating—much like HTML elements can be transformed using CSS Transforms. However, there are certain inevitable differences when it comes to the coordinate systems used and affected by these transformations. In this article we'll go over the SVG `transform` attribute and CSS property, covering how to use it, and things you should know about SVG coordinate system transformations.

SVG元素可以通过缩放，移动，倾斜和旋转来变换-类似HTML元素使用CSS transform来变换。然而，当涉及到坐标系时这些变换所产生的影响必然有一定差别。在这篇文章中我们讨论SVG的`transform`属性和CSS属性，包括如何使用，以及你必须知道的关于SVG坐标系变换的知识。

This is the second article in a series I'm writing about SVG coordinate systems and transformations. In the first article, I covered everything you need to know to understand the basics of SVG coordinate systems; more specifically, the SVG viewport, and the `viewBox` and `preserveAspectRatio` attributes.

这是我写的SVG坐标系统和变换部分的第二篇。在第一篇中，包括了任何要理解SVG坐标系统基础的需要知道的内容；更具体的是， SVG viewport, `viewBox` 和 `preserveAspectRatio` 属性。

* [Understanding SVG Coordinate Systems & Transformations (Part 1) – The viewport, `viewBox`, & `preserveAspectRatio`](http://sarasoueidan.com/blog/svg-coordinate-systems)
* Understanding SVG Coordinate Systems & Transformations (Part 2) – The `transform` Attribute
* [Understanding SVG Coordinate Systems & Transformations (Part 3) – Establishing New Viewports](http://sarasoueidan.com/blog/nesting-svgs)

* [理解SVG坐标系和变换（第一部分）-viewport，`viewBox`，和`preserveAspectRatio`](http://sarasoueidan.com/blog/svg-coordinate-systems)
* 理解SVG坐标系和变换（第二部分）-`transform`属性
* [理解SVG坐标系和变换（第三部分）-建立新视口](http://sarasoueidan.com/blog/nesting-svgs)

In this part I'm going to assume you read the first one, so, if you haven't, make sure you do before you continue reading this article.

这一部分我建议你先阅读第一篇，如果没有，确保你在阅读这篇之前已经读了第一篇。

##The `transform` Attribute Values
##`transform`属性值

The `transform` attribute is used to specify one or more transformations on an element. It takes a `<transform-list>` as a value which is defined as a list of transform definitions, which are applied in the order provided. The individual transform definitions are separated by whitespace and/or a comma. An example of applying a transformation to an element may look like the following:

`tranform`属性用来对一个元素声明一个或多个变换。它输入一个带有顺序的变换定义列表的`<transform-list>`值。每个变换定义由空格或逗号隔开。给元素添加变换看起来如下：

The possible SVG transformations are: *rotation, scaling, translation*, and *skewing*. The transformation functions used in the `transform` attribute work similar to the way CSS transform functions work in the `transform` property, except that they take different arguments.

有效地SVG变换有：*旋转, 缩放, 移动*, 和* 倾斜*。`transform`属性中使用的变换函数类似于CSS中transform属性使用的CSS变换函数，除了参数不同。

*Note that the function syntax defined below only works in the `transform` attribute. See the [section about transforming SVGs with CSS properties](http://sarasoueidan.com/blog/svg-transformations/#css-transformation-properties) for information on the syntax used in the CSS transform properties.*

*注意下列的函数语法定义只在`transform`属性中有效。查看[section about transforming SVGs with CSS properties](http://sarasoueidan.com/blog/svg-transformations/#css-transformation-properties)获取关于CSS变换属性中使用的语法信息。*

###Matrix
###矩阵

You can apply one or more transformations to an SVG element using the `matrix()` function. The syntax for the matrix transformation is:
你可以使用`matrix()`函数在SVG元素上添加一个或多个变换。matrix变换语法如下：

	matrix(<a> <b> <c> <d> <e> <f>)

The above declaration specifies a transformation in the form of a transformation matrix of six values. `matrix(a,b,c,d,e,f)` is equivalent to applying the transformation *matrix [a b c d e f]*.

上述声明通过一个有6个值的变换矩阵声明一个变换。`matrix(a,b,c,d,e,f)`等同于添加变换*matrix[a b c d e f]*。

For those of you who are not math-savvy, you're probably not going to be using this function. Those of you who are, you can read more about the math behind it here. Since this function is rarely used—if ever—I'm just going to skip to the other transformation functions.

如果你不精通数学，最好不要用这个函数。对于那些精通的人，你可以在[这里](http://www.w3.org/TR/SVG/coords.html#TransformMatrixDefined)阅读更多关于数学的内容。因此这个函数很少使用-我将忽略来讨论其他变换函数。

###Translation
###移动

To translate an SVG element, you can use the translate() function. The syntax for the translation function is:
要移动SVG元素，你可以用translate()函数。translate函数的语法如下：

	translate(<tx> [<ty>])

The `translate()` function takes one or two values which specify the horizontal and vertical translation values, respectively. `tx`represents the translation value along the x-axis; `ty` represents the translation value along the y-axis.

`translate()`函数输入一个或两个值得来声明水平和竖直移动值。`tx`代表x轴上的translation值；`ty`代表y轴上的translation值。

The `ty` value is optional; and, if omitted, it defaults to zero. The `tx` and `ty` values can be either space-separated or comma-separated, and they don't take any units inside the function—they default to the current user coordinate system units.

`ty`值是可选的，如果省略，默认值为0。`tx`和`ty`值可以通过空格或者逗号分隔，它们在函数中不代表任何单位-它们默认等于当前用户坐标系单位。

The following example translates an element by 100 user units to the right, and 300 user units to the bottom:

下面的例子把一个元素向右移动100个用户单位，向下移动300个用户单位。

	<circle cx="0" cy="0" r="100" transform="translate(100 300)" />

The above example is still valid if the transformation was applied using `translate(100, 300)` where the values are comma-separated.

上述代码如果以`translate(100, 300)`用逗号来分隔值的形式声明一样有效。

###Scaling
###缩放

You can resize an SVG element by scaling it up or down using the `scale()` function transformation. The syntax for the scale transformation is:
你可以通过使用`scale()`函数变换来向上或者向下缩放来改变SVG元素的尺寸。scale变换的语法是：

	scale(<sx> [<sy>])

The `scale()` function takes one or two values which specify the horizontal and vertical scaling values, respectively. `sx` represents the scaling value along the x-axis, used to stretch or shrink the element horizontally; `sy` represents the scaling value along the y-axis, used to stretch or shrink the element vertically.

`scale()`函数输入一个或两个值来声明水平和竖直缩放值。`sx`代表沿x轴的缩放值，用来水平延长或者拉伸元素；`sy`代表沿y轴缩放值，用来垂直延长或者缩放元素。

The `sy` value is optional; and, if omitted, it is assumed to be equal to `sx`. The `sx` and `sy` values can be either space-separated or comma-separated, and they are unitless numbers.

`sy`值是可选的，如果省略默认值等于`sx`。`sx`和`sy`可以用空格或者逗号分隔，它们是无单位值。

The following example doubles the size of an element by scaling it to twice its original size:

下面例子把一个元素的尺寸根据最初的尺寸放大两倍：

	<rect width="150" height="100" transform="scale(2)" x="0" y="0" />

The following stretches an element horizontally to 1.5 its original width, and shrinks it vertically to half its original height:

下列例子把一个元素缩放到最初宽度的两倍，并且把高度压缩到最初的一半：

	<rect width="150" height="100" transform="scale(2 0.5)" x="0" y="0" />

The above example is still valid if the transformation was applied using `scale(2, .5)` where the values are comma-separated.

上述例子使用逗号分隔的值例如`scale(2, .5)`仍然有效。

It is important to note here that *when an SVG element is scaled, its entire current coordinate system is scaled, resulting in the element also being repositioned inside the viewport*. Don't worry about this now, we'll get into it in more detail in the next section.

这里需要注意*当SVG元素缩放时，整个坐标系被缩放，导致元素在视口中重新定位*，现在不用担心这些，我们会在下一节中讨论细节。

###Skew
###倾斜

An SVG element can also be skewed. To skew it, you can use one or both of the two skew transformation functions: `skewX` and `skewY`.

SVG元素也可以被倾斜，要倾斜一个元素，你可以使用一个或多个倾斜函数`skewX` 和 `skewY`。

	skewX(<skew-angle>)
	skewY(<skew-angle>)

The `skewX` function specifies a skew transformation along the x-axis; and the `skewY` function specifies a skew transformation along the y-axis.

函数`skewX`声明一个沿x轴的倾斜；函数`skewY`声明一个沿y轴的倾斜。

The skew angle specified is a **unitless** angle that defaults to degrees.

倾斜角度声明是**无单位**角度的默认是度。

Note that skewing an element may result in the element being repositioned inside the viewport. More about this in the next section.

注意倾斜一个元素可能会导致元素在视口中重新定位。在下一节中有更多细节。

###Rotation
###旋转

You can rotate an SVG element using the `rotate()` function. The syntax for the function is:
你可以使用`rotate()`函数来旋转SVG元素。这个函数的语法如下：

	rotate(<rotate-angle> [<cx> <cy>])

The `rotate()` function specifies a rotation by `rotate-angle` **degrees** about a given point. Unlike rotation transformations in CSS, you cannot specify an angle unit other than degrees. The angle value is specified **unitless**, and is considered a degrees value by default.

`rotate()`函数对于给定的点和
`旋转角度`值执行旋转。不像CSS3中的旋转变换，不能声明除degress之外的单位。角度值默认**无单位**，默认单位是度。

The optional `cx` and `cy `values represent the **unitless** coordinates of the point used as a center of rotation. If `cx` and `cy` are not provided, the rotation is about *the origin of the current user coordinate system*. (See [Part 1](http://sarasoueidan.com/blog/svg-coordinate-systems) if you're not sure what a user coordinate system is.)

可选的`cx`和`cy`值代表**无单位**的旋转中心点。如果没有设置`cx`和`cy`，旋转点是**当前用户坐标系的原点**（查看[第一部分](http://sarasoueidan.com/blog/svg-coordinate-systems)如果你不知道用户坐标系是什么。）

Specifying a center of rotation inside the `rotate()` function is like a shorthand way for setting `transform: rotate()` and `transform-origin` in CSS. Since the default center of rotation in SVG is the upper left corner of the current user coordinate system in use, and since that may not allow you to create the rotation effect you want, you will probably end up specifying a new center inside `rotate()`. If you know your element's dimensions and position in the SVG canvas, you can easily specify its center as the center of rotation.

在函数`rotate()`中声明旋转中心点一个快捷方式类似于CSS中设置`transform: rotate()`和`transform-origin`。SVG中默认的旋转中心是当前使用的用户坐标系的左上角，这样也许你无法创建想要的旋转效果，你可以在`rotate()`中声明一个新的中心点。如果你知道元素在SVG画布中的尺寸和定位，你可以把它的中心设置为旋转中心。

The following example rotates a group of elements around a specified center of rotation positioned at (50, 50) in the current user coordinate system:

下面的例子是以当前用户坐标系中的(50,50)点为中心进行旋转一组元素：

	<g id="parrot" transform="rotate(45 50 50)" x="0" y="0">
	    <!-- elements making up a parrot shape -->
	</g>

However, if you want an element to rotate around its center, you'd probably rather specify the center as `50% 50%` like you would do in CSS; but unfortunately doing that inside the `rotate()` function is not possible—you need to use absolute coordinates. However, you can do this using the CSS `transform-origin` property in conjunction with the CSS `transform` property. More about this later in the article.

然而，如果你想要一个元素围绕它的中心旋转，你也许想要像CSS中一样声明中心为`50% 50%`；不幸的是，在`rotate()`函数中这样做是不允许的-你必须用绝对坐标。然而，你可以在CSS的`transform`属性中使用`transform-origin`属性。这篇文章后面会讨论更多细节。

##Coordinate System Transformations
##坐标系变化

Now that we've covered all possible SVG transformation functions, we'll dig into the visual part and the effect of applying each transformation to an SVG element. This is the most important aspect of SVG transformations. And they are called "coordinate system transformations" not just "element transformations" for a reason.

现在我们已经讨论了所有可能的SVG变换函数，我们深入挖掘视觉部分和对SVG元素添加每个变换的效果。这是SVG变换最重要的部分。因此它们被称为“坐标系统变换"而不仅仅是“元素变换”。

In the [specification](http://www.w3.org/TR/SVG/coords.html), the `transform` attribute is defined as being one of the two attributes that **establish a new user space (current coordinate system)** on the element it is applied to — the viewBox attribute is the second of the two attributes that create a new user space. So what exactly does this mean?

在这个[说明](http://www.w3.org/TR/SVG/coords.html)中，`transform`属性被定义成两个在被添加的元素上**建立新用户空间（当前坐标系）**之一-viewBox属性是创建新用户空间的两个属性中的另一个。所以到底是什么意思呢？

This behavior is similar to the behavior of CSS transformations applied to an HTML element—the HTML element's coordinate system is transformed, and this is usually most obvious when you're chaining tranformations (we'll get to this later). Despite being similar in many aspects, HTML and SVG transformations have some differences.

这个行为类似于在HTML元素上添加CSS变换-HTML元素坐标系发生了变换，当你把变换组合使用时最明显。虽然在很多方面很相似，HTML和SVG的变换还是有一些不同。

The main difference is the coordinate system. The coordinate system of an HTML element is established on the element itself. Meanwhile, in SVG, the coordinate system of an element is, initially, the current coordinate system or user space in use.

主要的不同是坐标系。HTML元素的坐标系建立在元素自身智商。然而，在SVG中，元素的坐标系最初是当前坐标系或使用中的用户空间。

When you apply the `transform` attribute to an SVG element, that element gets a "copy" of the current user coordinate system in use. You can think of it as just creating a new "layer" for the transformed element, where the new layer has its own copy of the current user coordinate system (the `viewBox`).

当你在一个SVG元素上添加`transform`属性，元素获取当前使用的用户坐标系的一个“副本”。你可以当做给发生变换的元素创建一个新“层”，新层上是当前用户坐标系的副本（the `viewBox`）。

Then, **the element's new current coordinate system is transformed by the transformation functions specified inside the `transform`attribute**, thus resulting in the transformation of the element itself. It is as if the elements are drawn onto the canvas in the transformed coordinate system.

然后，**元素新的当前坐标系被在`transform`属性中声明的变换函数改变**，因此导致元素自身的变换。这看起来好像是元素在变换后的坐标系中重新绘制。

To understand how SVG transformations are applied, let's start with the visual part. The following image shows the SVG canvas we're going to be working with.

要理解如何添加SVG变换，让我们从可视化的部分开始。下面图片是我们要研究的SVG画布。

![](svg/svg-transforms-canvas.png)

The parrot and the dog are the elements (groups `<g>`) that we're going to be transforming.

鹦鹉和小狗使我们要变换的元素(组`<g>`)。

	<svg width="800" height="800" viewBox="0 0 800 600">
	    <g id="parrot">
	        <!-- shapes and paths forming the parrot -->
	    </g>
	    <g id="dog">
	        <!-- shapes and paths forming the dog -->
	    </g>
	</svg>

The grey coordinate system is the initial coordinate system of the canvas established by the `viewBox`. For simplicity's sake, I'm going to not change the initial coordinate system—I'm using a `viewBox` that is the same size as the viewport, as you see in the above code.

灰色坐标是通过`viewBox`建立的画布的初始坐标系。为了方便起见，我将不改变初始坐标系-我用一个和视口相同尺寸的`viewBox`，如你在上述代码中看到的一样。

Now that we've established our canvas and an initial user space, we're going to start transforming elements. Let's start by translating the parrot by 150 units to the left and 200 units downwards.

现在我们建立了画布和初始用户空间，让我们开始变换元素。首先让我们把鹦鹉向左移动150单位，向下移动200个单位。

The parrot is, of course, made of several paths and shapes. It's enough to apply the `transform` attribute to the group wrapping these shapes `<g>`; this will in turn apply the transformation to the entire set of shapes and paths, and the parrot will be translated as one whole item. See the [article on structuring and grouping SVGs](http://sarasoueidan.com/blog/structuring-grouping-referencing-in-svg) for more information.

当然，鹦鹉是由若干路径和形状组成的。只要把`transform`属性添加到包含它们的组`<g>`上就行了；这会对整个形状和路径添加变换，鹦鹉会作为一个整体进行变换。查看 [article on structuring and grouping SVGs](http://sarasoueidan.com/blog/structuring-grouping-referencing-in-svg)获取更多信息。

	<svg width="800" height="800" viewBox="0 0 800 600">
	    <g id="parrot" transform="translate(150 200)">
	        <!-- shapes and paths forming the parrot -->
	    </g>
	    <!-- ... -->
	</svg>

The following image shows the result of translating the parrot by the above translation. The translucent version of the parrot shows the initial position before the transformation was applied.

下面图片展示了上述变换后的结果。鹦鹉的半透明版本是变换前的初始位置。

![](svg/svg-transformations-translate.png)

The translation transformation in SVG is as simple and straightforward as it is in CSS when applied on an HTML element. We mentioned earlier that applying the `transform` attribute to an element establishes a new current user coordinate system on it. The following image shows the "copy" of the initial coordinate system, that is established on the parrot element when it was transformed. Notice how the parrot's current coordinate system is translated.

SVG中的变换和HTML元素上CSS中的一样简单直观。我们之前提到在元素上添加`transform`属性时会在元素上创建一个新的当前用户坐标系。下面图片显示了初始坐标系的“副本”，它在鹦鹉元素发生变换时被建立。注意观察鹦鹉当前坐标系是如何变换的。

![](svg/svg-transformations-translate-system.png)

It's important to notice here that *the new current coordinate system established on the element is a replicate of the initial user space, with the position of the element preserved inside it. This means that it is not established on the element's bounding box, nor is the size of the new current coordinate system restricted to the size of the element.* This is where the difference between HTML and SVG coordinate system shines.

这里需要注意的非常重要的一点是*建立在元素上的新的当前坐标系是初始用户坐标系的复制，在里面元素的位置得以保持。这意味着它不是建立在元素边界盒上，或者新的当前坐标系的尺寸受制于元素的尺寸。*这就是HTML和SVG坐标系之间的区别。

The new current coordinate system established on a transformed element is not established on the element's bounding box, nor is its size restricted to the size of the element.

建立在变换元素上的新当前坐标系不是建立在元素边界盒上，或者新的当前坐标系的尺寸受制于元素的尺寸。

This is more evident if we are to transform the dog at the bottom right of the canvas. Suppose we want to translate the dog by 50 units to the right and then 50 units downwards. This is how the dog, its initial position, and the new current coordinate system (that is also translated with the dog) will look. Notice how the origin of the dog's new current coordinate system is not positioned at the top left cornder of the dog's bounding box. Also notice how the dog and its new coordinate system seem as if they were moved to a new "layer" on top of the canvas.

我们把小狗变换到画布的右下方时会更加明显。试想我们想要把小狗向右移动50单位，向下移动50单位。这就是狗的最初的坐标以及新的当前坐标系（也因为狗改变）会如何显示。注意小狗的新的坐标系统的原点不在狗边界盒子的左上角。另外注意狗和它新的坐标系看起来它们好像移动到画布新的一层上。

![](svg/svg-transformations-translate-dog.png)

Now let's try something else. Instead of translating the parrot, let's try scaling it. We're going to scale the parrot to double its size:

现在我们试一试其他事情。不再移动，试着缩放。我们将鹦鹉放大到两倍尺寸：

	<svg width="800" height="800" viewBox="0 0 800 600">
	    <g id="parrot" transform="scale(2)">
	        <!-- shapes and paths forming the parrot -->
	    </g>
	    <!-- ... -->
	</svg>

The result of scaling an SVG element differs from that of scaling an HTML element. The scaled SVG's element's position changes inside the viewport when it is scaled. The following image shows the result of doubling the size of the parrot. Notice the initial position and size, and the final size and position.

放缩SVG元素和放缩HTML元素的结果不一样。缩放后SVG元素的在视口中的位置随着缩放改变。下面图片展示了把鹦鹉放大到两倍时的结果。注意初始位置和尺寸，以及最终位置和尺寸。

![](svg/svg-transformations-scale.png)

What we can notice from the above image is that not only the size (width and height) of the parrot were doubled, but the coordinates (x and y) were also multiplied by the scaling factor (which is two, here).

从上面图片中我们可以注意到不只鹦鹉的尺寸（宽和高）变成了两倍，鹦鹉的坐标（x和y）也乘以了缩放因子（这里是两倍）。

The reason we ended up with this result is something we've mentioned earlier: the element's current coordinate system is transformed, and then the parrot is drawn into the new system. So, in this example, the current coordinate system was scaled. This effect is similar to the effect of using `viewBox = "0 0 400 300"`, which "zooms in" to the coordinate system, thus doubling the size of the content inside it (see [part 1](http://sarasoueidan.com/blog/svg-coordinate-systems) of the series if you haven't already).

这个结果的原因我们之前已经提到了：元素当前坐标系发生变化，鹦鹉在新系统中绘制。所以，在这个例子中，当前坐标系被缩放。这个效果类似于使用`viewBox = "0 0 400 300"`，等于“放大”了坐标系，因此把里面的内容放大到双倍尺寸（如果你还没有读过请查看这个系列的[第一部分](http://sarasoueidan.com/blog/svg-coordinate-systems)）。

So, if we were to visualize the coordinate system transformation showing the current transformed system of the parrot, we'd get the following result:

所以，如果我们把坐标系变换形象化来展现当前变换系统中的鹦鹉，我们会得到以下结果：

![](svg/svg-transformations-scale-system.png)

The new current coordinate system of the parrot is scaled up, "zooming in" to the parrot at the same time. Notice that, inside its current coordinate system, the parrot is not repositioned—it is only the effect of scaling the coordinate system that repositions it inside the viewport. The parrot is simply drawn at its original x and y coordinates inside the new scaled up system.

鹦鹉的新的当前坐标系统被缩放，同时“放大”鹦鹉。注意，在它当前的坐标系中，鹦鹉没有重新定位-只有缩放坐标系统才会导致它在视口中重定位。鹦鹉在新的缩放后的系统中按初始的x和y坐标被重绘。

Let's trying scaling the parrot in both directions using different scaling factors. If we scale the parrot by applying `transform="scale(2 0.5)`, we're doubling its width while making it half its original height. The effect will be similar to applying `viewBox="0 0 400 1200"`.

让我们尝使用不同因子在两个方向上缩放鹦鹉。如果我们添加`transform="scale(2 0.5)`缩放鹦鹉，我们把宽度变为两倍高度为原来的一半。效果和添加`viewBox="0 0 400 1200"`类似。

![](svg/svg-transformations-scale-2.png)

Notice the position of the parrot inside the scaled coordinate system, and compare it to the position in the initial system (translucent parrot): the x and y position coordinates are preserved.

注意一下鹦鹉在倾斜后的坐标系中的位置，并且把它和初始系统（半透明的鹦鹉）中的位置做比较：x和y位置坐标保持不变。

Skewing an element in SVG also results in the element being "moved" as a result of its current coordinate system being skewed.

在SVG中倾斜元素也导致元素被“移动”，因为它当前的坐标系统被倾斜了。

Suppose we apply a skew transformation to the dog along the x-axis using the `skewX` function. We're going to skew the dog by 25 degrees horizontally.

试想我们使用`skewX`函数沿x轴给一只狗增加一个倾斜变化。我们在垂直方向上把狗倾斜了25度。


	<svg width="800" height="800" viewBox="0 0 800 600">
	    <!-- ... -->
	    <g id="dog" transform="skewX(25)">
	        <!-- shapes and paths forming the dog -->
	    </g>
	</svg>

The following image shows the result of applying the skewing transformation to the dog. Its coordinate system is skewed, and so is the dog itself.

下列图片展示了对小狗添加倾斜变换的结果。

![](svg/svg-transformations-skew-system.png)

Note that the position of the dog with respect to its original position also changes, as a result of skewing its coordinate system.

注意到狗的位置对比初始位置也改变了，因为它的坐标系也被倾斜了。

The following image shows the result of skewing the dog by the same angle using `skewY()` instead of `skewX`:

下面的图片展示了同样角度的情况下使用`skewY()`而不是`skewX`倾斜狗的情况：

![](svg/svg-transformations-skew-system-2.png)

And last but not least, let's try rotating the parrot. The default center of rotation is the upper left corner of the current user coordinate system. The new current system established on the rotated element will also be rotated. In the following example, we're going to rotate the parrot by 45 degrees. The position direction of rotation is clockwise.

最后，让我们尝试旋转鹦鹉。旋转默认的中心是当前用户坐标系的左上角。新的建立在旋转元素上的当前系统也被旋转了。在下面的例子中，我们将把鹦鹉旋转45度。旋转方向为顺时针。

	<svg width="800" height="800" viewBox="0 0 800 600">
	    <g id="parrot" transform="rotate(45)">
	        <!-- shapes and paths forming the parrot -->
	    </g>
	    <!-- ... -->
	</svg>

The result of applying the above transformation looks like this:

添加上述变换的结果如下：

![](svg/svg-transformations-rotate.png)

You are probably going to want to rotate an element around a point other than the default origin of the coordinate system. Using the `rotate()` function in the `transform` attribute, you can specify that point explicitly. Suppose we want to rotate the parrot in this example around its own center. According to the width, height, and position of the parrot, I can determine its center to be at approximately (150, 170). The parrot can then be rotated around this point:

你很可能想要围绕默认坐标系原点之外的点来旋转一个元素。在`transform`属性中使用`rotate()`函数，你可以声明这个点。试想在这个例子中我们想按照它自己的中心旋转这个鹦鹉。根据鹦鹉的宽、高以及位置，我精确计算出它的中心在（150,170）。这个鹦鹉可以围着它的中心旋转。

	<svg width="800" height="800" viewBox="0 0 800 600">
	    <g id="parrot" transform="rotate(45 150 170)">
	        <!-- shapes and paths forming the parrot -->
	    </g>
	    <!-- ... -->
	</svg>

At this point, the parrot is rotated and will look like so:
在这个时候，这只鹦鹉会被旋转并且看起来如下：

![](svg/svg-transformations-rotate-center.png)

We said that the transformations are applied to the coordinate system, and because of that, the element is eventually affected and transformed. So how exactly does changing the center of rotation work on the coordinate system whose origin is at the point (0, 0)?

我们说变换添加在坐标系上，因此，元素最终被影响并且发生变换。那么究竟如何改变旋转中心工作在坐标系的原点（0，0）的点呢？

When you change the center or rotation, the coordinate system is translated, rotated by the specified angle, and then translated again by specific values depending on the center of rotation you specify. In this example, this:

当你改变中心或者旋转时，坐标系被变换或者旋转特定角度，然后再次根据声明的旋转中心产生特定变换。在这个例子中：

	<g id="parrot" transform="rotate(45 150 170)">

is performed by the browser as a series of translation and rotation operations equivalent to:

被浏览器当成一系列的移动和旋转等同于：

	<g id="parrot" transform="translate(150 170) rotate(45) translate(-150 -170)">

The current coordinate system is translated to the point you want to be the center. It is then rotated by the angle you specify. And then finally the system is translated by the negation of the values. The above transformation applied on the system looks like this:

当前坐标系变换到你想要的中心店。然后旋转声明的角度。最终系统被负值变换。上述添加到系统的变换如下：

![](svg/svg-transformations-rotate-center-system.png)

Before we move on to the next section where we're going to nest and chain transformations, I want to note that the current user coordinate system established on a transformed element is independent from other coordinate systems established on other transformed elements. The following image shows the two coordinate systems established on the dog and the parrot, and how they are independent from each other.

在我们进行下一部分讨论嵌套和组合变换前，我想请大家注意建立在变换元素上的当前用户坐标系是独立于建立在其他变换元素之上的其他坐标系的。下列图片展示了建立在狗和鹦鹉上的两个坐标系，以及它们之间是如何保持独立的。

![](svg/svg-transformations-multiple.png)

Also note that each current coordinate system still lies inside the main coordinate system of the canvas established using the`viewBox` attribute on the containing <svg>. Any transformations applied to the viewBox will affect the entire canvas and all elements inside it as well, whether they have their own established coordinate systems or not.

另外注意每个当前坐标系仍然处于在外层<svg>容器中使用`viewBox`属性建立的画布的主要坐标系中。任何添加到`viewBox`上的变换会影响整个画布以及所有里面的元素，不管它们是否建立了自己的坐标系。

For example, the following is the result of changing the user space of the entire canvas from `viewBox="0 0 800 600"` to `viewBox="0 0 600 450"`. The entire canvas is scaled up, preserving any transformations applied to the individual elements.

例如，以下是把整个画布的用户空间从`viewBox="0 0 800 600"`改成 `viewBox="0 0 600 450"`的结果。整个画布被缩放，保持任何添加到独立元素上的变换。

![](svg/svg-transformations-multiple-2.png)

###Nested and Chained Transformations
###嵌套和组合变换

A lot of times you may want to apply several transformations to an element. Applying multiple transformations in a raw is what is referred to as "chaining" transformations.

很多时候你可能想要在一个元素上添加多个变换。添加多个变换意味着“组合”变换。

When transformations are chained, the most important thing to be aware of is that, just like with HTML element transformations, each transformation is applied to the coordinate system after that system is transformed by the previous transformations.

当变换组合时，最重要的是意识到，和HTML元素变换一样，当这个系统发生了之前的变换后在添加下一个变换到坐标系中。

For example, if you're going to apply a rotation to an element, followed by a translation, the translation happens according to the new coordinate system, not the inital non-rotated one.

例如，如果你要在一个元素上添加旋转，接下来移动，移动变换会根据新的坐标系统，而不是初始的没有旋转时的系统。

The following example does just that. We're applying the previous rotation, and then translating the parrot using by 200 units along the positive x-axis`transform="rotate(45 150 170) translate(200)"`.

下面了例子就是做了这件事。我们先添加旋转，然后沿x轴使用`transform="rotate(45 150 170) translate(200)"`把鹦鹉移动200个单位。

![](svg/svg-transformations-rotate-translate.png)

Depending on the final position and transformation you're after, you need to chain your transformations accordingly. Always keep the coordinate system in mind.

取决于最终的位置和变换，你可以根据需要组合变换。总是记住坐标系。

Note that when you skew an element—and its coordinate system with it—the coordinate system will no longer be an orthogonal one, and the coordinates will no longer be calculated as orthogonal ones—they will be [skew coordinates](http://en.wikipedia.org/wiki/Skew_coordinates). Simply put, this just means that the coordinate system's origin is no longer a 90 degrees angle, and hence the new coordinates will be computed based on this new angle.

注意当你倾斜一个元素-以及它的坐标系统-坐标系统不再是最初的那个，坐标系不再会按照最初的来计算-它将会是[倾斜后的坐标系](http://en.wikipedia.org/wiki/Skew_coordinates)。简单来说，这意味着坐标系原点不再是90度的角，新的坐标会根据新的角度来计算。

Nested transformations occur when a child of a transformed element is also transformed. The transformation applied to the child element will be an accumulation of the transformations applied on its ancestors and the transformation applied on it.

当变换元素的子元素也需要变换时会发生变换嵌套。添加到子元素上的变换会累积父元素上添加的变换和它本身的变换。

So, in effect, nesting transforms is similar to chaining them; only difference is that instead of applying a series of transformations on one element, it automatically gets the transformations applied on its acestors, and then finally its own transformations are applied to it, just like we applied transformations in the chain above—one after the other.

所以，效果上来说，嵌套变化类似于组合：唯一区别是不像在一个元素上添加一系列的变化，它自动从父元素上获得变换，最后执行添加在它自身的变换，就像我们在上面添加的变换一样-一个接一个。

This is particularly useful for when you want to transform one element relative to another. For example, suppose you want to animate the tail of the dog. The tail is a descendant of the `#dog` group.

这对于你想要根据另外一个元素变换一个元素时尤其有用。例如，试想你想要给小狗的尾巴设定一个动画。这个尾巴是`#dog组`的后代。

	<svg width="800" height="800" viewBox="0 0 800 600">
	    <!-- ... -->
	    <g id="dog" transform="translate(..)">
	        <!-- shapes and paths forming the dog -->
	        <g id="head">
	            <!-- .. -->
	        </g>
	        <g id="body" transform="rotate(.. .. ..)">
	            <path id="tail" d="..." transform="rotate(..)">
	                <!-- animateTransform here -->
	            </path>
	            <g id="legs">
	                <!-- ... -->
	            </g>
	        </g>
	    </g>
	</svg>

Suppose we translate the dog group; then rotate its body by some angle around some point, and then we want to animate the tail by rotating it and animating that rotation.

试想我们变换dog组；围绕某一点把它的身体旋转一定角度，然后我们想要再把尾巴旋转一定角度。

When the tail is to be rotated, it "inherits" the transformed coordinate system of its ancestor (`#body`), which in turn inherits the transformed coordinate system of its transformed ancestor (`#dog`) as well. So, in effect, when the taill is rotated, it is as though it has been translated (by the same translation of the `#dog` group), then rotated (by the same rotation of the `#body` group), and then rotated by its own rotation. And the effect of applying a series of transformations here is the same as we explained in the chaining example above.

当尾巴被旋转后，它从祖先（`#body`）身上“继承”了变换坐标系，也从祖先（`#dog`）身上继承了变换坐标系，然后旋转（和`#body`组一样的旋转）然后在发生自身的旋转。这里添加的一系列变换的效果类似于我们之前在上述组合变换例子中解释的。

So, you see, nesting transformations has practically the same effect as chaining them on the `#tail`.

所以，你看，在`#tail`上嵌套变换实际上和组合变换有一样的效果。

##Transforming SVGs Using CSS Properties
##使用CSS属性变换SVGs

In SVG 2, the `transform` attribute is referred to as the `transform` property; this is because SVG transformations have been "exported" into the [CSS3 Transforms specification](http://dev.w3.org/csswg/css-transforms/). The latter combines the SVG Transforms, CSS 2D Transforms, and CSS 3D Transforms specifications, and introduces features like transform-origin and 3D transformations into SVG.

在SVG2中，`transform`属性简称`transform`属性；因为SVG变换已经被引入[CSS3变换规范](http://dev.w3.org/csswg/css-transforms/)中。后者结合了SVG变化，CSS2 2D变换和CSS 3D变换规范，并且把类似transform-origin 和 3D transformations引入了SVG。

The CSS transform properties specified in the CSS Transforms specifications can be applied to SVG elements. However, the values for the `transform` property functions need to follow the syntax specified in the CSS spec: function arguments must be separated with commas — space-separation alone isn't valid, but you can include one or more white space before and/or after the comma; and the `rotate()` function does not take`<cx> <cy>`values anymore — the center of rotation is specified using the `transform-origin` property. Also, the CSS transformatio functions do accept units for angles and coordinates, such as rad (radians) for angles (among others) and px, em, etc. for coordinate values.

声明在CSS变换规范中的CSS变换属性可以被添加到SVG元素上。然而，`transform`属性函数值需要遵循CSS规范中的语法声明：函数参数必须逗号隔开-空格隔开是不允许的，但是你可以在逗号前后引用一两个空格；`rotate()`函数不接受`<cx>`和`<cy>`值-旋转中心使用`transform-origin`属性声明。另外，CSS变换函数接受角度和坐标单位，例如角度的rad(radians)和坐标的px,em等。

An example of rotating an SVG element using CSS may look like the following:
使用CSS来旋转一个SVG元素看起来如下：

	#parrot {
	    transform-origin: 50% 50%; /* center of rotation is set to the center of the element */
	    transform: rotate(45deg);
	}

And SVG element can also be transformed in three-dimensional space using CSS 3D Transforms. Note that the coordinate systems are still, however, different from the coordinate systems established on HTML elements. This means that 3D rotations will also look different unless you change the center of rotation.

SVG元素也可以使用CSS 3D变换在三维空间中变换。依然要注意坐标系，然而，不同于建立在HTML元素上的坐标系。这意味着3D旋转看起来也不同除非改变旋转中心。

	#SVGel {
	    transform: perspective(800px) rotate3d(1, 1, 0, 45deg);
	}

Because transforming SVG elements with CSS is pretty much the same as transforming HTML elements with CSS—syntax-wise—I'm going to skip elaborating on this topic in this article.

因为通过CSS来变换SVG元素非常类似于通过CSS来变换HTML元素-语法层面-在这篇文章中我将跳过这个部分。

That said, at the time of writing of this article, implementations are still incomplete in some browsers and for some features. Because of how fast browser support changes, I recommend you experiment with the properties to determine what currently works and what doesn't, and decide on what you can start using today and what not.

另外，在写这篇文章的时候，在一些浏览器中实现一些特性是不可能的。因为浏览器支持改变很快，我建议你实验一下这些属性来决定哪些可以工作哪些不可以，决定什么现在可以用什么不可以。

Note that once CSS Transforms are fully implemented for SVG elements, it is recommended that you use the CSS transforms function syntax even when you apply the transformation in the form of a `transform` attribute. That said, the above mentioned syntax of the `transform` attribute functions will still be valid.

注意一旦CSS变换可以完全实现在SVG上，我依然建议你使用CSS变换函数语法即使你用`transform`属性的形式添加变换。也就是说，上面提到的`transform`属性函数的语法还是有效的。

##Animating `transform`
##动画`transform`

SVG transformations can be animated, just like CSS `transforms` can be. If you're using the CSS transform property to transform the SVG, you can animate the transformation using CSS animations and transitions just like you would animate CSS transforms on HTML elements.

SVG变换可以变成动画，就像CSS变换一样。如果你使用CSS `transform`属性来产生SVG变换，你可以像在HTML元素上创建CSS变换动画一样使用CSS动画把这些变换变成动画。

The SVG `transform` attribute can be animated using the SVG `<animateTransform>` element. The `<animateTransform>` element is one of three elements in SVG that are used to animate different SVG attributes.

SVG`transform`属性可以用SVG`<animateTransform>`元素来做成动画。`<animateTransform>`元素是SVG中三个用来给不同的SVG属性设置动画的元素之一。

Details of the `<animateTransform>` element are outside the scope of this article. Stay tuned for an article I'll be writing about the different SVG animation elements, including `<animateTransform>`.

关于`<animateTransform>`元素的详细内容不在本片文章的讨论范围内。阅读我写的关于不同SVG动画元素的文章，包括`<animateTransform>`。

##Final Words
##最后的话

Working with SVGs can be really frustrating at first, if the concepts behind the coordinate system transformations aren't very clear, especially if you're coming from a CSS HTML transformations background, and naturally expect SVG elements to respond the same way to transformations as HTML elements do.

学习SVGs一开始可能非常困惑，如果对于坐标系变换里的内容不是很清楚，尤其是如果你带着CSS HTML变换的背景知识，自然而然希望SVG元素和HTML元素的变换一样。

However, once you get a grip of how they work, you gain a better control over your SVG canvas, and can manipulate elements more easily.

然而，一旦你意识到它们的工作方式，你能更好得控制SVG画布，并且轻易操纵元素。

In the last part of this series, I'm going to go over nesting SVGs and establishing new viewports and viewboxes. Stay tuned!

这一系列的最后部分，我将讨论嵌套SVGs和建立新的viewports和viewboxes。敬请关注！