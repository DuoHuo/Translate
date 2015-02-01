##Compositing And Blending In CSS
##CSS中的拼接与混合

If you're a designer, then you've probably already come across blending effects some time or the other. Blending is one of the most frequently used effects in graphic and print design. You can add texture to text by blending it with its textured backdrop, create an illusion of merged images by blending these images together, and create a wide range of colorful effects that would not be possible without that fine level of color blending control.

如果你事一个设计师，你一定已经或者迟早会遇到混合效果。混合是在图形和印刷设计方面被使用最频繁的效果之一。你可以通过混合文字和纹理背景来给文字添加纹理，把图片混合在一起创造融合图片的幻觉，以及创造那些广泛而丰富多彩的效果，如果没有对混色控制达到如此精细的程度要创造这些效果是不可能的。

![](blending-examples.png)

Graphics editors such as Photoshop or Illustrator come with a set of blending modes. **Blend modes** allow you to specify how you want your elements to blend together, thus changing the colors of the area where these elements intersect. Each mode uses a specific color formula to mix the colors of the source and the destination.

图形编辑器例如Photoshop或Illustrator自带了一系列混合模式。**混合模式**让你可以指定混合的元素，从而改变元素交叉区域的颜色。每个模式使用一个特定颜色公式来混合源和目标的颜色。

Different modes give different end results. Before we talk about the different blend modes, and since we mentioned the **source** and **destination** elements, let's have a quick look at the concept of compositing, and how it is related to blending in CSS.

不同模式带来不同最终结果。在我们讨论不同混合模式前，既然我们提到了**源**和**目标**元素，让我们快速的了解一下合成的概念，以及它和CSS中的混合有什么关系。

###What Is Compositing?
###合成是什么？

Compositing is the combining of a graphic element with its backdrop.

合成是图形元素与背景的结合。

A **backdrop** is **the content behind the element** and is what the element is composited with.

**背景**是**位于元素后面的内容**并且也是元素与之合成的内容。

![](backdrop.png)

Compositing defines how what you want to draw will be blended with what is already drawn on the canvas. The source is what you want to draw, and the destination is what is already drawn (the backdrop).

合成定义了你想要绘制的元素将会如何与画布上已经绘制的元素混合。源是你想要绘制的元素，目标是你已经绘制的元素（背景）。

So, if you have two elements, and these elements overlap, you can think of the element on top as being the source, and the parts of the element behind that lie beneath it, will be the destination.

所以，如果你有两个元素，这些元素交叠在一起，你可以把上层的元素当做源，另一个元素位于它下面的部分是目标。

Using different composite operations (there are 16 operations), you can specify which parts of the two overlapping elements will be drawn, and which will not.

使用不同的复合操作（有16种操作），你可以指定绘制两个重叠元素的哪些部分，哪些不绘制。


![](porter-duff.png)

These composite operations are known as **Porter Duff compositing operations**. These operations specify what portions of the source and destination will be drawn, and blend modes specify how how the colors from the graphic element (source) and the backdrop (destination) interact. The illustrations in the above image are from the Compositing and Blending spec. In HTML5 Canvas context, these oprations are specified using the `globalCompositeOperation` property, and can be used to clip backgrounds to specific shapes, such as text, thus creating the effect of texture-filled text in Canvas. I have written about this process in [this article](http://tympanus.net/codrops/2013/12/02/techniques-for-creating-textured-text/) over at Codrops.

这些复合操作叫做**Porter Duff混合操作**。这些操作指定源和目标的哪些部分被绘制，混合模式指定图形元素（源）上的颜色如何与背景（目标）混合。上面图片中的插图来自合成和混合规范。



