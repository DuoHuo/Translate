#Sass起步 
  
![](http://i2.tietuku.com/f3ebfd41dc327060.jpg)   

Sass是一种CSS预处理语言，当你使用Sass这门语言时，你使用编译程序来转换Sass文件，通常以SCSS文件格式书写然后转换成CSS文件。Sass通过添加方便的函数，变量以及其他类似脚本的助手使CSS能更加快速得书写和更加简单的控制。  
起初我躲避Sass是因为它好像是针对程序员的（它的文档到处充斥着程序的专业术语），但是在我学习Sass一段时间后，我发现它不是那么的复杂。它方便的运算和函数会令程序员非常满意，但是它也加入了一些很酷的东西使我们能更快的书写CSS,这对我们这些其他人也是很高效的。  
我不想尝试Sass的另外一个原因是因为命令行。我不能正确的记住并且输入，我很害怕如果我偶然输入一些“死亡命令”会因此毁掉我的电脑。Sass通过使用命令行工作。在它可以做任何事情前必须先安装`Ruby`。但是我们并不需要为了使用Sass对命令行，安装`Ruby`或者`Ruby`本身了解很多。非常庆幸的是，有着简单易懂的可视化界面的`GUI`工具可以使我们很简单的来书写Sass。  
在这个三部系列中，我将会以我之前用Sass构建[Web Talk Dog Walk site](http://webtalkdogwalk.in/brighton/)所遵循的流程来来给你们介绍Sass。  
###使用`CodeKit`来建立你第一个Sass项目    
`Codekit`是我在写Sass时比较喜欢的`GUI`工具,在我下面的例子中我也会使用它。它可以编译Sass文件但是只有`Mac ox`版本。`Codekit`需要花费30美元购买，但可以免费试用。如果你是`windows`用户，和`Codekit`在功能和价格上相近的有[Prepro](https://prepros.io/)和[Mixture](http://mixture.io/),还有免费，跨平台的[Koala](http://koala-app.com/)可以替代`Codekit`。   
 
![](http://i3.tietuku.com/a78db421248c3991.jpg)  
安装完`Codekit`，你就可以看到他简洁的界面。  
###添加一个项目  
为了能正确编译项目的Sass文件，你需要把项目文件夹添加添加到`Codekit`,当你添加完后，你会发现你项目的所有文件都陈列在`Codekit`中。  
  
![](http://i2.tietuku.com/fc67e6aae3f066af.jpg)  
选择`File`>`Add Project`,然后选择项目文件夹。  

因为不必要通过`Codekit`来编译`html`,所以你需要隐藏一些文件，这样你能方便地看到创建好的Sass和CSS文件。  

![](http://i3.tietuku.com/6d99cf81aadb0502.jpg)    
按住`shift`来选择多个文件，然后选择隐藏这些文件。  
###创建一个sass文件夹  
接着，创建一个文件夹来放这些Sass文件，当这些Sass文件被编译后，`Codekit`将会在sass文件夹下创建一个css文件夹来放编译好的CSS文件。  
  
![](http://i3.tietuku.com/d31d921a36f985e2.jpg)    
在你项目的根目录或者任何你想放你CSS文件的地方创建一个叫sass的空文件夹。  
###创建一个Sass文件  
一旦你的项目和文件夹被创建好，你准备好写Sass。第一步在sass文件夹下面创建一个叫`style.scss`的空文件。  
你甚至可以把一个后缀为`.css`的文件后缀直接改为.scss,这个文件也是一个可以被`Codekit`编译的有效文件。这是一个最简单的方法当你想在你已经有的CSS文件中使用Sass特性的一种方法。  
###在`Codekit`中书写和编译Sass  
我推荐在新创建的`style.scss`文件中做的第一件事情就是`css reset`:  

```css
	html, body, div, span, applet, object, iframe,h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code,del, dfn, em, font, img, ins, kbd, q, s, samp,small, strike, strong, sub, sup, tt, var,b, u, i, center,dl, dt, dd, ol, ul, li,fieldset, form, label, legend,table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas, details, figcaption, figure, footer, header, hgroup, menu, nav, section, summary, time, mark, audio, video, svg, hr {margin: 0;padding: 0;border: 0;font-size: 100%; font: inherit; vertical-align: baseline; font-weight: normal;} …
```    
`reset`是普通的CSS,但是这不产生影响因为一个SCSS文件可以同时识别Sass和CSS,并且`Codekit`可以同时编译它们。当你保存`style.scss`,`Codekit`会在列表中把文件展示出来。  
![](http://i3.tietuku.com/4ddd68f8cf942dca.jpg)  
选择底部左侧的刷新图标就可以在`Codekit`看到`style.scss`文件。  

接着你要确认`Codekit`按照预期编译。在列表中选择`style.scss`文件可以查看`Codekit`编译出来的`style.css`文件的路径。然后点击`compile`来把SCSS文件编译为`.css`文件。  
![](http://i2.tietuku.com/1d48595499b16b36.jpg)  
选中`style.scss`然后点击`compile`来把SCSS文件编译为`.css`文件。

现在你将会在`Codekit`项目下的一个新的CSS文件夹中看到编译出来的CSS文件:  

```css  
html, body, div, span, applet, object, iframe, h1, h2, h3, h4, h5, h6, p, blockquote, pre, a, abbr, acronym, address, big, cite, code, del, dfn, em, font, img, ins, kbd, q, s, samp, small, strike, strong, sub, sup, tt, var, b, u, i, center, dl, dt, dd, ol, ul, li, fieldset, form, label, legend, table, caption, tbody, tfoot, thead, tr, th, td, article, aside, canvas, details, figcaption, figure, footer, header, hgroup, menu, nav, section, summary, time, mark, audio, video, svg, hr {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
  font-weight: normal; 
}
…
```  
`Codekit`一个非常好的特性就是一个文件第一次被编译后，你只需要通过保存SCSS文件就可以自动编译成CSS,这是因为`Codekit`一直监视你的文件。  
同时，你也可以选择你编译出来的CSS是压缩好的,在`Output Style`菜单中选择`Compressed`即可。  
  
![](http://i2.tietuku.com/6013c5f738acbdad.jpg)  
最后，需要记住的是只有最后编译好的CSS文件需要上传到服务器。并且像其他CSS文件一样在`HTML`头部引用一下。  

```html
<link rel="stylesheet" href="css/style.css">
```  
###部分引入(Partials)  
现在你了解了在`Codekit`创建一个项目和Sass文件的基础知识，下面让我们关注一些Sass提供的一些特殊的特性，先从文件组织开始吧。有时CSS文件读起来非常凌乱和困难，就像上边的`css reset`的样式。但是如果CSS文件被组织在一个个单独文件时中时就会变得非常好维护。  
利用Sass的这个特性你可以把CSS文件整理成不同文件却不会对网页加载造成任何影响。你需要做的就是把你的样式分成不同的文件，并且在你的`html`页面中把它们一一引入进来，或者在另一个CSS文件中通过`@import`引入。但是这样每次当你从另一个地方请求一个文件，你就创建了一次服务器请求。许多服务器请求会使得页面加载变得特别的慢，尽管你的文件本身都特别小。  
部分引入的文件可以是CSS块或者Sass块。通过`@import`指令就可以把要引入的文件引入到一个简单的Sass文件中。

```scss
@import "partial";
@import "another-partial";
@import "partial-name";
```  
当源文件被编译的时候，所有被引入的CSS文件和Sass文件都可以被很好的编译。编译器会把你所有的样式都合并成一个CSS文件让服务器来下载。  
###组织引入内容  
用适合你开发流程的方式来组织你的引入。我采用了像`SMACSS`这样模块结构的方法。 
 
* 基本的`html`选择器(`base.scss`)  
* 布局样式（`layout.scss`）
* 把没有任何依赖性像重置样式和`Web fonts`的样式划分成部分。(比如`reset.scss`)  

我会用`@import`语法在我的`style.scss`文件把这些部分引入进来。  

```scss
@import "reset.scss";
@import "base.scss";
@import "layout.scss";
```
在`Codekit`中，我们可以看见那些引入文件和`style.scss`在同一个文件夹中。但是那些引入的文件变成了灰色因为它们是作为`sytle.scss`的一部分被引入进来，没有被直接编译。  
  
![](http://i2.tietuku.com/437cac28fe172986.jpg)  

同时在css文件夹中，你可以发现`Codekit`没有把引入的文件单独地编译成新的CSS文件,这是因为所有的样式都被编译进了`style.css`这个文件中。   
 
![](http://i2.tietuku.com/dae466c3590a31ea.png)  
###变量  
变量是Sass中最简单和最常用的部分。我用变量来表示像颜色和字体这种的全局的变量。通过前缀名`$`后接属性名来定义一个变量。  

```scss
$grey-light: #f9f9f9;
```
在我的`Web Talk Dog Wal`的模板中，我设计了一个拥有所有颜色的色板。  
  
![](http://i2.tietuku.com/412e81f4e8641ad7.jpg)
为了定义我Sass中所有颜色，我单独新建了一个`variable.scss`文件来包含我所有的颜色变量。  

```scss
$white: #fff;

$grey-light: #f9f9f9;
$grey-mid-light: #eee;
$grey-mid: #ccc;
$grey-darker: #474747;

$green-dark: #3F5526;
$green-mid-dark: #44632B;
$green-mid: #637A3D;
$green-mid-light: #759845;
$green-bright: #97C459;
$green-light: #C0D0AA;
```
你可以按照你的想法来命名变量，但是尽可能给变量取语义化且容易被记住的名字。我倾向于把它们按颜色分组，按照深浅排序。这样在我需要一个更浅的颜色或者更深的颜色时，我能很方便地找出。  
`base.scss`文件中这些变量在不同的元素中被引用。变量的值随着十六进制的值而变化。  

```scss
body {
  background: $grey-mid-light;

  color: $grey-darker;

}

h1,
h1 a {
  color: $green-bright;

}

h2 {
  color: $green-dark;

}

…
```
保存Sass文件，被`Codekit`编译输出来的CSS:  

```scss
body {
  background: #eee;
  color: #474747;
}

h1,
h1 a {
  color: #97C459;
}

h2 {
  color: #777;
}

…
```
变量可以使用这种方式在整个样式表中使用。在我发现我的绿色不是足够深的时候，我可以修改变量的十六进制值，而且修改很快就可以在样式文件中生效。  

###注释  
当你想给你的项目或者未来自己留点提示时候，书写CSS时注释就变成很重要的部分。注释可以作为标志和标题来组织样式和解释复杂的CSS。Sass有两种注释语法,在要语句注释的结尾使用CSS的标准注释语法(`/* 注释 */`)，这样的注释在编译出来的CSS文件中还是被转译为注释。  
在Sass中，在单行的开头使用使用双斜杠(`//`)意味着整行注释。但是使用双斜杠注释(`//`)的语句不会在编译的CSS文件中被转译出来。  

```scss
/* This comment will be compiled to the final CSS */
// This comment won't be compiled to the final CSS
```
我在`Web Talk Dog Walk`中，我用双斜杠(`//`)来注释我Sass颜色变量的描述。因为变量不会在编译出来的CSS中显示，所以在编译出来的CSS文件就不要变量的注释。 

```scss
// Color variables


$white: #fff;

$grey-light: #f9f9f9;
$grey-mid-light: #eee;
$grey-mid: #ccc;
$grey-darker: #474747;
```
###Codekit出现错误  
如果你Sass和CSS文件中有错误,Sass就不会被编译。但是`Codekit`的错误提示可以从你Sass文件中找出错误并且在错误日志给你指出错误。  
  
![](http://i3.tietuku.com/8229839a9672269a.png)  
*错误提示:没有定义变量“$grey-dark”*  
在这个例子中，`Codekit`告诉我我没有定义变量`$grey-dark`,为了解决这个错误，我在我的颜色变量中添加了`$grey-dark`然后保存。  

```scss
// Color variables

$white: #fff;

$grey-light: #f9f9f9;
$grey-mid-light: #eee;
$grey-mid: #ccc;
$grey-dark: #777;

$grey-darker: #474747;
```
###第二部分预告  
在第二部分，我将会进一步钻进Sass变量中，关注使用数学来变量操作来获得垂直变化。我也将会介绍Sass的嵌套语法来使Sass更加易读和维护,对媒体查询尤其有用哦！保持期待吧！

###更加进步提升  
Sass有一些有用的颜色操作(可以理解为颜色函数)可以扩展颜色变量。在我想获得比我颜色变量中的颜色更加明亮的颜色时，我可以使用`saturate`操作，而不需要从新创建一个新的变量。  
这个函数告诉Sass把`h2`颜色的饱和度提升到100%。  

```scss
h2 {
  color: saturate($green-dark, 100%);

}
```
将会被编译成:

```scss
h2 {
  color: #5F8516;
}
``` 
###更多阅读  

* [sass](http://sass-lang.com/)  
* [Sass Reference](http://www.kaelig.fr/bettersassdocs/) *Kaelig*  
* [Sass.io](http://sass.io/)