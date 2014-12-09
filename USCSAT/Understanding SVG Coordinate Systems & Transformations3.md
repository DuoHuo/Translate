#Understanding SVG Coordinate Systems & Transformations (Part 3) – Establishing New Viewports
#理解SVG坐标系统和变化（第三部分）- 建立新视口

At any point in an SVG drawing, you can establish new viewports and user coordinate systems by either nesting `<svg>` or using elements such as the `<symbol>` element, among others. In this article we're going to have a look at how we can do that and how this can be useful for controlling SVG elements and making them more flexible (and/or fluid).

在SVG绘制的任何一个时刻，你可以通过嵌套`<svg>`或者使用例如`<symbol>`的元素来建立新的viewport和用户坐标系。在这篇文章中，我们将看一下我们如何这样做，以及这样做如何帮助我们控制SVG元素并让它们变得更加灵活（或流动）。

This is the third and last article in a series of articles about SVG coordinate systems and transformations. In the first article, I covered everything you need to know to understand the basics of SVG coordinate systems; more specifically, the SVG viewport, and the `viewBox` and `preserveAspectRatio` attributes. In the second article, you can find everything you need to know about how SVG system transformations work.

这是SVG坐标系和变换系列的第三篇也是最后一篇文章。在第一篇中，包括了任何要理解SVG坐标系统基础的需要知道的内容；更具体的是， SVG viewport, `viewBox`和 `preserveAspectRatio`属性。在第二篇文章里，你可以了解到任何你需要了解的关于SVG系统变换的内容。

