##一个前端开发者献给说明文档的颂歌

在物理世界，没有人不绘制详细蓝图就建造东西，因为人们的生命是紧要的事情。在数字世界，风险并没有那么高。

它被称为“软件”是有原因的：当击中你的脸，你不会很疼。没有人会因为你的网页头部和它下方的图片左边距差4个像素没有对齐而死。

但是，当用户的生命也许不是最紧要的事情时，设计蓝图（也叫设计说明书或说明）意味着被正确实施的提高用户体验和客户满意度的设计与混乱不一破坏用户体验并使用户不愉快的设计之间的区别。

对于我们这些创造数字产品的人，设计说明意味着高效合作与浪费的重复性的过程、高代价的执行错误以及传输延时之间的区别。这也可能意味着你事业赚钱和亏本之间的区别，这件事也许导致了生命成为最紧要的事情。

简单的说，说明帮助我们更快更高效得构建正确的产品。

###为什么是蓝图（它们为什么是蓝色的）？
为什么蓝图是蓝色的？要找到这个答案，我们往前倒退一点，[摘自维基百科](http://en.wikipedia.org/wiki/Blueprint)：
	
	“蓝图是技术绘制的再现，纪录建筑或者工程学设计，在感光的纸上使用接触性的打印过程。在19世纪杯引进, 这个过程可以快速而精确得复制在建筑和工业中使用的文档。蓝色打印的过程是通过把光照在蓝色的背景上形成的，最初被认为是副作用。”

建筑学蓝图起源于19世纪的影印机。它们是当时存在的最便宜可靠的复制工艺制图的技术。

![Architectural drawing](http://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Joy_Oil_gas_station_blueprints.jpg/800px-Joy_Oil_gas_station_blueprints.jpg)

蓝图通过把光线照到涂在透明胶卷上的墨水标记来创建。光线会透过除墨水外的每个地方并且照在涂有一层感光物质的纸上，从而把纸变蓝。这样在深蓝色背景上画出一个工程绘图复制图的白色轮廓。

这些复制图随后被分发给负责实施这些制图中设计的建造者。

如今，许多图形设计师同样把说明分发给负责实现这些设计的前端开发者。设计说明不再是用纸和灯光来制作，它们也不再是蓝色的，但是像过去一样，它们保证了产品被正确构建。

###从砖块到位和比特

之前作为房地产开发者的职业生涯让我学到了建筑学蓝图的价值。我的职责之一是寻找卓越的设计师来构建蓝图这样我们雇佣的建筑工人就可以精确知道要建造什么。在这条路上的某一时刻，我意识到现实的房地产开发不适合我：通过建造可扩展的虚拟的而不是真实的世界的轮廓，我想要产生更大的影响。我学习HTML,CSS和JavaScript并且寻求受雇于创业公司。我对详细蓝图重要性的理解一直跟随着我。

在万维网启动拓荒之时，我需要构建看起来很棒并且性能良好的单页JavaScript应用，并且我需要快速创建它。设计师通常会在产品发布日期一周前结束工作并传递给我们，然后我们要加速冲刺。设计图通常包含有许多图层但没有任何补充说明的Photoshop文件（PSDs）。

对一个之前现实世界的房地产开发者来说，和没有说明的图形设计师一起工作像是得到了一系列的包含所有图样的建筑蓝图却没有序号。没有必要的CSS“标准”。我不得不在形状和文字元素的图层和子图层中积极寻找来发现叫“Buy”的按钮边框的正确HEX值或者"Forget Passowrd？"区域使用的字体。这样的工作流非常低效。

我对于说明非常渴望，我的朋友Chen Blume给我提供了Specctr的点子。它是一个把和建筑蓝图类似的优点带到图形设计和网页前端开发世界中来的工具。我立即意识到这个点子的价值和潜力，所以我们立即开始一起工作，Specctr第一版发布了。

![Properties of objects (specs) created with the Specctr plugin](http://www.smashingmagazine.com/wp-content/uploads/2014/10/2-specctr-for-fireworks-properties-of-objects-500px.png)

目前，Specctr插件只能支持Adobe Fireworks用户，它在这个时候－2012-似乎是UI和web设计者的最佳工具。随后，我们扩展了支持的app范围，现在包括了Fireworks,Illustrator,Photoshop和InDesign。

###百闻（以及一些数字）不如一见
有人说百闻不如一见。当然，图片和一些RGB值可能更有价值！

![One look is worth a thousand words](http://www.smashingmagazine.com/wp-content/uploads/2014/10/3-1913-piqua-ohio-advertisement-500px.png)

谚语“百闻不如一见”意味着复杂的思想可以通过一张静止图片传递。它同样很好得描述了形象化的主要目标之一，这使得快速抛弃大量数据变为可能。然而，在设计和开发中，一张图片或单一的PSD文件是不够的。

开发者需要知道设计师的准确意图从而能构建必要的HTML和CSS以通过代码重新创建文本和形状元素。如果一个PSD文件没有详细说明，那么猜测相近意思或者从图层里寻找都可能导致错误或开发时间损失。

###开发者的焦点
当开发一些东西时，我在开始生产前可能需要几分钟来加载脑海中必要的思维模块。任何中断都会摧毁我脑海中不断斗争而组合起来的复杂的假想机械。

这就是为什么需要查看RGB值或向队友询问哪个用到的字体可能在我的生产过程中产生巨大的中断。

如果你是分布式或远程团队的一员，你甚至不敢奢望你的问题能得到同事的立即解答－你需要借助异步聊天工具如Skype，Hipchat，或者更糟，email。[像Chris Parnin写的一样](http://blog.ninlabs.com/2013/01/programmer-interrupted/)：
	
	“办公环境下中断引起的花销已经在研究。一个中断的任务被估计需要花费两倍的时间并且比起未中断的任务包含的两倍的错误。57%的任务会被中断，工作者需要在一个碎片化的状态中工作。对于程序员来说, 有很少的迹象表明中断的感受和普遍性。通常来说， 中断后至少要15分钟才能重新回到“零”状态。程序员的调查也提供了提供了相似的数字。”
	
![This is why you shouldn’t interrupt a programmer](http://www.smashingmagazine.com/wp-content/uploads/2014/10/4-this-is-why-you-shouldnt-interrupt-a-programmer-500px.png)

###错误的狂欢：开发者版本

Julia已经在电脑上工作了8个多小时并且耽误了和她父母的晚饭，但她已经承诺今天完成主要分支上"product"蒙板和"buy"蒙板的的CSS过渡。她已经快完成了，但是"Submit"按钮的类型看起来和现在网页中的那个不像。

“这没问题”，她想，“我明天修改一下。”

面对很短的最后期限以及在Photoshop图层中的仔细翻查，一些开发者也许会陷入一片黑暗而不知道应该用什么类型－因此，他们浪费了数个小时在设计查找上来投入一个充满压力的决定。

![The font looks the same. Well, almost.](http://www.smashingmagazine.com/wp-content/uploads/2014/10/5-buy-button-example-500px.png)

最后，我们无论如何都要重做，但是现在我们将面临最后期限。所有这些都关乎开发者是否方便。

历史上没有人永远把额外的努力花在错误的事情上。错误通常是遵循短暂捷径的结果。

有记载的工业上阻止数字音乐分发的失败是一个很好的例子。Spotify的[整体商业模型](http://www.theguardian.com/technology/2013/nov/10/daniel-ek-spotify-streaming-music)基于这样一个事实："人们只有在得到奖励的情况下比起做错误的事情更愿意做正确的事情，这是无需争辩的。"

提供给你的前端开发者一份说明完整的设计稿并且从他们脸上表现出的微小感激得到满足。他们会完全正确获得你设计的外边距和内边距；你花了很长时间匹配的微妙的渐变值；这样能更快得搞定工作。它们还能做一些其他什么事情呢？所有需要的信息就在他们面前！

###沉默的胜利：设计师版本
Lauren花了几秒欣赏她完成的设计。它很均衡并传递出一丝平静，这都是她把目光投在“Submit”按钮上感受到的。

她在一天长时间的工作后已经很疲惫并准备回家，但她已经承诺上传完成的设计图这样Julia可以在明天最后期限前立马开始开发。她有时候给一起合作的开发者写上说明，但她并不是“用手”来打印和画上每一个独立注释。

“Julia会自己理解的，”她边想边点击了“发送。”

这些都关乎设计师是否方便。

如果提供太多的设计说明（即蓝图），那么为什么不把它们纳入每一个设计师的工作流中呢？作为一个开发者我认为很多设计师忽略类型和不写说明的理由是一样的：这很容易忽略。

这是因为设计师没有使用正确的工具。他们手工测量和绘制每个尺寸，“手工”键入每个像素值和RGB值，他们使用相同的多用途绘制工具来创建设计。

任何时候你要让一个艺术家停止创造和专注一个过程，无疑是在打一场艰难上坡的战争。当这个过程缓慢且单调时那么这座山会戏剧性得陡峭。

通过正确的工具来自动创建说明，设计师可以减少花销并且让他们整个团队在创建和发布设计说明获得好处。

###让我们创建（和使用）设计说明
上面Julia和Lauren的两个例子是虚构的。但这并不意味着他们这样的例子不经常在现实生活中发生。开发者不应该需要做任何可能导致错误和时间损耗的猜测。另一方面，手动创建详细的说明是单调并且耗费很多设计师的时间。

有没有一个更好地办法呢？我相信是有的。

我们应该开始使用工具帮助我们在困难最小的情况下创建设计说明。这样的工具可以让设计师和开发者都节约时间并可以带来更好的设计师-开发者工作流。

下列是一些使用Specctr标注的设计文档的引用。通过Specctr插件的帮助，设计师可以快速提供任何设计元素的颜色值，精确的宽度和高度，渐变值，类型标签（包括字体，粗细，间距，行距，等等），外边距，内边距，边框属性，甚至更多。这会帮助开发者的设计实施因为他们不再需要从图层和子图层里去寻找或做任何猜测。

![Text and spacing specs generated with Specctr](http://www.smashingmagazine.com/wp-content/uploads/2014/10/6-specctr-top-left-spec-500px.png)

![hape and text specs generated with Specctr](http://www.smashingmagazine.com/wp-content/uploads/2014/10/7-specctr-mid-left-spec-500px.png)

![Coordinate and spacing specs generated with Specctr](http://www.smashingmagazine.com/wp-content/uploads/2014/10/8-specctr-mid-bottom-spec-large.png)

作为一个额外的副作用，当在现实世界里被实施时，使用详细设计说明会在最终版本的设计中帮助你避免错误和矛盾。下列是一系列当实施细节不精确时由于开发者的猜测而发生的“漂移”。

![A comparison of how a design can deviate from a designer’s vision without proper documentation: spec’ed design on the left, unspec’ed design on the right.](http://www.smashingmagazine.com/wp-content/uploads/2014/10/9-how-a-design-can-deviate-without-documentation-example-500px.png)

注意：Specctr不是唯一的自动生成详细设计说明的工具。例如[PNG Express](http://www.pngexpress.com/)（被设计成结合Photoshop使用）之类的插件能实现类似的功能，但我一直提Specctr因为它是我自己开发的并且我有更多的经验。如果你尝试了其他的说明生成工具，请在底下的评论中分享你的经验。

###组件和样式说明

开发者长久以来已经很熟悉通过[面向对象编程](http://en.wikipedia.org/wiki/Object-oriented_programming)把一个大型系统分成小型组件的好处，面向对象编程是目前占有统治性地位的编程范例，感谢一些语言的采用例如[Java](http://en.wikipedia.org/wiki/Java_%28programming_language%29)。把复杂系统分成自包含的部分来组成整体使得单个部分可以在项目中的许多地方复用并且使得项目组织结构更好，可维护性更高。

设计师也[发现](http://bem.info/method/)把一个设计分成构成的元素组件效率更高因为可以结合来复用[代码和样式](http://pea.rs/)。从项目整体设计的角度去看组件的出处能够立即传达出项目中使用样式的选择。组件的例子有栅格，按钮，表单，表格和列表。

![Grid component from Mozilla’s “Style Guide”.](http://www.smashingmagazine.com/wp-content/uploads/2014/10/10-mozilla-grid-comp-500px.png)

![List component from Mozilla’s “Style Guide”.](http://www.smashingmagazine.com/wp-content/uploads/2014/10/11-mozilla-list-comp-500px.png)

带有设计说明的组件组成一个[样式向导](http://medium.com/@bradhaynes/designing-products-that-scale-c8f3001f709b)。样式向导传递项目的设计美学并给开发者的实施细节提供了参考。开发者不再依赖设计师来提供独立文档说明，他们可以使用这个向导来寻找需要的信息。通过这种方式，样式向导是另一个设计师和开发者间高效合作的工具。

![A style guide will help you to maintain a consistent look over time. (Source: “How to Make an Effective Style Guide With Adobe Fireworks”).](http://www.smashingmagazine.com/wp-content/uploads/2014/10/12-style-guide-fireworks-500px.png)

###总结

我咨询了一些设计师关于他们对文档设计过程的评价。我最喜欢的一个回应是Jason Csizmadi的，来自[Cooper](http://www.cooper.com/)的高级视觉设计师：


> 开发者在项目的任何阶段都期望并且需要完整文档。


> 虽然文档从来不是设计中令人兴奋的方面，它是保证流畅工作关系，及时交付和最终成功传递的决定性一步。最终，设计文档会表现得像一个生命支持系统，保证你的想象力被完全执行。

如同任何优秀的企业流程，设计说明应该支撑最基本的努力-在这种情况下创建优美的网页和应用。创建这些需要设计师和开发者合作的产品，高效合作需要高效沟通。对开发中的工作流和工具的投资使得沟通变得更简单高效并会在产品构建时反馈更快的速度和效率，最终，事业的成功取决于这些产品。

###延伸阅读
* “[Best Practices for Designer-Developer Collaboration](http://pivotallabs.com/best-practices-for-designerdeveloper-collaboration/)，”George Dean
A nice summary of the different workflows available to developers and designers

* “[How to Improve Designer and Developer Workflow?](http://programmers.stackexchange.com/questions/141624/how-to-improve-designer-and-developer-work-flow),”StackExchange A discussion illustrating some of the concerns about designer-developer workflows

* “[Blueprint](http://en.wikipedia.org/wiki/Blueprint),” Wikipedia
A detailed definition (and some history) of the word “blueprint”

* “[Programmer Interrupted](http://blog.ninlabs.com/2013/01/programmer-interrupted/),” Chris Parnin
Some studies and resources on the effects of interruption on programming

* “[Creating a Killer Style Guide](http://zurb.com/university/lessons/31),” Ben Gremillion, Zurb
A tutorial on creating a style guide

* “[How to Make an Effective Style Guide With Adobe Fireworks](http://www.smashingmagazine.com/2014/02/17/effective-style-guides-with-adobe-fireworks/),” Joshua Mauldin, Smashing Magazine An interesting read on making style guides with Fireworks

* “[Blueprints for the Web: Specctr Adobe Fireworks Plugin](http://www.smashingmagazine.com/2012/05/25/blueprints-for-the-web-specctr-adobe-fireworks-plugin/)”and“[Blueprints for Web and Print: Specctr, a Free Adobe Illustrator Plugin](http://www.smashingmagazine.com/2013/11/15/specctr-an-adobe-illustrator-plugin-freebie/),” Chen Blume, Smashing Magazine Examples of using the Specctr plugins for Fireworks and Illustrator

我想要感谢[Michel Bozgounov](http://www.smashingmagazine.com/author/michel-bozgounov/)，他帮助我探索这篇文章并且提供了一些改进的建议。