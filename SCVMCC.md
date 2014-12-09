##单类 vs 多类CSS
像我之前在有关[模块化CSS](http://technology.customink.com/blog/2014/08/26/modular-css-with-suit/)文章中提到的那样，写Sass/CSS很困难。检查项目里用到的标签，是判断项目中结果代码是否简洁并且结构良好的最好的方法之一。过度嵌套的元素导致过度嵌套的CSS并且当你发现很难明白类名的意思，那么CSS本身很可能缺乏语义。随着我们在每个元素上增加越来越多的类，代码可读性越来越差，简直是雪上加霜。如果我们可以只写一个类就能实现元素需要的所有样式的话呢？

###单类CSS
让我们试一试单类的方法。为了让例子简明我们赋予一个按钮样式（为了达到这个例子的目的我们将使用[SUIT CSS](http://technology.customink.com/blog/2014/08/26/modular-css-with-suit/)来让我们的CSS语义化）。我们假设有不同类型的按钮，或者一个相同按钮的变形，让我们给每个想要类型的按钮写一个单类。

首先我们构建想要生成的HTML模型，然后在模型基础上构造CSS。

	<button class="Btn">Just a Button</button>
	<button class="Btn--disabled">Disabled Button</button>
	<button class="Btn-secondary">Secondary Button</button>
	<button class="Btn-secondary--disabled">Secondary Disabled Button</button>


哇，这让DOM树非常简洁，通过使用SUIT，我们的类名非常语义化并且易于理解。

	.Btn {
	  background-color: blue;
	  border-radius: 5px;
	  color: white;
	  padding: 0.5rem;
	}
	
	.Btn--disabled {
	  background-color: grey;
	  border-radius: 5px;
	  color: white;
	  padding: 0.5rem;
	}
	
	.Btn-secondary {
	  background-color: white;
	  border-radius: 5px;
	  color: blue;
	  padding: 0.5rem;
	}
	
	.Btn-secondary--disabled {
	  background-color: light-grey;
	  border-radius: 5px;
	  color: blue;
	  padding: 0.5rem;
	}


<a href="http://sassmeister.com/gist/ad10c8d57ac2807bcfc8" class="sb-Btn sb-Btn--secondary sb-Btn--responsive">Play with this example in Sassmeister</a>

我们写的CSS很繁复。我们可以通过Sass之类的预处理器进行改进。

	%Btn-base {
	  border-radius: 5px;
	  padding: 0.5rem;
	}
	
	@mixin ColoredBtn($color, $background-color) {
	  @extend %Btn-base;
	  color: $color;
	  background-color: $background-color;
	}
	
	.Btn {
	  @include ColoredBtn(white, blue);
	  // .Btn--disabled
	  &--disabled {
	    @include ColoredBtn(white, grey);
	  }
	  // .Btn-secondary
	  &-secondary {
	    @include ColoredBtn(blue, white);
	  }
	  // .Btn-secondary--disabled
	  &-secondary--disabled {
	    @include ColoredBtn(blue, light-grey);
	  }
	}


<a href="http://sassmeister.com/gist/b36147e990969e8ce40d" class="sb-Btn sb-Btn--secondary sb-Btn--responsive">Play with this example in Sassmeister</a>

Sass一般比等价的CSS更加简洁，让我们更一进步评估这个单类方法。到现在为止它很吸引人，但是它在不同寻常的例子中表现如何呢？

你也许已经注意到了单类存在的隐患，```.Btn-secondary--disabled```。一开始也许你很满意，甚至觉得可以如此简单得通过Sass构建样式便于打包使用单类的想法非常聪明。潜在的问题是如果我们有更多可以组合的类？我们需要创建一个单类来代表每一个构造。如果我们想要增加一个修饰符来控制按钮的尺寸，我们会使用这样的排列例如```.Btn-secondary--small--disabled```以及```.Btn-secondary--large--disabled```。或者也许是```.Btn-secondary--disabled--large```?我们既不需要记住所有修饰符的顺序，也不需要为相同的CSS生成更多CSS来代表每个顺序。单类方法开始失去它的吸引力。可选的方法是通过多类方法中的多类来构建我们的样式。

###多类CSS
比起用单类来表示每个元素的所有状态，我们可以考虑使用多类来达到想要的效果。我们依然使用上面按钮的例子。再一次，首先我们从HTML开始，可以用来当CSS的模板。


	<button class="Btn">Just a Button</button>
	<button class="Btn Btn--disabled">Disabled Button</button>
	<button class="Btn Btn-secondary">Secondary Button</button>
	<button class="Btn Btn-secondary Btn--disabled">Secondary Disabled Button</button>


基于这个HTML结构，多类Sass写法如下。

	.Btn {
	  background-color: blue;
	  border-radius: 5px;
	  color: white;
	  padding: 0.5rem;
	  // .Btn-secondary
	  &-secondary {
	    background-color: white;
	    color: blue;
	  }
	  // .Btn--disabled
	  &--disabled {
	    background-color: grey;
	  }
	}


<a href="http://sassmeister.com/gist/5d97c03de86bd194a007" class="sb-Btn sb-Btn--secondary">Play with this example in Sassmeister</a>

关于多类方法你会注意到的第一件事是需要的Sass代码明显更少。这是因为我们不需要对每个可能需要的样式组合生成CSS。取而代之我们可以创建最小块并且用它们构建我们期望的任何样式组合。

多类CSS很好得增添了写语义化模块化CSS的特性。如果可组合性没有让你心动那么只要看一下我们两个Sass例子生成代码的区别。

####单类生成的CSS

    .Btn, .Btn--disabled, .Btn-secondary, .Btn-secondary--disabled {
      border-radius: 5px;
      padding: 0.5rem;
    }
    
    .Btn {
      color: white;
      background-color: blue;
    }
    .Btn--disabled {
      color: white;
      background-color: grey;
    }
    .Btn-secondary {
      color: blue;
      background-color: white;
    }
    .Btn-secondary--disabled {
      color: blue;
      background-color: light-grey;
    }

####多类生成的CSS
	.Btn {
	  background-color: blue;
	  border-radius: 5px;
	  color: white;
	  padding: 0.5rem;
	}
	.Btn-secondary {
	  background-color: white;
	  color: blue;
	}
	.Btn--disabled {
	  background-color: grey;
	}

###结论
这个平凡例子中的Sass以及生成的CSS都更简洁精炼。想象下对于一个大型网页应用需要生成多少的单类，每个可能样式组的组合都有一个类。这会以指数增长，很快会变得不可管理。等价的多类会生成极小块并允许用户在DOM上通过多种方法结合这些类，这是一个更加灵活的方法。单类同样难以扩展，这在任何应用中都是很糟糕的更不要说在CSS框架里。

虽然单类方法一眼看上去很吸引人，但请在冲动之前好好考虑一下。长远来看用多类方法会有收益并且能帮助你编写简洁而强大的类来完成任何可能有的样式需求。

###后续阅读
我非常推荐这篇Nicolas Gallagher写的关于HTML语义化的[文章](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)，这篇文章研究了语义化css，包括多类vs单类的问题。