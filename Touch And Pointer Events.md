##触摸和点击事件

回到2007年苹果发布了第一个真正的触摸屏浏览器，它同时引入了触摸事件来监控用户的触摸动作。大多数其他浏览器厂商纷纷效仿，除了微软，它自己发明了点击事件。本章将讨论这两个事件。

W3C同时推荐了触摸和点击事件，所以连个事件都是web标准。他们分别可以在[http://smashed.by/mwhb8](file:///D:/translate/%E7%BF%BB%E8%AF%91%E5%B0%8F%E7%BB%84/the-mobile-web-handbook/mwhb8)和[http://smashed.by/mwhb9](file:///D:/translate/%E7%BF%BB%E8%AF%91%E5%B0%8F%E7%BB%84/the-mobile-web-handbook/mwhb9)被找到。

然而，看起来W3C正在远离触摸事件而偏向点击事件。创立触摸事件规则的Web事件研究小组已经解散了并且规则的研究已经终止，然而点击事件研究小组依然运行。W3C正考虑从把点击事件变成标准。

Google和Mozilla正致力于实现点击事件-也许你读这篇文章的时候他们已经完成了。在[http://smashed.by/mwhb10](file:///D:/translate/%E7%BF%BB%E8%AF%91%E5%B0%8F%E7%BB%84/the-mobile-web-handbook/mwhb10)查看Chrome的讨论以及在[http://smashed.by/mwhb11](file:///D:/translate/%E7%BF%BB%E8%AF%91%E5%B0%8F%E7%BB%84/the-mobile-web-handbook/mwhb11)查看Firefox的讨论。

虽然第一感觉点击事件也许看起来是IE-is-different-just-because的例子，情况并非如此。微软正在创建一个有趣值得我们长期讨论的哲学问题。当Google和Mozilla正考虑实现点击事件时，W3C也正将触摸事件转换成点击事件。

在大多数方面，触摸和点击事件是传统的JavaScript事件。它们在触摸动作发生时触发，你可以在它们上面绑定事件，它们的事件对象会提供关于触摸的实用信息。另外，由于可以双向切换，触摸设备必须触发鼠标事件因为许多网页依赖它们。但是当你没有鼠标的时候如何在设备上触发鼠标事件呢？这一章部分内容将讨论这个问题。

这一章其他的部分大多关于哲学问题。和iPhone一起，Apple引入了一种全新的交互方式，触摸，现在正和传统的鼠标键盘交互的方式共存。Web开发者必须保证页面可以在三种方式下运行。第一感觉触摸事件看起来和鼠标事件非常像。它们之间有什么区别呢？我们需要对不同的交互模式分离不同的事件吗？

###触摸事件
让我们从触摸事件开始，它们比点击事件支持更广泛。随后，我们会发现点击事件非常相似。有四种触摸事件：
1. `touchstart`，当用户的手指触摸到屏幕时立即触发。
2. `touchmove`，当用户移动手指时持续触发。
3. `touchend`，当用户手指离开屏幕时立即触发。
4. `touchcancel`，含义基于浏览器。随后讨论。

![](images/ch06-01.png)

大多数触摸屏浏览器支持这些事件，除了IE。一些其他的老式浏览器例如Symbian Anna的默认浏览器也不支持。代理浏览器也不支持因为这些事件不适合代理浏览器模型。我们已经在第二章中讨论了原因。

###touchcancel
我承认我不理解`touchcancel`事件。它在触摸序列取消时被触发，但它的意义很大程度上取决于每个浏览器。例如，Chrome在用户触摸手指离开屏幕时触发，但大多数其他浏览器不是这样。

幸运的是，我从来没有找到一个用这个事件的好理由，而且脚本和库也很少用`touchcancel`-它们都把它和`touchend`等同并且只是以防万一才引入它。因此，这一章会忽略`touchcancel`事件。如果你因为浏览器在特定情况下不能触发`touchend`而遇到了奇怪的问题，你也可以把`touchend`事件绑定到`touchcancel`事件。

###手势事件
除非触摸事件，IOS下的Safari同时引入了`gesturestart`,`gesturechange`和`gestureend`事件，IE有一些相似的事件。手势事件被定义成同时发生两个或多个触摸时间。

这些事件有两个问题：其他浏览器都不支持，因此它们很鸡肋。理论上来说检测用户手势非常棒，但是在实践中你必须通过动作协调计算出用户到底想要完成什么动作并且它们如何随时间改编。我们不需要手势事件因为：传统的触摸事件能提供相同的信息。因为这些原因手势事件并不重要并且这一章不会谈及它们。

###其他事件
一开始，触摸事件说明包含了`touchenter`和`touchleave`事件，当用户触摸或者离开一个特定元素时触发。它们从来没有实现，虽然IE支持微软的选项。既然这些事件是一个好点子，我们希望它们会被恢复。在特定的界面它们很实用因为可以知道用户的手指是否划入或者划出一个元素。

我们可以做的是`zoom`事件在用户缩放（或者，停止缩放）时被触发。我从2010年开始谈这个，但是到目前为止都没有人听。另外，知道用户是否缩放很实用-也许你想要改变一小点界面内容，或者你只是想要选中缩放数据来检测你的字体是不是太小。

###脚本例子
我们将使用三个脚本例子来展示相比较鼠标和键盘事件的触摸和点击事件。学习它们同时也会促使你思考交互模式以及如何把基于鼠标的效果引入到触摸中去，反之亦然。

###下来菜单
第一个例子是经典的老生常谈：下拉菜单。不管是否喜欢，在网页中它无所不在，它是一个非常好的脚本例子因为它包含了许多的事件处理的关键性部分。

![](images/ch06-02.png)

通常，下拉菜单配合鼠标工作。用户把鼠标指针悬浮在一个项目上菜单展开。用户移开鼠标指针，菜单闭合。它也可以和键盘配合：用户用键盘切换到项目时，当它获取焦点时（`focus`事件），菜单展开；如果焦点移除（`blur`事件），菜单闭合。这比鼠标效果更难实现，但这是可能的。

但是我们如果把下拉菜单引入到基于触摸的交互情况中呢？用`touchstart`替换`mouseover`以及用`touched`替换`mouseout`并不奏效。触摸一个项目展开菜单；并没有问题。但是一旦菜单展开了，用户想要点击特定的链接。他们移开手指然后菜单闭合了。这不奏效了。如果我们离开菜单时触发`ontouchend`，那菜单什么时候闭合呢？

跨设备环境的最好的解决方案是使用`click`事件。`Click`而不是`mouseover`，展开菜单，点击另一个菜单项会再次关闭它。如同我们随后会在这一章看到的，`click`事件非常安全可靠，另外下拉菜单在鼠标和触摸模式下都表现良好。

移动浏览器必须和成千上万的基于`mouseover`的下拉菜单作斗争。幸运的是，Apple在设计触摸事件集合时已经把下拉考虑成一个特殊的使用情况，所有其他浏览器都效仿了它的解决方案，我们会在这一章的后面再次讨论。

###拖放
![](images/ch06-03.png)

关于下拉菜单的两面是拖动和放下脚本。用户点击一个元素(`mousedown`)，把它拖到其他地方(`mousemove`)，然后放下(`mouseup`)，在这后脚本计算出如果现在的区域是有效的放置目标，然后基于输出做一些事情。

把这个引入到触摸情况中非常简单：只要确保`mousedown`替换成`touchstart`，`mousemove`替换成`touchmove`，`mouseup`替换成`touchend`。这样表现良好，唯一的小问题是找到用户的协调点。我们可以随后再讨论。

这里的问题是键盘。你如何让键盘用户移动一个可拖拽的元素呢？你可以让一个区域成为一个元素可用键盘选中的区域，一旦用户选中它你就开始监听方向键。技术上来说这并不难，但是用户体验上恰恰想法。这个问题基本没法解决：人们默认观念上觉得拖放是基于鼠标或者触摸的，而不是键盘。

如果你很困惑，这里有一段脚本把拖放引入鼠标和键盘的。我很久以前写的：[http://smashed.by/mwhb14](file:///D:/translate/%E7%BF%BB%E8%AF%91%E5%B0%8F%E7%BB%84/the-mobile-web-handbook/mwhb14)。键盘拖放很不直观，我还没找到一个更好的解决方案。把触摸事件添加到这个脚本里非常简单，作为你的一个小练习。

###层级滚动
在2011年我需要一个可以在所有设备上使用的水平滚动元素。回到那时候，这需要一个脚本，所以我写了一个。同时，原生的滚动已经改进了，已经不需要这样的脚本了；我们在CSS一章中已经谈及。但滚动脚本依然是一个很实用的例子，所以我们还是需要讨论一下。
![](images/ch06-04.png)

写这个滚动脚本本身不是一个问题。`ontouchstart`，计算滚动元素现在的位置并且初始化其他的事件处理器；`ontouchmove`，滚动元素和触摸移动的距离相同的像素；`ontouchend`，运行一个特定的函数来计算出一个交互友好的减速，一个元素停止函数也性质。这个很简单，只花了我大概两个小时。

但是如果是在没有触摸的设备上呢？为了让它生效我需要把交互方式从触摸切换到鼠标和键盘。键盘很简单，我只要监听`keydown`事件，当用户使用左右键时滚动元素。这也许不容易发现（我讨厌解释这些功能所以从来不提它），但是现在脚本支持了键盘。

但是鼠标呢？从技术上说，通常在脚本中添加`mousedown`，`mousemove`和`mouseup`事件。但是交互方式很奇怪。用户需要按下鼠标在元素上移动来滚动元素。这和拖放的交互方式是一样的，但是在层级滚动的例子中很不直观。

我可以使用过时的左右箭头来滚动元素，当鼠标移到箭头上时发生滚动脚本，但是视觉上会很混乱。另外，当用户使用触摸或者键盘时我需要隐藏箭头，但是我没法安全和正确得实现这个功能。(我们之后会回到这个问题)。最后，我决定不创建鼠标交互方式。

###事件以及交互模式
回到1996年网景引入了鼠标事件和著名的鼠标悬浮效果，web开发者发现它非常好。然后专家说话了，指出有些人不用鼠标，所以浏览器也需要键盘事件。一些web开发者实现了它，从那之后他们同时兼容两个交互方式：鼠标和键盘。随后Apple加入了触摸的交互模式，把整个交互模式的数量变成了3个。

Web开发者必须确保页面在三种交互模式下表现良好。有时候很简单，有时候很难，但总是必要的-并不只是现在的网页，同时在思考如何改变一个UI元素在不同模式的交互上也必要的。我希望我对于脚本例子的注释能呈现给你如何思考这些问题。

未来我们没有理由不诞生更多的交互模式。例如Xbox Kinect，把身体移动转换成屏幕动作，你可以使用手来操纵屏幕的光标。技术上说，操纵光标意味着使用鼠标事件，但是从用户角度来说这算一个新的交互方式。总体来说它感觉上不同。

汽车，冰箱，穿戴设备和任何其他类型的新型设备也许给用户带来全新的交互方式以及网页开发者`doorclose`事件，任何人想过这个吗？（事实上，发明新的JavaScript事件对于发布大会是一个很有意思的游戏。）

试想一下交互模式以及JavaScript事件引发的三个问题：

1. 每个交互模式需要独立的事件吗？
2. 设备是否会支持遗留交互模式的JavaScript事件即便它们在设备上没有意义。
3. 你如何确定设备支持哪些交互模式，或者用户正在使用哪种交互模式？

到现在为止，答案是，是，是，已经实现了。第一个答案在未来也许会变成否定的。在一次看一下Kinect的例子：我们需要全新的`handwave`事件吗，还是使用点击和鼠标事件？技术上说，光标就是光标，不管用户怎么移动它。

###等效事件

到现在为止，每个交互模式都有自己的一系列事件。事实上，特定的事件间有联系。下列表格给出了一个大概的表示。
![](images/ch06-table-01.png)

显而易见，触摸序列`touchstart`-`touchmove`-`touchend`类似

……

###touch的不同
所以事件之间有时候是等同的，这要取决于内容，但是触摸，按键和鼠标事件不是完全相同的。键盘是三者中最特别的，web开发者倾向于专注鼠标和触摸事件，让我们来谈一下它们之间的区别。

当鼠标焦点移动到一个元素上，或者用户点击了鼠标，立马非常清晰的表现出下面要发生的事情以及要触发什么事件。触摸事件并不是这样：它们通过含义来重载。当你手指触摸到屏幕的那一刻，系统和浏览器不知道接下来会发生什么。你想要展开一个元素？或你想要双击？浏览器必须在给触摸事件分配意义之前等上一会儿，这个间隔是明显的。我们下面会再次讨论这个问题－oh不，我们会么？

可能会同时发生多个触摸操作。这在鼠标动作里是不可能的：一个电脑只有一个鼠标。通常来说，这并不要紧：许多页面只支持单点触控的交互方式，这方便用鼠标来模拟。即使在一个页面中有两个幻灯片，你不会同时和两个进行交互，如果用户同时滚动了两个你也把它们当作独立的系统，每个系统在触摸和鼠标模式下都会运行良好。

当一个页面允许或者需要多点触控的交互方式，事情发生了改变。如果有一个脚本把同时发生的若干个触摸操作转换成一个手势，比如旋转或缩放，这些效果不能用鼠标模拟。这个问题的难度取决于页面和使用情况，但是清楚这一点非常重要。

触摸事件比鼠标事件精度要小。鼠标光标总是点击到精准的一个像素，而触摸也许会有几个像素的重叠。通常，系统计算触摸的中心像素作为基准来计算坐标，并且容许你在`touchstart`和`touchend`间移动手指中的一定误差－但是随着而来的是不这样做的浏览器如果一个噩梦。

![图]()
*“A mouse cursor moving from A to B will pass through the central element. A touch will not; the user has no need to touch the central element.”*

触摸事件是间断的而鼠标事件是连续的。当你把鼠标光标从元素A移动到元素B的时候你必须要经过它们之间的所有元素。鼠标事件是连续的并且可以通过一段脚本追踪。但是当你通过触摸把A移动到B时，你通常释放A并且触摸B而不用处理它们之间的元素：触摸移动是间断的。事实上，这是当我们把下拉菜单引入到触摸事件中时要面对的问题。下拉需要连续的事件因为它们最初的只考虑了只有鼠标的情况。

触摸事件比点鼠标事件包含更多的信息。例如，触摸屏设备也许可以提供你的手指温度，触摸的半径以及你施加的压力等信息。它们现在并不是这样做，但是将来也许会发生改变－尤其是因为一些众所周知的ie点击事件中的可用隐藏属性。

总之，为希望你明白鼠标和触摸事件很相似，但是不是完全相同。

###合并触摸和鼠标？
我们已经发现鼠标和触摸通常非常相似，但还有一些很小但是有时候非常重要的区别。我们需要这个背景知识来理解微软的点击事件以及视窗的观点。

微软的观点是鼠标和触摸不需要分离的事件。因此，当用户通过光标做出改变时点击事件就被触发－光标可以是鼠标光标，触摸或者一支笔（或唱针）。所以下图是微软处理事件相似性的做法：
![图]()
*“Event equivalents according to Microsoft”*

我们现在有两个基本完全不同的方法：苹果的方案，鼠标和触摸完全分开；微软的方案，鼠标和触摸成为一体。到现在为止，只有IE支持微软的模型，其他浏览器都支持苹果的模型。正如我们所知，Mozilla和Google正考虑实现点击事件，所以未来这个情况也许会改变。

![图]()

*“The Microsoft Surface is a touchscreen tablet, but you can attach a keyboard with a trackpad. You can switch between mouse and touch while using a website, and that’s a use case addressed by pointer events.”*

Google考虑点击事件的原因很有趣。像微软的Surface平板一样，Chromebook Pixel带有触摸屏的同时自带带有trackpad的键盘。因此，两个设备都允许你使用鼠标和触摸事件作为交互方式，并且甚至在两者间切换。网页需要同时追踪两种事件，把它们合并成一个系列时这会变的更加容易。

微软是否有一个好的解决方案呢？个人来说，我倾向于是有的。随着时间推移，越来越多的设备会同时存在鼠标和触摸的交互方式，点击事件是长远考虑。同样的，它们很容易被扩展来支持其他的交互方式。现在的点击事件可以通过笔（或者唱针）来实现，并且不仅仅是当笔触摸到屏幕，你也可以通过Wacom平板或者类似的来实现。在未来，它们可以非常方便的包括移动的TV遥控器或者Kinect手势来模拟光标并且激活元素例如一个链接。（然而这样也许会走出舒适区。）所以点击事件被证实比独立的鼠标和触摸事件在未来更加用户友好。

让我们尝试一下在我们的三个脚本例子中实现点击事件：

1. 拖放是一个完美的融合。不论用户是使用鼠标或触摸，或甚至一支笔，他们都能拾起一个元素，拖动然后放下。点击事件一定会增加拖放脚本的未来友好性，因为看起来我们不需要为Kinect,电视遥控器或者其他类似的类点击交互的方式增加任何代码。
2. 滚动层可以通过点击事件来实现。在触摸的交互模式中它表现良好。当使用一支笔时，用户会把笔按在层上，滚动，然后释放。这也行得通。鼠标交互类似于笔，但是通过鼠标按键来拾起元素感觉很奇怪，这就是为什么我觉得这个效果很难引用到鼠标上。这个问题一直存在不管我们使用分离的鼠标和触摸事件或者一体的点击事件，所以点击事件不会造成任何问题。
3. 下拉菜单是最复杂的例子。`pointerover`和`pointerout`看起来很适合这个例子，但是事实证明并不是（原因如下）。下拉在触摸的交互方式下表现并不好，从触摸转换成点击事件并没有改变多少。在触摸屏幕中处理下拉的最好方式是`click`事件。

例子显示出当一个交互方式不是专门为某一个交互模式定制时点击事件的表示是最好的，事实上，`pointerType`属性，我们后面会讨论到，会告诉你正在处理时什么类型的点击，如果愿意的话，你可以分开处理鼠标和触摸。（这个属性违反了点击事件的理论，但是实际上它很必要。）

###鼠标覆盖/点击覆盖问题

`Pointerover`取代了过时的`mouseover`事件以及我们称之为“`touchover`”的事件：用户的触摸，已经发生在屏幕上，作用于一个特定元素。`Pointerout`实现了相同功能，但是当用户手指或者光标离开元素时。将会是`:hover`问题我们在CSS一章中谈论了但是是以JavaScript形式。

再一次我们遇到了连续和间断事件之间最根本的不同。当我们用鼠标把A移到B，用户没有选择只能进入再离开所有的中介元素。然而当触摸时，用户可以先触摸A然后B，他们不这样做的唯一理由是因为他们已经拖动了一些东西。`Pointerover`在这样情况下很有用：用户进入的这个元素是有效的拖动目标吗？

除了这个设想，`pointerover`从本质上和`mouseover`不同，细微的`mouseover`效果，尤其是显示额外信息，不能在触摸屏上生效因为在这样的情况下用户触摸不能从其他地方进入一个元素。作为替代，用户可能触摸到元素而没有预先的`pointerover`，所以额外信息不会显示。

这里的情况需要`mouseover`和`mouseout`，它们会在触摸交互中被触发，而不是当用户的触摸进入或者离开一个元素。我们随后会讨论细节。然而，这个解决方案依然不完美因为在触摸环境中悬浮依然格格不入。

###输入渐进增强
非常感谢Jason Grigsby使我脑子中的概念变的清晰。我从他那里借鉴了*输入渐进增强*这个术语，以及这一章节中若干关键想法。

跟相应式设计教导我们针对多屏幕尺寸设计一样，我们需要针对多种输入模型进行设计。让我们现在称之为*输入渐进增强*。不幸的是，输入渐进增强和响应式设计分割并不清晰。

响应试设计基于一个设计可以自适应所有尺寸的屏幕的观点，许多例子中输入渐进增强要求我们对于不同的输入模型写单独的脚本－看，到现在为止，对于滚动层模型，本质上需要三段独立的脚本来处理鼠标，键盘和触摸。

另外，通常屏幕尺寸在用户进行交互时不会发生改变，但是输入模型会改变。微软Surface平板用户也许开始使用鼠标，切换到触摸，又切换回鼠标，而没有离开页面。你的代码需要处理这个情况，是的，这非常复杂。

通常，这对于平板很重要，对于智能手机没那么重要，因为用户没有那么多输入模式的选择。然而，考虑用户与一个页面交互时只使用一个特定的输入模式是一个集体幻觉。这让我们作为web开发者的工作更加轻松，但是对于混乱的现实没有意义。
![图]()
*“This is the most restrictive input mode, and it would be a good idea to start designing your interactions here.”*

响应式设计教会我们一件或者更多关于输入渐进增强。让进行响应式设计时，从最受限制的使用情况开始是一个好点子：最小的屏幕。输入渐进增强会产生一样的效果。最受限的使用情况基本是D-pad，通常带有四个方向键以及中间一个OK或回车键。好消息是D-pads通常触发按键事件并且和通常的键盘使用相同的方向和回车按键代码，这意味着把D-pads和常规键盘区分是没有必要的。坏消息是他们仍然非常受限。

最坏的消息是没有任何的指南可以分享。输入渐进增强太新颖所以我们还没有找到所有情况都奏效的策略，甚至是帮助你深入的清晰的点子都很少。你可以把这个当作一个问题，或者一个挑战。谁知道呢，也许是你教会这个世界如何实现输入渐进增强。

###查明当前交互模式

也许，输入渐进增强需要你查明用户当前的交互模式。技术上来说这是可能的（虽然非常困难），但是真正的问题在于它会给出什么样有用的信息。

再次用微软的Surface平板用户作为例子。你可以查明用户目前是使用鼠标。但是这意味着他们会在整个过程中持续这样做吗？并不是。事实上，很有可能他们至少偶尔会用键盘或者触摸。或者他们也许会移除键盘（以及鼠标trackpad）然后只用触摸。如果其中任何一个情况发生了，你的交互模式侦测的值是什么？

唯一你可以确定的事情是当用户在一个特定的模式下开始一个特定的行为，他们不会中途切换。所以如何你侦测到用户正在使用鼠标拖放，他们不会在拖放中切换到触摸。但是当拖放完成后，用户也许会选择切换到触摸在进行下一个行为－或者坚持使用鼠标，或者甚至换成键盘。

你要做的最重要的事情是确保你所有的交互工作适用所有的交互模式。拖放适用于鼠标，触摸和甚至键盘。一旦你确保了这一点，用户使用哪个交互模式就无关紧要了。

但是我们假设查明现在的交互模式很有必要。也许你需要统计用户最喜欢用哪个模式。所以让我们考虑一些例子：
* 点击事件是最容易的：它有一个`pointerType`属性，值可以是`mouse`，`touch`或者`pen`。查询当前值你就可以知道用户在做什么。
* 另一个简单的方式：如果任何按键事件被触发，那么用户一定在使用键盘。这并不涉及任何一种未来的交互方式－用户也许在任何时候切换到鼠标或者触摸。它还是提供了一些有用的信息。
* 类似的，如果一个触摸事件被触发了你可以确定用户正使用触摸交互模式。再一次，这不涉及未来的交互方式，但这仍是一些信息。
* 看一下鼠标事件：当用户触摸屏幕时它们也被触发，因此不适合用来侦测交互模式。侦测鼠标使用的方案是排除所有其他的交互模式。如果用户没有使用触摸或者键盘，很有可能他正使用鼠标。

有多种侦测触摸交互模式是否可用的方法。Modernizr库中有一个受欢迎的方法，但不幸的是还不是很可靠，方法如下：
```
“var hasTouch = !!('ontouchstart' in window)”
```
如何`window`对象有一个`ontouchstart`属性那么浏览器支持触摸事件并且我们可以安全使用它们。至少，你会这么想。虽然第一个结论是正确的，支持触摸事件的浏览器不一定要运行在触摸屏设备上。例如，黑莓6浏览器，即便运行在一个无触摸的设备上但支持触摸事件。老版本的Chrome也有相同的问题。并且依赖`touchstart`完全排除了IE。

唯一安全侦测触摸的途径是查看一个真实的触摸或者点击事件是否被触发。只有这样你才能确保浏览器支持触摸并且用户正使用它。
```
“var hasTouch = false;
document.ontouchstart = function () {
    hasTouch = true;
}
document.onpointerdown = function (e) {
    if (e.pointerType === 'touch') {
        hasTouch = true;    
    }
}
”
```

这最好是一个接一个侦测交互模式并且看一下你是否发现了任何有用的事。从点击事件开始，因为`pointerType`属性也许会给你一些不实用的信息。然后侦测触摸事件，原因我们会稍晚解释，触摸行为也会触发鼠标事件，所以鼠标事件只有在触摸不算的情况下才算。按键最后－不是任何本质问题而是因为它们需要去一些地方。你可以做如下的一些事：
```
“var interactionMode;
document.onpointerdown = function (e) {
    interactionMode = e.pointerType;
}
document.ontouchstart = function () {
    if (!interactionMode) {
        interactionMode = 'touch';
    }
}
document.onmousedown = function () {
    if (!interactionMode) {
        interactionMode = 'mouse';
    }
}
document.onkeydown = function () {
    if (!interactionMode) {
        interactionMode = 'keyboard';
    }
}”
```

运行这个检查的理论情况时登陆屏幕或者类似的用户知道他们必须和页面交互的地方。当用户登录时，你使用类似上述的脚本来侦测他们在用哪个输入模式。再一次，这并没有告诉你任何关于用户在页面上整个交互过程的信息；只是关于他们和登陆屏幕交互时的信息。但是这依然是一些信息，并且这些信息可能有预见性的控制力。

这个方法依然没有办法预见用户接下来要使用什么交互模式。到现在为止最好的处理不同交互模式的方法需要代码来确保鼠标，键盘和触摸用户都可以使用你的界面。

###触摸行为事件流
一些关于我们都知道的我们正在讨论的事情的定义：

行为
    用户产生一个行为；立即，触摸一个元素或者点击。

事件
    触发一个特殊的JavaScript事件来反馈用户的行为。

事件流
    触发一系列特殊的JavaScript事件来反馈用户的行为。特别是，单词点击行为，引起了一长串事件流。

事件处理
    当特定事件触发时执行的一个JavaScript片段。

所以一个触摸行为导致触发了一系列事件流，并且你可以在它们中的一个或者更多上绑定一个事件处理器。（我建议你规范你自己在每个流上绑定一个事件。）

这是很多理论上的东西。让我们进入到实践部分。下面的一部分将会调查触摸事件的几个方面，它们中的大多数也适用于点击事件。这一章的结尾是点击事件的一个正式介绍。

当`touchstart, touchmove, touchend, pointerdown, pointermove`和`pointerup`触发时，这很清晰。不清楚的是如何处理鼠标事件。虽然它们在纯触摸屏设备上没有意义，它们对于许多网页还是极其重要的，甚至触摸屏浏览器也应该触发它们。

这就是为什么所有浏览器在触摸事件后立即触发鼠标事件。这引起了*触摸行为事件流*：当用户进行触摸行为时一系列的事件被触发。确切的哪个事件被触发取决于用户行为，也取决于浏览器。

###单击行为
当用户单击一个元素，以下事件被触发：
1. `touchstart/pointerdown`
2. `touchend/pointerup`
3. `mouseover`
4. 一个`mousemove`
5. `mousedown`
6. `mouseup`
7. `click`
8. 如何加在这个元素上的`:hover`样式

确切的事件顺序没有被设置。例如Android Webkit4，在`touchstart`事件之前触发`mouseover`和`mousemove`。老的黑莓，以及诺基亚的塞班Webkit，在流结束的时候触发`touchend`而不是在开始时。所有的这些区别并不重要。总的来说，你只给这些事件中的一个创建事件处理，当用户触摸屏幕时这个处理器就会被执行，不管你使用哪个一个事件。这只有在你使用几个鼠标事件时你才需要考虑这个问题。解决方案是在大多数情况下使用一个鼠标事件。

当用户虽然单击另外一个元素时，`mouseout`事件在最初的元素上被触发并且任何`:hover`样式被移除。当用户随后点击相同的元素，整个事件流再次触发，除了`mouseover`。显然，浏览器假定鼠标（像上一次一样）已经在元素上。这通常没有意义。但是这是最差的方法在触摸屏上实现mouseover内容。
![图]()
*“The traditional drop-down menu opens `onmouseover` and closes `onmouseout`.”*
![图]()
*“When the user touches the drop-down menu, the `mouseover` event fires in the cascade and the menu opens. When the user removes her touch, though, the `mouseout` event does not fire and the menu stays open. This is deliberate: the user can now touch one of the links in the menu. Touching an element somewhere else on the page fires the `mouseout` event on the drop-down menu, and it closes.”*

例如下拉菜单：用户触摸菜单项；事件流被触发，包括`mouseover`；当展开子菜单时脚本再次执行。现在用户触摸了页面上的其他东西：`mouseout`事件被触发，子菜单收回。这和用鼠标进行交互时不太一样，但这是触摸屏浏览器能做到的最好的程度。

###其他行为
当用户进行除了单击之外的一些其他行为时，事件流变的非常不同。`touchmove`和`pointermove`事件现在参与进来，变成了交互特有事件例如`scroll`和`resize`。鼠标事件被禁止。理论上，如果用户滑过一个下拉菜单项，它不会展开因为`mouseover`没有被触发。

当用户在桌面浏览器上右击时`contextmenu`被触发。

###Safari: 取消流
Safari有两个奇怪的地方:
1. 如果`mouseover`或`mousemove`改变了某一内容，Safari取消其余的事件流并且不触发`mousedown`,`mouseup`和`click`事件。有两个问题，为什么是`mouseover`和`mousemove`？内容改变是什么意思？

###Safari：鼠标事件冒泡
Safari另一个很奇怪的地方时鼠标和点击事件只在特定的情况下冒泡到文档中。所有浏览器中在流中的事件都要冒泡除了Safari。鼠标和点击事件只在下述情况中冒泡：

1. 事件的目标元素时一个链接或者一个表单区域
2. 目标元素，或者它任何祖先元素但是不包括<body>，有对鼠标事件设置了明确的事件处理。这个事件处理可以时一个空函数。
3. 目标元素，或者它任何祖先元素有一个`cursor:pointer`的CSS申明。

如果想要结束鼠标或者点击事件，只要如下代码：
`targetElement.onclick = function () {}`

###解析一次点击
触摸事件流中最重要的事件时`click`事件。当激活一个元素时触发；`click`事件不管你如何激活这个元素。
`click`这个名称不太恰当，这个事件应该叫`activate`事件。它之所以有现在的名字是因为它是由鼠标事件衍生出来的。所有现在和未来的浏览器都支持`click`事件。
需要在触摸屏设备上注意两个问题：
1. 臭名昭著的延迟
2. 罕见的难易触发某个元素的`click`事件

####300毫秒
点击一个元素后有300毫秒的延时。这个问题理论上来说无法解决。因为浏览器不知道用户接来下想要进行什么操作，所以只能等待一段时间。
关于这个问题的概述以及几个解决方案可以在[](http://smashed.by/mwhb12)找到。
尤其双击是一个问题。当你的手指离开了屏幕后是要继续点击屏幕呢还是应该触发单击事件呢？当页面不可缩放时很多浏览器去掉了这个延迟。但是禁止缩放又是不好的。
Chrome有一个非常有意思的方法，如果用户通过`width=device-width`设置了meta viewport。Chrome就认为双击不会发生。并且移除了延迟。这是我听到最好的解决方案。IE下你可以通过`touch-action: manipulation`禁用延迟。唯一不会禁用延迟的是Safari。因为在IOS中双击也是滚动命令。

####相同像素
在桌面端，`click`事件在`mousedown`和`mouseup`事件发生在同一个像素上时被触发。因为鼠标总是点击一个像素。但是在触摸屏上你的手指会选中一块像素，所以`touchstart`和`touchend`事件不是在一个地方发生所以有的浏览器认为`click`事件没有发生。好的浏览器是给用户一定容差的，它们允许用户手指偏差4到20个像素。你经常会在测试版浏览器里碰到这个问题。

###分离触摸事件
如果你在监听触摸或点击事件，你想要了解更多。你需要深入挖掘事件对象：
```
var el = [an element];
el.addEventListener('touchstart',handleTouch,false);

function handleTouch(e) {
    // e refers to the event object
    // e.type gives the event type
    // e.target gives the event target
    // return false or e.preventDefault() prevents
    // the default action
}”

`Type, target`，并且组织默认行为像其他事件一样。你需要从一个标准的`return false`或`e.preventDefault()`开始。

####触摸列表
触摸事件对象把每个独立的触摸对象存到`touchList`数组里。有三个touchList：
* `touches`：整个屏幕中现在激活的触摸列表。
* `changedTouches`：一系列如果改变会触发触摸事件的触摸。
* `targetTouches`：在事件目标上发生的一系列触摸。

####找到事件坐标
下列函数用来找到事件发生的坐标：
```
function handleTouch(e) {
    // use pageX/Y instead of clientX/Y if necessary
    var touch = e.changedTouches[0];
    var coorX = touch.clientX;
    var coorY = touch.clientY;
}
```
```clientX/Y```按照视口viewport的左上角来计算而```pageX/Y```按照布局viewport来计算。
IE不支持`touchLists`。
跨浏览器支持的代码如下：
```
function findCoordinates(e) {
    // use pageX/Y instead of clientX/Y if necessary
    var x,y;
    if (e.changedTouches) { // touch events
        x = e.changedTouches[0].clientX;
        y = e.changedTouches[0].clientY;
    } else {        // pointer or mouse events
        x = e.clientX;
        y = e.clientY;
    }
    return [x,y];
}
```

####离开元素
即使禁用了`touchstart, touchmove`和`touchend`，当手指离开屏时`touchmove`或者其他浏览器里是`touchend`还是会触发。所以`touchenter`和`touchleave`很有用。

####禁用默认值
通过返回`false`或`calling event.preventDefault()`可以取消默认事件的动作。
第一个需要注意的地方：一些浏览器没有按照默认的取消浏览器的手势。
如果你禁用默认的`ontouchstart`，浏览器认为你不想要默认行为，所以默认的行为被禁用了。
最复杂的一小部分内容是区分`touchstart`和`touchmove`。
1. 只有`touchstart`：敲击（点击），双击，持续触摸和事件流。
2. `touchstart`或`touchmove`：滚动或者缩放。
点击事件不支持`preventDefault()`。只能通过CSS`touch-action`申明来禁用。

####例子：水平和竖直滚动
水平滚动滑动应该引起一个元素的滚动，垂直滚动应该引起整个页面的滚动。处理的方式如下：
```
document.ontouchmove = function (e) {
    // origin[] has the coordinates of the touchstart
    var currentPos = findCoordinates(e);
    var newPosX = (currentPos[0] - origin[0]);
    var newPosY = (currentPos[1] - origin[1]);
    if (Math.abs(newPosY) > Math.abs(newPosX)) {
        returnValue = true;
    } else {
        returnValue = false;
        // pos is the element's X-coor when the
        // scrolling started
        newPosX += pos;
        // min and max are the pre-calculated
        // minimum and maximum scroll
        if (newPosX <= max && newPosX >= min) {
            layer.style.left = newPosX + 'px';
        }
    }
    return returnValue;
}
```

###点击事件
IE11对于点击事件的支持如下：
![图]()
`pointerenter/leave`和`pointerover/out`之间的区别和`mouseenter/leave`和 `mouseover/out`之间的区别一样。
触摸和点击事件在这些地方不同：
1. 在写本书的时，点击事件只有IE支持，虽然Chrome和Firefox正考虑实现。
2. 点击事件需要MS前缀，在IE10中需要驼峰命名。
3. 点击事件没有`touchLists`；事件坐标存在事件对象本身，和鼠标事件一样。
4. 不能用JavaScript来禁用点击事件默认的行为。

####命名和前缀
在IE中点击事件是带前缀的，有时候是驼峰命名。
例如如下代码：
```
el.onmspointermove = doSomething; 
    // lowercase; IE10 and IE11
el.onpointermove = doSomething; 
    // lowercase; IE11 only
el.addEventListener('MSPointerMove',doSomething,false); 
    // camelCase; IE10 and IE11
el.addEventListener('pointermove',doSomething,false); 
    // lowercase; IE11 only

```
IE10和IE11的点击事件类型也不一样。如果你要确保事件的触发你需要这样写：
```
function doSomething(e) {
    if (e.type === 'MSPointerMove' ||
        e.type === 'pointermove') {
        // this is a pointermove event
    }
}
```
####事件属性
事件通常有`target`和`clientX/Y`等属性。点击事件有一些额外的属性，`pointerType`就是其中之一。

####touch-action
`touch-action`是一个CSS申明。它告诉系统要处理什么类型的触摸行为。目前只有IE支持。IE10使用前缀，IE11可用可不用。要支持IE10必须要用`-ms-touch-action`。



