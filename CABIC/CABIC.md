##Compositing And Blending In CSS
##CSS中的拼接与混合

If you're a designer, then you've probably already come across blending effects some time or the other. Blending is one of the most frequently used effects in graphic and print design. You can add texture to text by blending it with its textured backdrop, create an illusion of merged images by blending these images together, and create a wide range of colorful effects that would not be possible without that fine level of color blending control.

如果你是一个设计师，你很可能已经遇到或者总有一天会遇到混合效果。混合在图形和印刷设计方面是使用最频繁的效果之一。你可以通过混合文字和纹理背景来给文字添加纹理，通过把图片混合营造出图片融合的错觉，并创造出广泛而丰富多彩的效果，如果对混色控制没有达到如此精细的程度是不可能创造出这些效果的。

![](blending-examples.png)

Graphics editors such as Photoshop or Illustrator come with a set of blending modes. **Blend modes** allow you to specify how you want your elements to blend together, thus changing the colors of the area where these elements intersect. Each mode uses a specific color formula to mix the colors of the source and the destination.

图形编辑器例如Photoshop或Illustrator自带了一系列混合模式。**混合模式**让你可以指定混合的元素，从而改变元素交叉区域的颜色。每个模式使用特定颜色公式来混合基色和目标色。

Different modes give different end results. Before we talk about the different blend modes, and since we mentioned the **source** and **destination** elements, let's have a quick look at the concept of compositing, and how it is related to blending in CSS.

不同的模式产生不同最终结果。在我们讨论不同混合模式前，既然我们提到了**源**和**目标**元素，让我们快速的了解一下合成的概念，以及它和CSS中的混合有什么关系。

###What Is Compositing?
###合成是什么？

Compositing is the combining of a graphic element with its backdrop.

合成是图形元素与背景结合。

A **backdrop** is **the content behind the element** and is what the element is composited with.

**背景**是**元素后面的内容**并且也是元素与之合成的内容。

![](backdrop.png)

Compositing defines how what you want to draw will be blended with what is already drawn on the canvas. The source is what you want to draw, and the destination is what is already drawn (the backdrop).

合成定义了你将要绘制的元素会如何与画布上已经绘制的元素混合。源元素是你想要绘制的元素，目标元素是已经绘制的元素（背景）。

So, if you have two elements, and these elements overlap, you can think of the element on top as being the source, and the parts of the element behind that lie beneath it, will be the destination.

所以，如果你有两个元素，这些元素重叠在一起，你可以把位于上层的元素当做源元素，另一个元素位于它下层的部分是目标元素。

Using different composite operations (there are 16 operations), you can specify which parts of the two overlapping elements will be drawn, and which will not.

使用不同的混合操作（共有16种），你可以指定两个重叠元素的哪些部分被绘制，哪些不绘制。


![](porter-duff.png)

