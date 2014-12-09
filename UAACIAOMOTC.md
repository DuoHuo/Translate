##使用和滥用 – CSS继承和层叠的滥用

我认为我们正滥用CSS的继承模型。我知道CSS中的“C”代表“层叠”，但这不意味着从最简单的选择器到一个复杂组件都需要层叠。经常性的一个```h2```从根一级的```h2```标签获得了基础层的样式，然后得到第二个样式应用因为它定位在页面上一个特别区域。第三个样式应用被添加因为它属于一系列共享普遍样式的组件。最后，由于```h2```属于这个组件的一个特殊变化，它在最上面有第四层样式。

仅仅是标记的一小部分，4个分布各处的样式来源组合在一起。听起来复杂而又疯狂？这也许很疯狂，但是绝不是罕见的。

###掉进兔子洞

这都是因为某人说了一句：“我不想每次增加一个h2都写CSS”引起的。所以我们这样写：

	h2 {
	  color: #fd7900;
	  font-size: 1.8em;
	  line-height: 1.1;
	  margin-bottom: .3em;
	}

![](http://ivanctoe.qiniudn.com/uaa-1.png)

这一开始非常有效，但随后发生了一件事情：故事的主人想要改变```.sidebar h2``的样式。

	.sidebar h2 {
	  color: #8cc5e6;
	  font-size: 2.2em;
	  padding-bottom: .2em;
	  border-bottom: 1px solid black;
	}

![](http://ivanctoe.qiniudn.com/uaa-2.png)

我们不需要改变所有东西，只是颜色，尺寸和边框。所以我们利用了CSS层叠的好处并扭转需要更新的值。

###充满废弃鞋子的储藏室

我们试着聪明的把功能性的小块分离成可复用的侧边栏块，所以我们决定创建一些默认块样式。不管是现在或未来我们通过这种方法创建的所有块都能继承相同的样式。每个块都有一个```h2```，所以让我们看一看这会是怎样被赋予样式的。

	.block
	  border: 1px solid #8cc5e6;
	  padding: 0 15px;
	}
	.block h2 {
	  /* Color was changed by .sidebar h2, set it back */
	  color: #fd7900;
	  /* remove border added by .sidebar h2 */
	  border: none;
	  /* remove the margin set by h2 */
	  margin: 0;
	  padding: .3em;
	  background: #8cc5e6;
	  margin: 0 -15px;
	}

![](http://ivanctoe.qiniudn.com/uaa-3.png)

###下一次冲刺我们会喘不过气来

我们的块表现得很好。现在我们被要求使用最初的侧边栏头部创建一个可选的块级样式，但是填充灰色背景色。

	/* 
	The Markup
	<div class="block alt-block">
	  <h1>My Title</h1>
	  ...
	</div> 
	*/ 
	
	.alt-block {
	  /* Remove border from .block */
	  border: none;
	  padding: 15px;
	  background: #eee;
	}
	
	.alt-block h2 {
	  /* Need to set color set by .block h2 */
	  color: #8cc5e6;
	  /* Need to set the padding-bottom back to .sidebar h2 styles */
	  padding-bottom: .2em;
	  /* Need to set the border back to .sidebar h2 styles */
	  border-bottom: 1px solid black;
	  /* Remove negative margins and background from .sidebar h2 
	  but set bottom margin again from root h2 */
	  margin: 0 0 .3em;
	  /* remove background from .sidebar h2 */
	  background: none;
	}

![](http://ivanctoe.qiniudn.com/uaa-4.png)

####我们做了什么？
到这里！我们已经完成！故事是可接受的，代码被合并到主分支。但代价是什么呢？我们的```.alt-block h2```只包含覆盖的样式或恢复到我们已经写的样式。

在顶部，我们的标题现在从4个不同的选择器继承样式，显得臃肿，页面表现遭受重击，样式系统难以置信得脆弱。任何对```h2```,```.sidebar h2,.block h2```做出的改变都将影响```.alt-block h2```，无论我们是有意或者无意的。

![](http://ivanctoe.qiniudn.com/uaa-5.png)

###我的代码是受到约束的
所以到底发生了什么？在上面的例子里我们见识了3种不同的CSS继承的类型：标签继承，上下文继承和类继承。让我们来看一下它们每一个是如何生效的，它们为什么会引起问题以及修复这些问题的解决方案。

####标签继承
我们用HTML标签来使我们的页面语义化。当我们在这些标签上应用样式时，
我们最终会混淆语义和表现。我不介意把非常基础的一系列默认样式应用到标签上，但在我们的例子中当我们把完成的表现样式绑定到```h2```标签上时会陷入问题。这不仅仅是混淆其他```h2```标签，这也让那些基础样式一旦被覆盖就不可能再复用。

除了依赖标签继承来扩展我们的基础样式，我们应该把这些样式移动到可复用的类或继承上。如果你想的话甚至可以取```.h1```或```%h1```！但关键是避免把描述绑定到基础标签上，而是移动到[可选打印样式](http://css-tricks.com/opt-in-typography/)上。

####上下文继承
我经常听到有关于上下文继承的争论：“我想要侧边栏中的每个h2都看起来一样，我不想每次创建一个新的侧边栏部件时都写CSS。”

这一类型的想法完全违背了组件应该独立，可复用，并且不依赖父容器的宗旨。使用上下文继承意味着你头部的样式取决于是否在侧边栏中（不是独立或者可复用的），并且在写样式前你需要清楚直接父容器。

当我了解了上下文继承的意图后，我个人看到它很多情况下的不足。

1. 有些人要求你为侧边栏创建一个新的头部样式，你最不想做的事情是尝试所有的6种头部标签（```h1```-```h6```）来看一下哪个的样式覆盖最少。
2. 你最终将被要求把一个主要内容区域的组件移动到侧边栏。你敢打赌有多少的可能性```.sidebar h2```的样式不会对你要移动的```.widget h2```产生任何影响。
3. 你也许认为使用后代选择器（例如```.sidebar > h2```）会解决所有问题，但你现在的样式取决于标记顺序，没有可以在页面其他地方复用那些```h2```样式。

最后，如果避免依赖上下继承，你的样式会变得更加灵活并且减少被破坏的可能。

###类继承
类继承尝试通过单类来把整个系统的样式应用到标记集合上。在我们的例子中有一个```.block```类是一个完整的组件，然后我们用```.alt-block```增加另外一系列规则。在“面向对象”的队伍里，这意味着```.alt-block```和```.block```紧密联系，或者它[“变更或依赖于另一个模块的核心作用”](http://en.wikipedia.org/wiki/Coupling_(computer_programming))。这不总是一件坏事，但这件事很快会变得复杂而脆弱。

想象一下你写的```.block```代码，队伍中的其他一个人决定使用```.block```创建```.my-calendar-widget```作为一系列基础样式，例如一个"依赖模块"。

	<div class="block my-calendar-widget">
	  <h2>My Calendar Title</h2>
	  ...
	</div>

除非系统的文件编码关系创建得很好，这会变成我喜欢称为“继承劫持”的情况。我们没有在CSS中指明```.block```有和它紧密联系的另一个组件，所以我们需要在每次更新```.block```时处理日历页面的随机bug。

这个困境的解决方法是放弃类继承并且把父类分离成可扩展块，包括容器，标题，文本和图像处理。这个方法通常被推荐来妥协，我只会用在少部分段落里。

###系统中继承的问题
继承不是CSS特有的。许多面向对象的编程语言使用继承的概念从父元素向子元素传递属性和方法。这类中的许多语言需要描述这个方法可能带来的陷阱（[Javascript](http://javascriptweblog.wordpress.com/2010/12/22/delegation-vs-inheritance-in-javascript)，[Java](http://javarevisited.blogspot.com/2013/06/why-favor-composition-over-inheritance-java-oops-design.html)，[Ruby](http://ruby.learncodethehardway.org/book/ex44.html)）。CSS也许不是一个像Ruby或者Java之类的编程语言，但是很多时候我们可以从这些语言里学到很多东西来帮助我们解决CSS中继承性的问题。让我们来看一看以下[一些经验](http://ruby.learncodethehardway.org/book/ex44.html#when-to-use-inheritance-or-composition)：

####多继承
> 不计代价避免多继承，因为要可靠得使用它会非常复杂。如果你被问题缠住，准备好理清类的层次并且花时间找出每样东西的来源。

如果你的组件使用不同的组合类来获得样式（例如我们的```.block```和```.my-calendar-widget```)，预见CSS组件的改变会如何影响页面将变得非常困难。除了搜索整个页面外（对于某些CMS来说几乎不可能），我们没有其他办法知道我们正在编辑的组件使用了哪些样式，并且这个改变会如何与其他被使用的类进行交互。

第二点，我们要终止把太多时间耗费在尝试理解一个元素样式的层次结构上。样式是从哪里来的？标签，类，父类，上下文，媒体查询，或是它们的结合？当每个元素的样式应用有各自的来源，调试和理解元素的预期行为会更加容易。

####结构 vs 继承
> 使用结构来将许多不同且在互不相关的地方和情况的代码打包成模块

尽管只有单个继承，我们的```.block```元素依然完全依赖于级联关系。把```.block```移出侧边栏会导致崩溃。把头部改成```H3```会崩溃。问题在于```.block```中的每个元素都从父类继承样式，例如块的位置和自身的HTML标签。因为语义化的关系没有定义样式，这是一个“标题”。

结构考虑的是一个html组件“包含”其他样式，而不是“继承”那些样式。你会发现这个原则被广泛得应用与OOCSS,BEM和Sass @extends里。并不是通过样式层级，每一个覆盖上一个，这个方法通过超级目标选择器使用[单一责任原则](http://en.wikipedia.org/wiki/Single_responsibility_principle)来[每次做好一件事并且只做一件事](http://csswizardry.com/2012/04/the-single-responsibility-principle-applied-to-css/)。

###把所有放在工作中

我们花了很大一部分时间探索不同类型的继承以及传统的面向对象的原则如何帮助我们识别继承模型中的问题并找到解决方案。现在让我们看看如何用Sass通过结构的方式来创建这个```.block```元素

####标记
注意有多少个标题有它特有的类。这允许我们选中标题而不管使用的标签。
	
	<aside class="sidebar">
	  <div class="calendar-widget">
	    <h2 class="calendar-widget-title">My Calendar Title</h2>
	    ...
	  </div>
	  <div class="latest-blogs">
	    <h2 class="latest-blogs-title">My Blog Title</h2>
	    ...
	  </div>
	  <div class="latest-news">
	    <h2 class="latest-news-title">My News Title</h2>
	    ...
	  </div>
	</aside>

####继承
如果你刚接触Sass，我们可以使用extend来传递一系列样式而不需要应用表现类，或者复制那些样式。使用静态的extends例如```%primary-header```来避免样式表中出现不可用的样式是很重要的。

	%primary-header {
	  font-size: 1.8em;
	  line-height: 1.1;
	  color: #fd7900;
	  margin: .3em;
	}
	
	%secondary-header {
	  font-size: 2.2em;
	  line-height: 1.1;
	  color: #8cc5e6;
	  margin: 0 0 .3em;
	  padding-bottom: .2em;
	  border-bottom: 1px solid black;
	}
	
	%block-header {
	  font-size: 2.2em;
	  line-height: 1.1;
	  color: #fd7900;
	  margin: 0;
	  padding: .3em;
	  background: #8cc5e6;
	  margin: 0 -15px;
	}
	
	%block {
	  border: 1px solid #8cc5e6;
	  padding: 0 15px;
	}
	
	%alt-block {
	  padding: 15px;
	  background: #eee;
	}

####给每个块赋予样式
要使用这些扩展中的一个我们只要简单得在选择器里写上```@extend %extend-name```，Sass会处理剩余的工作。

注意样式表是由多少语义化的选择器组成而不是从标签，上下文或者父类继承样式。这使得我们可以“打包代码并且在许多互不相关的地方和情况下复用。”

	.calendar-widget {
	  @extend %block;
	}
	.calendar-widget-title {
	  @extend %block-header;
	}
	
	/*...*/
	
	.latest-blogs {
	  @extend %alt-block;
	}
	.latest-blogs-title {
	  @extend %secondary-header;
	}
	
	/*...*/
	
	.latest-news {
	  @extend %alt-block;
	}
	.latest-news-title {
	  @extend %secondary-header;
	}

####编译后的CSS
在编译后的CSS中你会看到静态的extend```%secondary-header```被替换成继承它的两个类。你也会注意到我们从来没有停止使用```%primary-header```，所以那些样式被省略了。这是静态扩展的好处之一。
	
	.latest-blogs-title,
	.latest-news-title {
	  font-size: 2.2em;
	  line-height: 1.1;
	  color: #8cc5e6;
	  margin: 0 0 .3em;
	  padding-bottom: .2em;
	  border-bottom: 1px solid black;
	}
	
	.calendar-widget-title {
	  font-size: 2.2em;
	  line-height: 1.1;
	  color: #fd7900;
	  margin: 0;
	  padding: .3em;
	  background: #8cc5e6;
	  margin: 0 -15px;
	}
	
	.calendar-widget {
	  border: 1px solid #8cc5e6;
	  padding: 0 15px;
	}
	
	.latest-blogs,
	.latest-news {
	  padding: 15px;
	  background: #eee;
	}

![](http://ivanctoe.qiniudn.com/uaa-6.png)

####单一来源的样式表

在这个CSS中我们发现```.latest-blogs-title```和```latest-news-title```很像并且我们通过结构把它们联系在一起。

![](http://ivanctoe.qiniudn.com/uaa-7.png)

####这会使得我们的CSS膨胀吗？
通常关于extends的抱怨是它比其他方法产生了更大的CSS文件。OOCSS或BEM的方法会像我们上述做的一样除了把```.alt-block```和```.secondary-header```类直接应用到标签上而不是通过Sass继承。当然这个方法会让我们节约一些比特，这是extends的好处，但是对于一个项目的长期发展来看，这样的好处远大于重复带来的影响。Ben Frain几周前做出了很好得[总结](http://benfrain.com/enduring-css-writing-style-sheets-rapidly-changing-long-lived-projects/)：
> 对于我来说，CSS的代码库越大，组成的组件在很多方面与其他互相隔离，这有利于更小的由互相依赖和本质相关样式组成的CSS代码库。

只要我们将这些表象类直接添加到我们博客和新闻标题的标记上就会变得互相依赖并且本质相关。也就是说，我们不能改变它们中的一个而不改变另一个。

###旧容换新颜
我没有传统的程序员背景，所以这是我第一次有机会深入研究继承和结构间的区别。讨论这样一个在类似的Java和C++语言下的话题，我经常发现我阅读的文章大部分像网页本身一样过时！最令人惊奇的是它们几乎100%有重大意义甚至是16年以后。摘自“[继承与结构：你应该选择哪一个？](http://www.javaworld.com/article/2076814/core-java/inheritance-versus-composition--which-one-should-you-choose-.html)”

> “在一个继承关系中，超类通常被认为很“脆弱”，因为在超类上做一个很小的改变会有连带作用并引起应用代码中其他很多地方的改变。”

这是我们确实碰到的问题，当我们改变```h2```时会引起```.block h2```的改变并且引起代码的回滚。

这些点子并不是新的，但是随着网页的成熟，以及项目复杂性的增加，它们和我们的行业愈发相关。不管是对我还是我的代码来说，我将花更多的时间来阅读其他的语言，那些语言在12年前也发生过我们现在面对的那些相似的问题。在[这里](http://phase2technology.com/?s=css)阅读更多Phase2对于CSS的想法。