* [Understanding SVG Coordinate Systems & Transformations (Part 1) – The viewport, `viewBox`, & `preserveAspectRatio`](http://sarasoueidan.com/blog/svg-coordinate-systems)
* [Understanding SVG Coordinate Systems & Transformations (Part 2) – The `transform` Attribute](http://sarasoueidan.com/blog/svg-transformations)
* Understanding SVG Coordinate Systems & Transformations (Part 3) – Establishing New Viewports

* [理解SVG坐标系和变换（第一部分）-viewport，`viewBox`，和`preserveAspectRatio`](http://sarasoueidan.com/blog/svg-coordinate-systems)
* [理解SVG坐标系和变换（第二部分）-`transform`属性](http://sarasoueidan.com/blog/svg-transformations)
* 理解SVG坐标系和变换（第三部分）-建立新视口

Throughout this article, **I'm going to assume that you read the first part of this series about SVG viewports and the `viewBox` and `preserveAspectRatio` attributes.** You don't need to have read the second one about coordinate system transformations to follow along this article.

通过这篇文章，**我假定你已经读了这个系列的第一部分关于SVG viewport, `viewBox` 和 `preserveAspectRatio` 属性的内容**。在阅读这篇文章之前你不需要读第二篇关于坐标系变换的内容。

##Nesting `<svg>` Elements
##嵌套`<svg>`元素

In the [first part](http://sarasoueidan.com/blog/svg-coordinate-systems) we talked about how the `<svg>` element establishes a viewport for the content of the SVG canvas. At any point in an SVG drawing, you can establish a new viewport into which all contained graphics is drawn by including an `<svg>` element inside another `<svg>`. By establishing a new viewport, you also implicitly establish a new viewport coordinate system and a new user coordinate system.

在[第一部分](http://sarasoueidan.com/blog/svg-coordinate-systems)我们讨论了`<svg>`元素如何为SVG画布内容建立一个视口。在SVG绘制过程中的任何一个时刻，你可以创建一个新的视口其中包含的图形是通过把一个`<svg>`元素包含在另一个中绘制的。通过建立新视口，你隐性得建立了一个新视口坐标系和新用户坐标系。

For example, suppose you have an `<svg>` and some content inside it:
例如，试想有一个`<svg>`以及里面的内容：

	<svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	    <!-- some SVG content -->
	    <svg>
	        <!-- some inner SVG content -->
	    </svg>
	<svg>

The first thing to note here is that the inner `<svg>` element does not require specifying a namespace xmlns on it because it is assumed to be the same namespace as the outer `<svg>`'s namespace. Of course, even the outer `<svg>` does not require a namespace if it is embedded inline in an HTML5 document.

第一件需要注意的是内容`<svg>`元素不需要声明一个命名空间xmlns因为默认和外层`<svg>`的命名空间相同。当然，如果在HTML5文档中外层`<svg>`也不需要命名空间。

You can use a nested SVG to group elements together and then position them inside the parent SVG. Now, you can also group elements together and position them using the`<g>` group—by wrapping elements inside a [group `<g>` element](http://sarasoueidan.com/blog/structuring-grouping-referencing-in-svg), you can position them on the canvas by [using the `transform` attribute](http://sarasoueidan.com/blog/svg-transformations). However, an `<svg>` element has certain advantages over using `<g>`. Positioning using x and y coordinates is, in most cases, more convenient than using transforms. Moreover, an `<svg>` element accepts `width` and `height` attributes, which the `<g>` element doesn't. That said, the `<svg>` may not always be needed or necessary, because it leads to the creation of a new viewport and coordinate systems, which you may not need or want.

你可以使用一个嵌套的SVG来把元素组合在一起然后在父SVG中定位它们。现在，你也可以把元素组合在一起并且使用组`<g>`来定位-通过把元素包括在[一组<g>元素](http://sarasoueidan.com/blog/structuring-grouping-referencing-in-svg)中。你可以[使用`transform`属性](http://sarasoueidan.com/blog/svg-transformations)在画布中定位它们。然而，使用`<svg>`肯定好过使用`<g>`。使用x和y坐标来定位，在许多情况下，比使用变换更加方便。另外，`<svg>`元素接受宽高值，`<g>`不行。这意味着，`<svg>`也许并必要的，因为它可以创建一个新的viewport和坐标系，你可以不需要也不想要。

By specifying a width and height to the `<svg>`, you restrict the content inside it to the bounds of the viewport that is defined by the `x`, `y`,`width`, and `height` attributes. Any content that lies beyond these bounds will be clipped.

通过给`<svg>`声明宽高值，你把内容限制在通过x,y,width和height属性定义的viewport的边界。任何超过边界的内容会被裁切。

If you don't specify `x` and `y` attributes, they're assumed to be zero. If you don't specify `height` and `width` attributes, the `<svg>` will be 100% the width and height of its parent SVG.

如果你不声明`x`和`y`属性，它们默认是0。如果你不声明`height`和`width`属性，`<svg>`会是父SVG宽度和高度的100%。

Moreover, specifying a user coordinate system other than the default one will also affect the content inside the inner `<svg>`, too.

另外，声明用户坐标系而不是默认的也会影响内部`<svg>`的内容。

Percentage values specified for elements inside the inner `<svg> `will be calculated relative to it, not relative to the outer svg. Percentage values specified on the inner itself `<svg>` will be calculated relative to the outer svg. For example, the following will result in the inner SVG being equal to 400 units, and the rectangle inside it will be 200 units:

给`<svg>`内的元素百分比值的声明会根据`<svg>`计算，而不是外层svg。例如，下面的代码会导致内层SVG等于400单位，里面的长方形是200个单位：

	<svg width="800" height="600">
	    <svg width="50%" ..>
	        <rect width="50%" ... />
	    </svg>
	</svg>

If the width of the outermost `<svg>` is set to 100% (for example, if it is embedded inline in a document and you want it to be fluid), then the inner SVG will expand and shrink as necessary to maintain a width that is half of that of the outer SVG – this is powerful.

如果最外层`<svg>`的宽度为100%（例如，如果它在一个文档中内联或者你想要它可以流动），内层SVG会扩展拉伸来保持宽度为外层SVG的一半-这是强制的。

Nested SVGs are particularly useful for adding flexibility and fluidness to elements on the SVG canvas. We know that, using `viewBox` values and `preserveAspectRatio`, we can already create responsive SVGs. The outermost `<svg>`'s with can be set to 100% to make sure it expands and shrinks as its container (or the page) grows or shrinks. Then, by using viewBox values and preserveAspectRatio, we can make sure that the SVG canvas also responds to the changes in the viewport (outermost svg). I've written about responsifying SVGs in my [CSSConf talk slides](http://sarasoueidan.com/blog/cssconf-2014-talk). You can check the technique out [here](https://docs.google.com/presentation/d/1Iuvf3saPCJepVJBDNNDSmSsA0_rwtRYehSmmSSLYFVQ/pub?start=false&loop=false&delayms=3000#slide=id.g180585666_036).

嵌套SVG在给SVG画布中的元素增加灵活性和扩展性时尤其有用。我们知道，使用`viewBox`值和`preserveAspectRatio`，我们已经可以创建响应式SVG。最外层`<svg>`的宽度可以设置成100%来确保它扩展拉伸到它的容器（或页面）扩展或拉伸。然后通过使用viewBox值和 preserveAspectRatio，我们可以保证SVG画布可以自适应viewport中的改变（最外层svg）。我在[CSSConf演讲的幻灯片](http://sarasoueidan.com/blog/cssconf-2014-talk)中写到了关于响应式SVG的内容。你可以在[这里](https://docs.google.com/presentation/d/1Iuvf3saPCJepVJBDNNDSmSsA0_rwtRYehSmmSSLYFVQ/pub?start=false&loop=false&delayms=3000#slide=id.g180585666_036)查看这个技术。

However, when we do responsify an SVG like that, the entire canvas with all the elements drawn on it will respond and change simultaneously. But sometimes, you may want to have only one element inside the graphic to be flexible, while keeping others "fixed" in position and/or size. This is where nested `svg`S can be useful.

然而，当我们像这样创建一个响应式SVG，整个画布以及所有绘制在上面的元素都会有反应并且同时改变。但有时候，你只想让图形中的一个元素变为响应式，并且保持其他东西“固定”在一个位置和/或尺寸。这时候嵌套`svg`就很有用。

An `svg` element can have its own coordinate system independent of its parent, and it can have its own `viewBox` and `preserveAspectRatio` attributes that allow you to size and position the content inside it any way you want.

`svg`元素有独立于它父元素的坐标系，它可以有独立的`viewBox`和`preserveAspectRatio`属性，你可以任意修改里面内容的尺寸和位置。

So, in order to make one element flexible, we can wrap it in an `<svg>` element, and give that `svg` a flexible width so that it adjusts to the width of the outermost SVG, and then specify `preserveAspectRatio="none"` so that the graphic inside it also stretches and shrinks with the container width. *Note that `svg`s can be nested to many levels, but in order to keep things simple, I'm nesting only one level deep in this article.*

所以，要让一个元素更加灵活，我们可以把它包裹在`<svg>`元素中，并且给`svg`一个弹性的宽度来适应最外层SVG的宽度，然后声明`preserveAspectRatio="none"`这样的话里面的图形会扩展和拉伸到容器的宽度。*注意`svg`可以多层嵌套，但是为了让事情简洁，我在这篇文章里只嵌套一层深度。*

To demonstrate how nested `svg`s can be useful, let's look at some examples.

为了演示嵌套`svg`如何发挥作用，让我们来看一些例子。

####Example

####例子

Suppose we have the following SVG:

试想我们有如下的SVG：

![](svg/svg-nesting-example-1.png)

The above SVG is responsive. Resizing the screen will result in the entire SVG graphic responding as necessary. The following screenshot shows the result of shrinking the page, and how the SVG becomes smaller. Notice how **the contents of the SVG maintain all their initial positions with respect to the SVG viewport and with respect to each other.**

上述SVG是响应式的。改变屏幕的尺寸会导致整个SVG图形根据需要做出反应。下面的截图展示了拉伸页面的结果，以及SVG如何变得更小。注意**SVG的内容如何根据SVG视口和相互之间保持它们的初始位置。**

![](svg/svg-nesting-example-1-resized.png)

Using nested SVGs, we're going to change that. We can specify a position for individual elements inside the SVG relative to the SVG's viewport, so that as the SVG viewport size changes (i.e the size of the outermost `svg` changes), the elements respond independently of each other.

使用嵌套SVG，我们将改变这个情况。我们可以对SVG中每个独立的元素根据SVG视口声明一个位置，所以随着SVG 视口尺寸的改变（即最外层`svg`的改变），每个元素独立于其他元素发生改变。

*Note that, at this point, it is necessary that you be familiar with how the SVG viewport, `viewBox`, and `preserveAspectRatio` work.*

*注意，在这个时候，你需要熟悉SVG viewport, `viewBox`, 和`preserveAspectRatio`是如何生效的。*

We're going to create an effect such that, when the screen is resized, the upper part of the egg is going to be moved so that the cute chicken inside it peeks out, as shown in the following image:

我们将要创建一个效果，当屏幕尺寸变化时，蛋壳的上部分移动使得其中的可爱的小鸡显示出来，如下图所示：

![](svg/svg-nesting-example-1-new.png)

In order to get that effect, the egg's upper part has to be separated from the rest by wrapping it inside an `svg` of its own. This `svg` wrapper will get an ID `upper-shell`.

为了达到这个效果，蛋的上半部分必须和其他部分分离出来单独包含一个自己的`svg`。这个`svg`包含框会有一个ID`upper-shell`。

Then, we're going to make sure the new `svg#upper-shell` has the same height and width as the outer SVG. This can be achieved by either specifying `width="100%"` `height="100%"` on the `svg`, or by not specifying any height and width at all. If no width and height are specified on the inner SVG, it automatically expands to 100% the width and height of the outer SVG.

然后，我们保证新的`svg#upper-shell`和外层SVG有一样的高度和宽度。可以通过在`svg`上声明`width="100%"` `height="100%"`或者不声明任何高度和宽度来实现。如果内层SVG上没有声明任何宽高，它会自动扩展为外层SVG宽高的100%。

And finally, to make sure the upper shell is "lifted" up or positioned at the top center of the `svg#upper-shell`, we're going to use the appropriate `preserveAspectRatio` value which makes sure the viewBox is positioned at the top center of the viewport—the value is `xMidYMin`.

最终，为了确保上壳被“抬”起或定位在`svg#upper-shell`顶部的中心，我们将使用适当的`preserveAspectRatio`值来确保viewBox被定位在视口的顶部中心-值是`xMidYMin`。

The code for the SVG graphic becomes:

SVG图形的代码如下：

	<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	    <!-- ... -->
	    <svg viewBox="0 0 315 385" preserveAspectRatio="xMidYMid meet">
	        <!-- the chicken illustration -->
	        <g id="chicken">
	            <!-- ... -->
	        </g>
	        <!-- path forming the lower shell -->
	        <path id="lower-shell" fill="url(#gradient)" stroke="#000000" stroke-width="1.5003" d="..."/>
	    </svg>

	    <svg id="upper-shell" viewBox="0 0 315 385" preserveAspectRatio="xMidYMin meet">
	        <!-- path forming the upper shell -->
	        <path id="the-upper-shell" fill="url(#gradient)" stroke="#000000" stroke-width="1.5003" d="..."/>
	    </svg>
	</svg>

At this point, note that the `viewBox` specified on the nested `svg#upper-shell` has the same value as that of the outermost `svg` (before it was removed). The reason we used the same `viewBox` value is so that, the SVG maintains its original look on big screens.

这个时候，注意在嵌套`svg#upper-shell`上声明的`viewBox`和最外层`svg`有相同的值（在它被移除之前）。我们用相同的`viewBox`值我原因就是这样，SVG在大屏幕上保持最初的样子。

So, the way this goes is: we start with an SVG—in our case, it's the image of a cracked egg with a chicken hidden inside it. Then, we create another "layer" and promote the upper shell to it—this layer is created by using a nested `svg`. The nested `svg` has the same dimensions as the outer `svg` and the same `viewBox`. And finally, the viewBox of the inner SVG is set to "stick" to the top of the viewport no matter what the screen size is—this makes sure that, when the screen size is narrow and the SVG is elongated, the upper shell will be lifted upwards, thus showing the chicken "behind" it on the canvas.

所以，这件事是这样的：我们开始一个SVG-在我们的例子中，这是一张里面藏着一个小鸡的带裂纹的蛋。然后，我们创建了另一“层”并把上部分的壳放在里面-这一层通过使用嵌套`svg`创建。嵌套`svg`和外层`svg`的尺寸和`viewBox`一样。最终，内层SVG的viewBox被设置成不管屏幕尺寸是多少都“固定”在viewport的顶部-这确保了当屏幕尺寸很窄时SVG被拉长，上层的壳被向上举起，因此展示出“隐藏”在里面的小鸡。

![](svg/svg-nesting-example-1-layered.png)

Once the screen size shrinks, the SVG is elongated, and the viewBox containing the upper shell is positioned at the top of the viewport using `preserveAspectratio="xMidYMin meet"`.

一旦屏幕尺寸拉伸，SVG被拉长，使用`preserveAspectratio="xMidYMin meet"`把包含上部分壳的viewBox被定位到viewport的顶部。

![](svg/svg-nesting-example-1-viewbox.png)

Click on the following button to see the live SVG. Remember to resize your browser to see the SVG adapt.

点击下面按钮来查看在线SVG。记住改变屏幕尺寸再看SVG变化。

<a href="/images/svg-nesting-chick.svg" class="button">View Live Example</a>

Nesting or "layering" SVGs allows you to position parts of the SVG relative to the changing viewport, while maintaining the elements' aspect ratio. So the image adapts without distorting the elements inside it.

嵌套或"分层"SVG使你可以根据改变的视口定位SVG的一部分，在保持元素宽高比的情况下。所以图片可以在不扭曲内容元素的情况下自适应。

If we wanted the entire egg to come off the chicken, we could always wrap the lower shell in an `svg` layer of its own, having the same `viewBox`, too. Then, to make sure the lower shell moves down and sticks to the bottom center of the viewport, we position it using `preserveAspectRatio="xMidYMax meet"`. The code would look like this:

如果我们想要整个鸡蛋剥离显示出小鸡，我们可以单独用一个`svg`层包含下部分壳，`viewBox`也相同。确保下部分壳向下移动并固定在视口的底部中心，我们使用`preserveAspectRatio="xMidYMax meet"`来定位。代码如下：

	<svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
	    <svg id="chick" viewBox="0 0 315 385" preserveAspectRatio="xMidYMid meet">
	        <!-- the chicken illustration -->
	        <g id="chick">
	            <!-- ... -->
	        </g>
	    </svg>

	    <svg id="upper-shell" viewBox="0 0 315 385" preserveAspectRatio="xMidYMid meet">
	        <!-- path forming the upper shell -->
	        <path id="the-upper-shell" fill="url(#gradient)" stroke="#000000" stroke-width="1.5003" d="..."/>
	    </svg>

	    <svg id="lower-shell" viewBox="0 0 315 385" preserveAspectRatio="xMidYMax meet">
	        <!-- path forming the lower shell -->
	        <path id="the-lower-shell" fill="url(#gradient)" stroke="#000000" stroke-width="1.5003" d="..."/>
	    </svg>
	</svg>

Each of the `svg` layers/viewports is equal to 100% the width and height of the outermost `svg`. So we basically have three clones. Each layer contains an element—the upper shell, the lower shell, or the chick. The `viewBox` for the three layers is the same, with only the `preserveAspectRatio` being different.

每个`svg`层/viewport等于最外层`svg`宽高的100%。所以我们基本有了三个副本。每层包含一个元素-上部分壳，下部分壳，或小鸡。三层的`viewBox`是相同的，只有`preserveAspectRatio`不同。

![](svg/svg-nesting-example-1-2.png)

Of course, in this example I started with a graphic of a chicken hiding inside an egg, and that is revealed when the screen becomes smaller. However, you could do something different: you could start with a graphic on a small screen, that then reveals something new as the screen becomes bigger; i.e as the `svg` becomes wider and there is more horizontal space to show elements.

当然，在这个例子里，一开始的图形中小鸡隐藏在蛋里，随着屏幕变小才显示出来。然而，你可以做一些不一样的：你可以开始在小屏幕上创建一个图形，然后在大屏幕上显示一些东西；即当`svg`变宽时才有更多垂直空间来展示元素。

You could get a lot more creative, and show and hide elements according to different screen sizes—using media queries—and have the new elements be positioned in a certain way to achieve a certain effect. The sky is the limit here.

你可以更有创造性，根据不同屏幕尺寸来显示和隐藏元素-使用媒体查询-把新元素通过特定方式定位来达到特定的效果。想象力是无穷的。

Also note that the nested `svg`s don't need to have the same height and width as their containing `svg`; you can specify a height and width and have the content of the `svg` be limited to and clipped by the boundaries specified by that height and width—it all boils down to what you're trying to achieve.

同时注意嵌套`svg`不需要和容器`svg`有相同的宽高；你可以声明宽高并且限制`svg`内容，超出边界裁切-这都取决于你想要达到什么效果。

###Making Elements Fluid Using Nested SVGs
###使用嵌套SVG使元素流动

In addition to positioning elements while preserving their aspect ratios, we can use nested `svg`s allow only certain elements to be fluid—this can be done by not preserving the aspect ratio of these particular elements.

在保持宽高比的情况下定位元素，我们可以使用嵌套`svg`只允许特定元素流动-可以不保持这些特定元素的宽高比。

For example, if you want only one element in the SVG to be fluid, you can wrap it in an `svg`, and use `preserveAspectRatio="none"` to have that element expand to fill the entire width of the viewport at all times, while maintaining the aspect ratio and positioning of other elements like we did in the previous example.

例如，如果你只想SVG中的一个元素流动，你可以把它包含在一个`svg`中，并且使用`preserveAspectRatio="none"`来让这个元素扩展始终撑满这个视口的宽，并且保持宽高比和像我们在之前例子中做的一样定位其他元素。

	<svg>
	    <!-- ... -->
	    <svg viewBox=".." preserveAspectRatio="none">
	        <!-- this content will be fluid -->
	    </svg>
	    <svg viewBox=".." preserveAspectRatio="..">
	        <!-- content positioned somewhere in the viewport -->
	    </svg>
	    <!-- ... -->
	</svg>

[Jake Archibald](http://jakearchibald.com/) created a simple and practical use case for nested SVGs that does exactly that: a simple UI that contains elements positioned at the corners of the outermost `svg`, maintaining their aspect ratios, and a middle part of the UI is fluid and responds to the change in the svg width by shrinking and expanding with it. You can check his demo out [here](https://jsbin.com/loceqo/1). Make sure you inspect the code in the dev tools to select and visualize the different viewboxes and svgs used.

[Jake Archibald](http://jakearchibald.com/)创建了一个简单实用的嵌套SVG使用案例：一个简单的UI可以包含定位在最外层`svg`角落的元素，并且保持宽高比，UI的中间部分浮动并且根据svg宽度改变进行拉伸。你可以在[这里](https://jsbin.com/loceqo/1)查看。确保你在开发工具里检查代码来选取和想象不同viewbox和svg使用的效果。

##Other Ways To Establish New Viewports
##其他建立新视口的方法

`svg` elements are not the only elements that establish new viewports in SVG. In the following sections, we're going to go over the other ways to establish new viewports using other SVG elements.

`svg`不是唯一能在SVG中创建新视口的元素。在下面部分，我们会讨论使用其他SVG元素创建新视口的方法。

###Establishing a new viewport by `<use>`ing `<symbol>`
###使用`<use>`ing `<symbol>`建立一个新的视口

The `symbol` element defines a new viewport whenever it is instantiated by the `use `element.

`symbol`元素会定义新视口，无论它什么时候被`use`元素实例化。

A `symbol` element can be used by referencing it in the `xlink:href` attribute of the `use` element:

`symbol`元素的使用可以参考`use`元素中的`xlink:href`属性：

	<svg>
	    <symbol id="my-symbol" viewBox="0 0 300 200">
	        <!-- contents of the symbol -->
	        <!-- this content is only rendered when `use`d -->
	    </symbol>
	    <use xlink:href="#my-symbol" x="?" y="?" width="?" height="?">
	</svg>

The question marks used as values above are used only to indicate that these values may or may not be specified—if `x` and `y` are not specified, they default to zero, and you don't need to specify a height and width either.

上面值中的问号表示这些值也许没有声明-如果`x`和`y`没有声明，默认值为0，也不需要声明宽高。

You see, when you `use` a `symbol `element, and then inspect the DOM using the dev tools, you will not see the contents of the symbol inside the use tag. The reason for this is that the contents of use are rendered into a shadow tree, which you can inspect if you enable inspecting the shadow DOM in the dev tools.

看到了吧，当你`use`一个`symbol`元素，然后使用开发工具检查DOM，你不会看到`use`标签中`symbol`的内容。因为use的内容在shadow tree里被渲染，如果你在开发工具中允许shadow DOM显示你就能看到。

When the `symbol` is used, it is deeply cloned into the generated shadow tree, with the exception that the `symbol` is replaced by an `svg`. This generated `svg` will always have explicit values for attributes `width` and `height`. If attributes `width` and/or `height` are provided on the `use` element, then these attributes will be transferred to the generated `svg`. If attributes `width` and/or `height` are not specified, the generated `svg` element will use values of 100% for these attributes.

当`symbol`被使用时，它被深度克隆到生成的shadow tree中，例外是`symbol`被`svg`替换。这个生成的`svg`总是有明确的宽高。如果宽高的值在`use`元素上，这些值会被转换生成`svg`。如果属性宽和/或高没有声明，生成的`svg`元素会使用这些值的100%。

Because we end up with an `svg` in the DOM, and because this `svg` is practically contained in the outer `svg` where `use` is used, we're left with a nested `svg` situation not very different from the one we talked about in the previous section—the nested `svg` forms a new viewport. The `viewBox` for the nested `svg` is the `viewBox` specified on the `symbol` element. (*The `symbol` element accepts a `viewBox` attribute value. For more information, refer to the article: [Structuring, Grouping, and Referencing in SVG – The <g>, <use>, <defs> and <symbol> Elements](http://sarasoueidan.com/blog/structuring-grouping-referencing-in-svg/)*).

因为我们在DOM中使用了`svg`，并且因为这个`svg`实际上包含在外层`svg`中，我们遇到的嵌套`svg`的状况和我们在之前一章讨论到的并没有多少不一样-嵌套的`svg`形成了一个新的`viewport`。嵌套`svg`的`viewBox`是在`symbol`元素上声明的`viewBox`。（`symbol`元素接受`viewBox`元素值。更多信息，阅读这篇文章：[Structuring, Grouping, and Referencing in SVG – The <g>, <use>, <defs> and <symbol> Elements](http://sarasoueidan.com/blog/structuring-grouping-referencing-in-svg/))

So we now have a new viewport whose dimensions and position can be specified in the `use` element (`x`, `y`, `width`, `height`), and whose `viewBox` value can also be specified in the `symbol` element. The content of the `symbol` is then rendered and positioned inside this viewport and viewBox.

所以我们现在有了一个新的viewport，尺寸和位置可以使用元素（`x`,` y`, `width`, `height`）声明，`viewBox`值可以在`symbol`元素上声明。`symbol`的内容随后再这个视口和viewBox中被渲染和定位。

And last but not least, the `symbol` element also accepts a `preserveAspectratio` attribute value, that allows you to position the `viewBox` inside the new viewport established by `use`. Pretty neat, right? You can control the newly created nested `svg` just like we did in the previous sections.

最后，`symbol`元素也接收`preserveAspectratio`属性值，你可以在由`use`建立的新视口中定位`viewBox`。这很清楚，不是吗？你可以像我们在之前的部分里一样控制新创建的嵌套`svg`。

[Dirk Weber](http://eleqtriq.com/) has also created a demo that uses nested SVGs and `symbol` elements to mimic the behavior of CSS border images. You can check his article out [here](http://w3.eleqtriq.com/2014/02/the-4-slice-scaling-technique-for-svg/).

[Dirk Weber](http://eleqtriq.com/) 也创建了一个使用嵌套SVG和`symbol`元素来模仿CSS border images的表现。你可以在[这里](http://w3.eleqtriq.com/2014/02/the-4-slice-scaling-technique-for-svg/)查看文章。

###Establishing a new viewport by referencing an SVG image in `<image>`
###参考`<image>`中的SVG image建立一个新视口

The `image` element indicates that the contents of a complete file are to be rendered into a given rectangle within the current user coordinate system. The `image` element can refer to raster image files such as PNG or JPEG or to files with MIME type of "image/svg+xml".

`images`元素表明整个文件的内容被渲染到一个当前用户坐标系中给定的长方形。`image`元素可以代表图片文件例如PNG或JPEG或者有"image/svg+xml"的MIME类型的文件。

An `image` element that references an SVG file will result in the establishment of a temporary new viewport since the referenced resource by definition will have an `svg` element.

代表SVG文件的`image`元素会导致建立一个临时新视口因为定义相关资源有`svg`元素。

	<image xlink:href="myGraphic.svg" x="?" y="?" width="?" height="?" preserveAspectRatio="?" />

The `<image>` element accepts many attributes, some of these attributes—the ones that are relevant to this article—are `x` and `y` position attributes, `width` and `height` attributes, and `preserveAspectratio`.

`<image>`元素接收许多属性，其中一些属性-和这篇文章有关的-是`x`和`y`位置属性，`width`和`height`属性以及`preserveAspectratio`。

Normally, an SVG file will contain a root `<svg>` element; this element may or may not have position and dimensions specified, in addition to a `viewBox` and a `preserveAspectratio` value.

通常，SVG文件会包含一个根`<svg>`元素；这个元素也许声明位置和尺寸，另外也许有`viewBox`和`preserveAspectratio`值。

When an `image` element references an SVG image file, the `x`, `y`, `width` and `height` attributes on the root `svg` are ignored. Unless the value of `preserveAspectRatio` on the `image` element starts with 'defer', the `preserveAspectRatio` attribute on the root element in the referenced SVG image is also ignored. Instead, the `preserveAspectRatio` attribute on the referencing `image` element defines how the SVG image content is fitted into the viewport.

当一个`image`元素代表SVG图片文件，根svg的`x`，`y`，`width`和`height`属性被忽略。除非`image`元素上的`preserveAspectRatio`值以“defer”开头，根元素上的`preserveAspectRatio`值在代表SVG图片时也被忽略。然而相关`image`元素上的`preserveAspectRatio`属性定义SVG图片内容如何适应视口。

The value of the `viewBox` attribute to use when evaluating the `preserveAspectRatio` attribute is defined by the referenced content. For content that clearly identifies a viewBox (e.g. an SVG file with the `viewBox` attribute on the outermost svg element) that value should be used. For most raster content (PNG, JPEG) the bounds of the image should be used (i.e. the `image` element has an implicit `viewBox` of '0 0 raster-image-width raster-image-height'). Where no value is readily available (e.g. an SVG file with no `viewBox` attribute on the outermost svg element) the `preserveAspectRatio` attribute is ignored, and only the translation due to the `x` & `y` attributes of the viewport is used to display the content.

评估被参考内容定义的`preserveAspectRatio`属性时使用`viewBox`属性值。对于明确定义的viewBox内容（例如，最外层元素上有`viewBox`属性的SVG文件）值应该被使用。对于大多数值（PING,JPEG），图片边界应该被使用（即`image`元素有隐含的尺寸为'0 0 raster-image-width raster-image-height'的`viewBox`）。如果值不全的话（例如，外层的svg元素没有`viewbox`属性的SVG文件）`preserveAspectRatio`值被忽略，只有视口`x`&`y`属性引起的移动才用来显示内容。

For example, if the image element referenced a PNG or JPEG and `preserveAspectRatio="xMinYMin meet"`, then the aspect ratio of the raster would be preserved, the raster would be sized as large as possible while ensuring that the entire raster fits within the viewport, and the top/left of the raster would be aligned with the top/left of the viewport as defined by the attributes `x`, `y`, `width` and `height` on the `image` element.

例如，如果一个image元素代表PNG或JPEG并且`preserveAspectRatio="xMinYMin meet"`，那么栅格的宽高比会保持，栅格会在保证整个栅格适应视口的情况下尽可能放大尺寸，栅格的左上角会和由`image`元素上`x`,`y`,`width`和`height`定义的视口的左上角对齐。

If the value of `preserveAspectRatio` was 'none' then aspect ratio of the image would not be preserved. The image would be fitted such that the top/left corner of the raster exactly aligns with coordinate (`x`, `y`) and the bottom/right corner of the raster exactly aligns with coordinate (`x`+`width`, `y`+`height`).

如果`preserveAspectRatio`的值是“none”那么图片的宽高比不会保持不变。图片会自适应，栅格的左上角和坐标系（`x`,`y`）完全对齐，栅格的右下角和坐标系(`x`+`width`, `y`+`height`)完全对齐。

###Establishing a new viewport using `<iframe>`
###使用`<iframe>`建立新视口

An `iframe` element that references an SVG file establishes new viewport similar to the situation of `image` element explained above. An `iframe` element can also have `x`, `y`, `width`, and `height` attributes, in addition to its own `preserveAspectratio`.

代表SVG文件的`iframe`元素建立新坐标系的情况类似于上述解释的`image`元素的情况。`iframe`元素也可以有`x`,`y`,`width`和`height`属性，除了它自身的`preserveAspectratio`之外。

###Establishing a new viewport using `<foreignObject>`
###使用`<foreignObject>`建立新视口

A `foreignObject` element creates a new viewport for rendering the content that is within the element.

`foreignObject`元素建立一个新的viewport来渲染这个元素的内容。

The `foreignObject` tag allows you to add non-SVG content into an SVG file. Usually, the contents of foreignObject are assumed to be from a different namespace. For example, you could drop some HTML in the middle of an SVG element.

`foreignObject`标签允许你把非SVG内容添加到SVG文件中。通常，foreignObject的内容被认为不同于命名空间。例如，你可以把一些HTML放到SVG元素的中间。

The `foreignObject` element accepts attributes, among which are `x`, `y`, `height`, and `width`, which are used to position the object and size it, creating the bounds used to render the contents referenced inside it.

`foreignObject`接收属性包括`x`，`y`，`height`和`width`，用来定位对象和调整尺寸，创建用于呈现它里面所引用的内容的范围。

There is a lot to say about the `foreignObject` element besides its creation of a new viewport for its content. If you're interested, you can check the [MDN entry](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/foreignObject) or check [this practical use case](http://thenittygritty.co/css-masking) by [Christian Schaeffer](http://twitter.com/derschepp) on [The Nitty Gritty Blog](http://thenittygritty.co/).

有需要关于`foreignObject`元素的要说因为它给内容创建了新的viewport。如果你感兴趣，可以查看[MDN entry](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/foreignObject)或者在[The Nitty Gritty Blog](http://thenittygritty.co/)上查看[Christian Schaeffer](http://twitter.com/derschepp)创建的[实际使用例子](http://thenittygritty.co/css-masking)。

##Wrapping Up
##结束语

Establishing new viewports and coordinate systems—be that by nesting `svgs` or another element from the ones mentioned above—allows you to control parts of the SVG that you would otherwise not be able to control the same way.

建立新的viewports和坐标系-像上述提到的一样通过嵌套`svg`和其他元素-允许你控制SVG的部分内容而通过其他方式你可能没法一样控制。

The entire time that I was working on this article and thinking of demos and use cases, all I kept thinking of is how nesting SVGs can give us finer control and flexibility for when we're dealing with SVGs. Adaptive SVGs can be created with neat effects, fluid elements inside SVGs that are independent of the other elements on the page are possible, mimicing CSS border images for crispier backgrounds on high-resolution screens, and so much more.

在写这片文章以及思考例子和使用情况的整个过程中，我一直在思考嵌套SVG如何让我们在处理SVG时能更好控制并有更灵活的方式。自适应SVG可以通过简洁的代码创建，在SVG中可以创建独立于其他元素的流动元素，用来模拟CSS border images来在高分屏上定义背景。

Have you created any interesting examples using nested viewports in SVG? Can you think of more creative examples?
你是否已经在SVG中使用嵌套视口来创建有趣的例子了呢？你能否相处更多有创意的例子呢？

This article concludes the series of "Understanding SVG Coordinate Systems & Transformations". Next up, we'll be diving into animations, and more! Stay tuned, and thank you for reading!

这篇文章总结了“理解SVG坐标系和变换”这个系列。下一步，我们会讨论动画，甚至更多！敬请期待，感谢你的阅读！