These composite operations are known as **Porter Duff compositing operations**. These operations specify what portions of the source and destination will be drawn, and blend modes specify how how the colors from the graphic element (source) and the backdrop (destination) interact. The illustrations in the above image are from the Compositing and Blending spec. In HTML5 Canvas context, these oprations are specified using the `globalCompositeOperation` property, and can be used to clip backgrounds to specific shapes, such as text, thus creating the effect of texture-filled text in Canvas. I have written about this process in [this article](http://tympanus.net/codrops/2013/12/02/techniques-for-creating-textured-text/) over at Codrops.

这些混合操作叫做**Porter Duff混合操作**。这些操作指定源和目标的哪些部分被绘制，混合模式指定图形元素（源）上的颜色如何与背景（目标）混合。上面图片中的插图来自合成和混合规范。在HTML5 Canvas的背景中，这些操作通过`globalCompositeOperation`属性指定，可以用来把背景裁切成特定图形，例如文字，从而在画布上创建纹理填充文本的效果。我已经在Codrops上的[这篇文章](http://tympanus.net/codrops/2013/12/02/techniques-for-creating-textured-text/)中提到了这个过程。

Together, Porter Duff Compositing and blending form the overall compositing operation for intersecting elements. According to the specification, “typically, the blending step is performed first, followed by the Porter-Duff compositing step. In the blending step, the resultant color from the mix of the element and the the backdrop is calculated. The graphic element’s color is replaced with this resultant color. The graphic element is then composited with the backdrop using the specified compositing operator.”

总之，Porter Duff合成和混合是对于交叉元素的总体合成操作。根据规范，“通常，首先进行混合步骤，然后进行Porter-Duff合成步骤。在混合步骤中，会计算混合元素的合成色以及背景。图形元素的颜色被合成色替代。图形元素随后使用指定合成操作与背景合成。”

Therefore, the way two intersecting or overlapping elements are handled is by blending their colors based on a blend mode, and then drawing only the parts specified by the composite operation.

因此，处理两个相交或重叠的元素的方法是基于一个混合模式混合颜色，然后只绘制合成操作指定的部分。

In CSS, we have no way to specify a composite operation. The default composite operation used is source-over. Both the source and the destination elements remain, and the area where they intersect is blended using the blend mode specified.

在CSS中，没有办法指定合成操作。默认使用的合成操作是源元素-覆盖。源元素和目标元素都保留，使用指定混合模式混合它们重叠的区域。

Before the [Compositing and Blending specification](http://www.w3.org/TR/compositing-1/) was introduced, CSS allowed one type of composite operations: simple alpha compositing. This is what the `opacity` property is for. By changing an element's opacity, the browser makes it translucent so that the colors of its backdrop can show through.

在[合成和混合规则](Compositing and Blending specification](http://www.w3.org/TR/compositing-1/)提出前，CSS只有一种合成操作：简单alpha合成。这是`opacity`属性的作用。改变元素的不透明度，浏览器中元素变透明从而使背景显示出来。

Today, two main properties exist that allow us to blend elements and backround images by specifying one of 16 available blend modes. These two properties are `background-blend-mode` and `mix-blend-mode`. Let's get to know each.

如今，已经有两个主要的属性让我们可以指定16种可用混合模式的一种来混合元素和背景图片。这两个属性是 `background-blend-mode`和`mix-blend-mode`。让我们都来了解一下。

###Blending Background Layers: The `Background-Blend-Mode` Property
###混合背景层：`Background-Blend-Mode`属性

The `background-blend-mode` property, as its name suggests, is used to specify a blend mode for an element's background layer. A background layer can be an image, or the background color.

`background-blend-mode`属性，像名字一样，用来给元素背景层指定一个混合模式。背景层可以是图片，或背景色。

In other words, `background-blend-mode` allows you to blend together an element's background image with the images and/or background color behind it.

换句话说，`background-blend-mode`允许你把元素的背景图片和它背后的图片和/或背景色混合在一起。

If the element has more than one background image, you can specify multiple blend modes—each blend mode will be used for a background image such that the first blend mode in the list corresponds to the first background image in the list of background images, and so on.

如何这个元素有超过一张的背景图，你可以指定多个混合模式-每个混合模式用在一个背景图上并且列表上的第一个混合模式对应背景图列表中的第一张背景图，以此类推。

Then, each background layer is blended with the element’s background layer that is below it and the element’s background color. Which means that, if you have two background images and a background color:

随后，背景层与元素的背景层以及元素的背景色混合。意味着，如果你有两张背景图和一个背景色：

```
	background-image: url(first-image.png), url(second-image.png);
	background-color: orange;
	background-blend-mode: screen, multiply;
```

The `second-image.png` background will blend with the background color using the `multiply` mode, and then the `first-image.png` background will blend with the second image and the background color using the `screen` blend mode. (Reminder: the first background image in the list is the one on top, and the ones following it are beneath it.)

背景图`second-image.png`会使用`multiply`模式和背景色混合，背景图`first-image.png`会使用`screen`模式和第二张图片以及背景色混合。（提示：第一张背景图位于上层，随后一张位于下层。）

Note that an element's background layers must not blend with the content that is behind the element, instead they must act as if they are rendered into an **isolated group**.

注意元素的背景层不能和元素后面的内容混合，它们必须表现得被渲染成一个**隔离组**。

Also note that if the `background` shorthand is used, the `background-blend-mode` property for that element must be reset to its initial value.

还要注意如果使用了`background`的速记形式，这个元素的`background-blend-mode`属性必须重置成初始值。

###The Blend Modes
###混合模式

Okay so we've established that each background layer can get its own blend mode which specifies how it blends with the layers beneath it. But what blend mode options do we have?

既然每个背景层可以指定混合模型来与它下面的层混合。但是我们可以用哪些混合模式选项呢？

There are 16 blend modes available in CSS: `normal` (which is the default blend mode and means that no blending is applied), `multiply`, `screen`, `overlay`, `darken`, `lighten`, `color-dodge`, `color-burn`, `hard-light`, `soft-light`, `difference`, `exclusion`, `hue`, `saturation`, `color` and `luminosity`.

CSS里有16中可用的混合模式：`normal` (默认混合模式代表没有添加混合模式), `multiply`, `screen`, `overlay`, `darken`, `lighten`, `color-dodge`, `color-burn`, `hard-light`, `soft-light`, `difference`, `exclusion`, `hue`, `saturation`, `color` 和 `luminosity`。

Each filter, when applied to an image, for example, will give a different end result—the colors of the image are going to be changed based on the mode you choose.

例如，每个滤镜应用在图片上时，会产生不同的最终结果-图片的颜色为会根据你选择的模式变化。

`normal`

`正常模式`

This is the default mode which specifies no blending. The blending formula simply selects the source 
color.

默认模式指定没有混合。混合公式简单得选择基色。

`multiply`

`正片叠底模式`

The source color is multiplied by the destination color and replaces the destination. The resultant color is always at least as dark as either the source or destination color. **Multiplying any color with black results in black. Multiplying any color with white preserves the original color.**

基色和目标色复合后替换目标色。合成色至少与基色或目标色一样深。**任何颜色与黑色复合得到黑色。任何颜色与白色复合保持初始颜色。**

`screen`

`滤色模式`

Multiplies the complements of the backdrop and source color values, then complements the result. The result color is always at least as light as either of the two constituent colors. **Screening any color with white produces white; screening with black leaves the original color unchanged.** The effect is similar to projecting multiple photographic slides simultaneously onto a single screen.

把背景色的互补色与基色混合，取结果的互补色。合成色至少和两个构成色一样浅。**任何颜色与白色滤色产生白色；和黑色滤色颜色不变。**效果类似于在一个屏幕上投影多个幻灯片。

`overlay`

`叠加模式`

Multiplies or screens the colors, depending on the backdrop color value. Source colors overlay the backdrop while preserving its highlights and shadows. The backdrop color is not replaced but is mixed with the source color to reflect the lightness or darkness of the backdrop.

对颜色正片叠底或滤色依赖于背景色值。基色覆盖背景同时保留高光和阴影。背景色没有被替换但是与基色混合来反映背景的亮暗。

`darken`

`变暗模式`

Selects the darker of the backdrop and source colors. The backdrop is replaced with the source where the source is darker; otherwise, it is left unchanged.

选择背景和基色的较暗部分。背景被基色中较暗的部分替换；否则，保持不变。

`lighten`

`变亮模式`

Selects the lighter of the backdrop and source colors. The backdrop is replaced with the source where the source is lighter; otherwise, it is left unchanged.

选择背景和基色中较亮的部分。背景被基色中较亮的部分替换；否则，保持不变。

`color-dodge`

`颜色减淡模式`

Brightens the backdrop color to reflect the source color. Painting with black produces no changes.

减淡背景色来反映基色。黑色绘制的部分不变。

`color-burn`
`颜色加深模式`

Darkens the backdrop color to reflect the source color. Painting with white produces no change.

加深背景色来反映基色。白色绘制的部分不变。

`hard-light`

`强光模式`

Multiplies or screens the colors, depending on the source color value. The effect is similar to shining a harsh spotlight on the backdrop.

对颜色正片叠底或滤色依赖于基色值。效果类似于在背景上用强聚光灯照射。

`soft-light`

`柔光模式`

Darkens or lightens the colors, depending on the source color value. The effect is similar to shining a diffused spotlight on the backdrop.

使颜色变暗或变亮，取决于基色值。效果类似于在背景上用发散的聚光灯照射。

`difference`

`差值模式`

Subtracts the darker of the two constituent colors from the lighter color. Painting with white inverts the backdrop color; painting with black produces no change.

从较浅的颜色中减去两个组成颜色的较深部分。白色绘制的部分背景反色；黑色绘制的部分不变。

`exclusion`

`排除模式`

Produces an effect similar to that of the Difference mode but lower in contrast. Painting with white **inverts the backdrop color**; painting with black produces no change.

产生类似于差值模式的效果但是对比度更低。白色绘制的部分**背景反色**；黑色绘制的部分不变。

`hue`

`色相模式`

Creates a color with the hue of the source color and the saturation and luminosity of the backdrop color.

创建于基色的色相、饱和度和亮度相同的颜色。

`saturation`

`饱和度模式`

Creates a color with the saturation of the source color and the hue and luminosity of the backdrop color. Painting with this mode in an area of the backdrop that is a pure gray (no saturation) produces no change.

创建饱和度与基色相同，色相和亮度与背景色相同的颜色。在背景是纯灰（没有饱和度）的区域使用这个模式不产生改变。

`color`

`颜色模式`

Creates a color with the hue and saturation of the source color and the luminosity of the backdrop color. This preserves the gray levels of the backdrop and is useful for coloring monochrome images or tinting color images.

创建色相和量度和基色相同，饱和度和背景色相同的颜色。保持背景的灰度并且对于给单色图片或图片着色很有用。

`luminosity`

`亮度模式`

Creates a color with the luminosity of the source color and the hue and saturation of the backdrop color. This produces an inverse effect to that of the Color mode. This mode is the one you can use to create monchrome "tinted" image effects like the ones you can see in different website headers.

创建亮度和基色相同，色相和饱和度与背景色相同的颜色。这个模式产生的效果和Color模式相反。你可以用这个模式创建和许多网页头部图片效果一样的单色图片效果。

The following image shows the result of applying the different blend modes to an image, in the same order mentioned above, starting from the top left corner.

下面图片展示了在一张图片上应用不同混合模式的结果，跟上述提到的顺序一致，从左上角开始。

![](background-blend-mode-examples.png)

For more information about these blend modes, I refer you to [this article](http://www.slrlounge.com/school/photoshop-blend-modes/) on the SLR Lounge blog. It claims to be the ultimate visual guide to blend modes, and does include some nice explanations of the blend modes.

要获取更多这些混合模式的信息，我推荐你SLR Lounge博客上的[这篇文章](http://www.slrlounge.com/school/photoshop-blend-modes/)。这篇文章被称为混合模式终极视觉指南，确实包括一些关于混合模式非常好的解释。

Personally, I think that even with the definition for each mode at hand, it can be really hard (if not impossible) to predict the result of applying these modes to an image.

从个人角度而言，我认为即使眼前有每个模式的定义，要预测出对一张图片应用这些模式的结果依然是很难的（几乎不可能）。

Picking a suitable blend mode will be—in most cases—a case of trial and error. If you use Instagram you know that sometimes you just go over each of the available filters, applying them one after the other, till you get the effect you're after. (I know I do that!) With CSS blend modes, it's practically the same.

在大多数情况下，选择合适的混合模式将会是经历一系列试验和错误的结果。如果你用过Instagram那么一定知道有时候你会尝试每一个可用的滤镜，一个个应用，直到你获得了想要的效果。（我就这样做！）这在css混合模式中，几乎是一样的。

For that reason, I've created a simple interactive demo that you can use to pick the right blend mode for your effects.

因此，我创建了一个简单的互动演示你可以用来为达到想要效果选择正确的混合模式。

![Screenshot of the CSS Blender demo.](css-blender-demo-screenshot.png)

You can upload an image, and choose a background color to blend it with. The background color of the live preview (thumbnails) will live-update as you make your way around the color picker. **Clicking on a thumbnail will preview the selected blend mode in the larger preview area.**

上传一张图片，选择想要混合的背景色。实时预览（缩略图）的背景色会随着你在拾色器中的移动实时更新。**点击缩略图会在更大的预览区域预览选择的混合模式。**

<a href="http://sarasoueidan.com/demos/css-blender" class="button">Try the blend modes in the demo out.</a>

Of course, the effects will be visible only in browsers that support the `background-blend-mode` property. **For more information about browser support, refer to** [the compatibility table over at CanIUse.com](http://caniuse.com/#feat=css-backgroundblendmode).

当然，只有在支持`background-blend-mode`属性的浏览器中才能看见效果。要获取更多浏览器支持信息，参考[CanIUse.com上的支持性表格](http://caniuse.com/#feat=css-backgroundblendmode)。

In addition to blending a background image with a background color in the interactive demo, you can also blend a piece of text with the element that has this background.

除了演示例子中的把背景图和背景色混合，你也可以把文字和有背景的元素混合。

But blending separate elements together requires a property other than the `background-blend-mode` property. Let's have a look at that next.

然而要把分离元素混合到一起需要除了`background-blend-mode`之外的属性。下面让我们来看一看。

###Blending An Element With Elements In Its Backdrop: The `Mix-Blend-Mode` Property
###将元素与背景中的元素混合：`Mix-Blend-Mode`属性

As we mentioned earlier, a **backdrop** is **the content behind the element** and is what the element is composited with.

我们之前提到，**背景**是**元素背后的部分**也是元素与之复合的部分。

The content behind the element can be anything—including other elements. And this is where the interesting effects come in. Think fixed headers blending with the content as the page scrolls down, or text blended with an image in the background, or text blending with other text, etc.

元素背后的部分可以是任何东西－包括其他元素。这里会产生有趣的效果。试想一下当页面向下滚动时固定的头部和内容混合，或者文字和背景上的图片混合，或者文字和其他文字混合等等。

Blending elements together is done using the `mix-blend-mode` property.

使用`mix-blend-mode`属性把元素混合在一起。

The `mix-blend-mode` property is similar to the `background-blend-mode` property, and takes the same blend mode values. So, you can specify any blend mode to get different blending effects.

`mix-blend-mode`属性类似于`background-blend-mode`属性，使用相同的混合模式值。所以你可以指定任何混合模式来达到不同的混合效果。

For example, the text in the following image blends with the image behind it using `mix-blend-mode: difference`, giving the illusion of the water bubbles passing through and in front of the text. The reason this effect is established is the color inversion process of the `difference` mode.

例如，下面图片中的文字与下方图片使用`mix-blend-mode: difference`混合，表现出水泡穿过并且在文字上方的错觉。这个效果的原理是`difference`模式下的颜色反转。

![](mix-blend-mode-example-1.png)

The area of the image where it overlaps with the text is the text's backdrop, and that is where the blending happens. You can check the live demo out [here](http://codepen.io/SaraSoueidan/pen/e90334f6ffdbb2a2cdd5604e769054e4?editors=110).

这幅图片与文字重叠的地方是文字背景，也是混合的地方。你可以在[这里](http://codepen.io/SaraSoueidan/pen/e90334f6ffdbb2a2cdd5604e769054e4?editors=110)查看在线演示。

Using `mix-blend-mode`, you can create many creative effects—far more than I could list in this post. One particularly interesting effect you can create is see-through text. Without CSS blend modes, you would need CSS masking and/or background clipping, along with some CSS hackery to create this effect and make it work.

使用`mix-blend-mode`，你可以创建许多创造性效果－远不止我在这片文章中列的这些。你可以创建的一个特别有趣的效果是－穿透的文字。没有CSS混合模式的话，你需要CSS遮罩和/或背景裁剪，以及一些CSS hackery来创建这些效果并使之生效。

With blend modes, and using the `difference` blend mode again, you can create this effect by—again—leveraging the color inversion process.

通过混合模式，再一次使用`difference`混合模式，你可以再一次借助反色过程创造这样的效果。

The following image shows this effect in action. It is merely a piece of text, positioned on top of an image, and blended with it.

下面图片实际展示了效果。这不过是一段·文字，位于一张图片上方并且与之混合。

![](see-through-text-mix-blend-mode.png)

That's pretty cool, isn't it? You can check the live demo out [here](http://codepen.io/SaraSoueidan/pen/887433527fac4e926e84b613be483bfc?editors=110).

这很酷，不是吗？你可以在[这里](http://codepen.io/SaraSoueidan/pen/887433527fac4e926e84b613be483bfc?editors=110)查看在线演示。

It is worth noting here that the colors you choose strongly affect the end result. That being said, the interactive demo can make picking the right colors for such an effect easier and faster.

值得注意的是你选择的色彩严重影响最终结果。也就是说，互动演示让你更简单快速得选择正确颜色来到达这一效果。

In the interactive demo, you have an option to add editable text to the preview area, and then style that text and blend it with the preview image using `mix-blend-mode`. The following is a screenshot showing an example.

在这个互动演示中，你可以选择在预览区域添加编辑文字，给文字赋予样式并使用`mix-blend-mode`与预览图片混合。下面是这个例子的截图。

![](css-blender-demo-screenshot-with-text.png)

<a href="http://sarasoueidan.com/demos/css-blender" class="button">Check the demo out.</a>

Since we're talking about blending elements together, it only makes sense that we mention stacking contexts, especially considering that they affect how and what elements can be blended together.

当我们讨论把元素混合在一起时，只有在提到层级时才有意义，尤其是考虑到它们会对把什么样的元素如何混合在一起产生影响。

According to the specification, applying a blend mode other than `normal` to the element must establish a new stacking context on that element, forming a group. This group must then be blended and composited with the stacking context that contains the element.

根据规范，在元素上应用除`normal`外的混合模式必须在它之上建立一个新的层级，形成一组。这个组必须被包含这个元素的层级混合并复合。

Also, an element that has blending applied, must blend with all the underlying content **of the stacking context that that element belongs to**. It will not blend with contents outside that context.

另外，应用了混合的元素，必须和所有这个元素**所属层级的底层内容混合**。它不会和背景外的内容混合。

For example, the following image shows the result of mix-blending two images with the `overlay` mode. ([Live demo](http://codepen.io/SaraSoueidan/pen/09efabde7114d37a736525b5ab616bc5?editors=110))

例如，下面的图片展示了用`overlay`模式混合两张图片的结果([在线演示](http://codepen.io/SaraSoueidan/pen/09efabde7114d37a736525b5ab616bc5?editors=110))

![](mix-blend-mode-example-2.png)

The code for the above simple example looks like so:

上面这个简单例子的代码如下：

```
	<div class="container">
	  <img src="path/to/destination.png" alt="" />
	  <div class="img-wrapper">
	    <img src="path/to/source.png" alt="" class="source"/>
	  </div>
	</div>
```

I've wrapped the image on top (the `.source`) in a `div` that I'm going to create a stacking context on. Since the `opacity` property leads to the creation of a new stacking context when given a value other than th default (`1`), I'm going to use that.

我把上方的图片（`.source`）包裹在我想要创建层叠环境的一个`div`中。因为当给`opacity`属性一个除了默认值（`1`）之外的值时会导致新层的创建，我将用到这一。

```
	.img-wrapper {
	  opacity: .99;
	}
```

(Try it in the [live demo](http://codepen.io/SaraSoueidan/pen/09efabde7114d37a736525b5ab616bc5?editors=110).)

(去[在线例子](http://codepen.io/SaraSoueidan/pen/09efabde7114d37a736525b5ab616bc5?editors=110)尝试)

By creating a stacking context, the `.source` image no longer blends with the bottom image, because the latter lies outside the stacking context containing the former.

通过创建层叠环境，`.source`图片不再和底部图片混合，因为后者在包含前者的层叠环境之外。

This is because we have **isolated** the image (and any other contents of the `.img-wrapper` context) from the rest of the elements, and thus they don't blend with their backdrops anymore.

这是因为我们把图片和（和任何其他`.img-wrapper`背景的内容）元素的其余部分**隔离**了，因此它们不会再和背景混合。

This brings us to the `isolation` property. But before we move on, note that the `mix-blend-mode` property also applies to SVG elements, and can be used to blend overlapping SVG elements together as well. As a matter of fact, the logo for the CSS Blender demo is a result of applying a `mix-blend-mode` to the three squares that make the demo up. You can see how the areas where these squares overlap have different colors due to the color blending applied.

这把我们引入了`isolation`属性。在我们继续前，注意`mix-blend-mode`属性也可以应用在SVG元素上，用来把重叠的SVG元素混合在一起。事实上，CSS混合事例的logo就是把`mix-blend-mode`应用在三个方形上组成的。你可以看到三个方形重叠的区域由于颜色混合的应用有不同的颜色。

Browser support for the `mix-blend-mode` property is not as wide as that of the `background-blend-mode` property. For details, refer to [the browser compatibility table over at CanIUse.com](http://caniuse.com/#feat=css-mixblendmode).

`mix-blend-mode`属性的浏览器支持不像`background-blend-mode`属性一样广泛。更多细节，参考[CanIUse.com上的支持性表格](http://caniuse.com/#feat=css-backgroundblendmode)。

###Isolating Elements: The `Isolation` Property
###隔离元素：`Isolation`属性

When a property that leads to the creation of a stacking context is applied to an element, that element is said to be **isolated**. The last example in the previous section is an example of this happening.

当一个能导致层叠环境创建的属性应用在元素上时，我们称这个元素**被隔离**。上一节的最后一个例子是一个这种情况的例子。

On the other hand, you can use the `isolation` property to isolate elements.

另一方面，你可以使用`isolation`属性来隔离元素。

In SVG, this property defines whether an element is isolated or not. For CSS, setting `isolation` to `isolate` will turn the element into a stacking context, and thus affect whether or not the element's contents can blend with their backdrop lying outside this context. By default, the `isolation` property is set to `auto`—which implies that they are not isolated.

在SVG中，这个属性定义一个元素是否被隔离。在CSS中，设置`isolation`为`isolate`会把元素变为层叠环境，因此影响元素的内容是否会和这个环境外的背景混合。默认的，`isolation`属性被设置为`auto`-代表着它们没有被隔离。

If we were to go back to the previous example with the two blended images, we can prevent the image on top from blending with the image behind it by using the `isolation` property instead of the `opacity` property.

如果我们回到之前两个混合图片的例子，我们可以使用`isolation`属性而不是`opacity`属性来防止上层图片与它后面的图片混合。

```
	.img-wrapper {
	  isolation: isolate;
	}
```

This has the same effect as using `opacity` in the previous example. If you use this rule instead of `opacity` in the live demo, you will get the same result.

这和之前的例子中使用`opacity`有一样的效果。如果你在线上例子中使用这个规则而不是`opacity`，会得到一样的结果。

Note that by creating a stacking context on an element, you are isolating the content of that element and preventing them from blending with the backdrop of that element. However, you can still apply a blend mode to the entire context to blend it with its backdrop.

注意通过在元素上创建层叠环境，你把元素的内容隔离并且防止它们和这个元素的背景混合。然而，你仍然可以给整个环境应用混合模式来把它与背景混合。

Moreover, If you are using the `background-blend-mode` property, the `isolation` property is not needed since background layers must not blend with the content that is behind the element, instead they must act as if they are rendered into an isolated group (the element itself), as specified in the specification. This is why the `isolation` property will have an effect when used with the `mix-blend-mode` property, but not with the `background-blend-mode` property.

而且，如果你正在用`background-blend-mode`属性，`isolation`就没有必要了因为背景层一定不会和元素后面的内容混合，规范中规定，它们必须表现出被渲染在一个隔离组中（元素自身）。这就是为什么`isolation`属性和`mix-blend-mode`一起用时有效，和`background-blend-mode`属性一起用时无效。

###Note: Order Of Graphical Operations
###注意：图形操作的顺序

CSS blending modes, [filters](http://www.w3.org/TR/filter-effects-1/) and [masks](http://www.w3.org/TR/css-masking-1/), can all be applied to the same element. But which effect is applied first?

CSS混合模式，[滤镜](http://www.w3.org/TR/filter-effects-1/) 和 [遮罩](http://www.w3.org/TR/css-masking-1/)，都可以应用在相同元素上。但是哪个效果会首先应用呢？

According to the specification, first any filter effect is applied, then any clipping, masking, blending and compositing.

根据规范，首先任何滤镜效果会被应用，然后是任何裁剪，遮罩，混合以及复合。

###Final Words
###最后的话
With all the graphical operations available to us via CSS, we are getting more possibilities for designing in the browsers—this is particularly interesting if you—like me—are not into graphics editors and don't know your way around them well.

通过CSS的所有可用图形操作，我们有了更多浏览器中设计的可能性－这尤其有趣如果你－像我们一样－不使用图形编辑器并且不知道怎么使用它们。

The web platform team at Adobe have been doing a tremendous job bringing many of their tools' graphical capabilities to the web. From filters, to blend modes, clipping and masking, and even [CSS Shapes](http://sarasoueidan.com/blog/css-shapes), we are gaining more control over layout and graphics on the web.

Adobe的网页平台团队进行了庞大的工作来把它们的工具的图形能力移植到网页上。从滤镜，到混合模式，裁切和遮罩，甚至[CSS Shapes](http://sarasoueidan.com/blog/css-shapes)，我们将获得更多网页端的控制布局和图形的能力。

Many creative effects can be created using CSS blend modes, and when combined with other technologies, they open a door to endless creative possibilities.

使用CSS混合模式可以创造许多创造性的效果，结合其他技术，它们打开了一闪通往无尽创造可能性的大门。

I hope you liked this article and found it useful.

我希望你喜欢这篇文章并发现它有用。

Thank you for reading!

感谢阅读！