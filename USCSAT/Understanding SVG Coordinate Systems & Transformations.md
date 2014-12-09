#Understanding SVG Coordinate Systems & Transformations (Part 1) �C The viewport, viewBox, & preserveAspectRatio
#���SVG����ϵ�ͱ任����һ���֣�-�ӿ�,`viewbox`��`preserveAspectRatio`

SVG elements aren't governed by a CSS box model like HTML elements are. This makes positioning and transforming these elements trickier and may seem��at first glance��less intuitive. However, once you understand how SVG coordinate systems and transformations work, manipulating SVGs becomes a lot easier and makes a lot more sense. In this article we're going to go over three of the most important SVG attributes that control SVG coordinate systems: `viewport`, `viewBox`, and `preserveAspectRatio`.

SVGԪ�ز���HTMLԪ��һ����CSS��ģ�͹�����ʹ�����ǿ��Ը�����λ�ͱ任��ЩԪ��-Ҳ��һ�ۿ���ȥ��ֱ̫�ۡ�Ȼ����һ���������SVG����ϵ�ͱ任������SVG��ǳ��򵥲��Һ������塣��ƪ���������ǽ����ۿ���SVG����ϵ������Ҫ���������ԣ�`viewport`�� `viewBox`�� �� `preserveAspectRatio`��

This is the first in a series of three articles covering the topic of coordinate systems and transformations in SVG.

���Ǳ�ϵ����ƪ�����еĵ�һƪ����ƪ��������SVG�е�����ϵ�ͱ任��

* Understanding SVG Coordinate Systems & Transformations (Part 1) �C The viewport, `viewBox`, & `preserveAspectRatio`
* [Understanding SVG Coordinate Systems & Transformations (Part 2) �C The `transform` Attribute](http://sarasoueidan.com/blog/svg-transformations)
* [Understanding SVG Coordinate Systems & Transformations (Part 3) �C Establishing New Viewports](http://sarasoueidan.com/blog/nesting-svgs)

* ���SVG����ϵ�ͱ任����һ���֣�-viewport��`viewBox`����`preserveAspectRatio`
* [���SVG����ϵ�ͱ任���ڶ����֣�-`transform`����](http://sarasoueidan.com/blog/svg-transformations)
* [���SVG����ϵ�ͱ任���������֣�-�������ӿ�](http://sarasoueidan.com/blog/nesting-svgs)

For the sake of visualizing the concepts and explanations in the article even further, I created an interactive demo that allows you to play with the values of the `viewBox` and `preserveAspectRatio` attributes.

Ϊ��ʹ���е����ݺͽ��͸����󻯣��Ҵ�����һ��������ʾ�����������ı�`viewBox` �� `preserveAspectRatio`��ֵ��

<a class="button" href="/demos/interactive-svg-coordinate-system/index.html">Check the interactive demo out.</a>

<a class="button" href="/demos/interactive-svg-coordinate-system/index.html">�鿴������ʾ</a>

*The demo is the cherry on top of the cake, so do make sure you come back to read the article if you check it out before you do!*

*�������ֻ����Ҫ���ݵ�һС���֣����Կ�������������Ķ���ƪ����*

##The SVG Canvas
##SVG����

The **canvas** is the space or area where the SVG content is drawn. Conceptually, this canvas is infinite in both dimensions. The SVG can therefore be of any size. However, it is rendered on the screen relative to a **finite region** known as the viewport. Areas of the SVG that lie beyond the boundaries of the viewport are clipped off and not visible.

**canvas**�ǻ���SVG���ݵ�һ��ռ�����������ϣ�����������ά���϶������޵ġ�����SVG����������ߴ硣Ȼ����SVGͨ��**��������**չ������Ļ�ϣ�����������`viewport`��SVG�г����ӿڱ߽������ᱻ���в������ء�

##The Viewport
##�ӿ�

The viewport is the viewing area where the SVG will be visible. You can think of the viewport as a window through which you can see a particular scene. The scene may be entirely or partially visible through that window.

�ӿ���һ��SVG�ɼ�����������԰��ӿڵ���һ��������͸������������Կ����ض��ľ��󣬾���Ҳ��������Ҳ��ֻ��һ���֡�

The SVG viewport is similar to the viewport of the browser you're viewing this page through. A web page can be of any size; it can be wider than the viewport's width, and is in most cases also longer than the viewport's length. However, only portions of a web page are visible through the viewport at a time.

SVG���ӿ����Ʒ��ʵ�ǰҳ���������ӿڡ���ҳ�������κγߴ磻�����Դ����ӿڿ�ȣ������ڴ��������¶����ӿڸ߶�Ҫ�ߡ�Ȼ����ÿ��ʱ��ֻ��һ������ҳ������͸���ӿڿɼ��ġ�

*Whether or not the entire SVG canvas or part of it is visible depends on the *size of that canvas\** and *the value of the `preserveAspectRatio`attribute*. You don't have to worry about these now; we'll talk about them further in more detail.*

*����SVG�����ɼ����ǲ��ֿɼ�ȡ�������*canvas\*�ĳߴ�*�Լ�*`preserveAspectRatio`����ֵ*�������ڲ���Ҫ������Щ������֮������۸����ϸ�ڡ�*

You specify the size of the viewport using the `width` and `height `attributes on the outermost `<svg>` element.

������������`<svg>`Ԫ����ʹ��`width`��`height`���������ӿڳߴ硣

	<!-- the viewport will be 800px by 600px -->
	<svg width="800" height="600">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

In SVG, values can be set with or without a unit identifier. A unitless value is said to be specified in user space using user units. If a value is specified in user units, then the value is assumed to be equivalent to the same number of "px" units. This means that the viewport in the above example will be rendered as a 800px by 600px viewport.

��SVG�У�ֵ���Դ���λҲ�����Բ�����һ��������λ��ֵ�������û��ռ���ͨ���û���λ���������ֵͨ���û���λ��������ô���ֵ����ֵ����Ϊ��"px"��λ����ֵһ��������ζ���������ӽ�����ȾΪ800px*600px���ӿڡ�

You can also specify values using units. The supported length unit identifiers in SVG are: `em`, `ex`, `px`, `pt`, `pc`, `cm`, `mm`, `in`, and percentages.

��Ҳ����ʹ�õ�λ������ֵ��SVG֧�ֵĳ��ȵ�λ�У�`em`��`ex`��`px`��`pt`��`pc`��`cm`��`mm`��`in`�Ͱٷֱȡ�

Once the width and height of the outermost SVG element are set, the browser establishes an initial viewport coordinate system and an initial user coordinate system.

һ�����趨�����SVGԪ�صĿ�ߣ�������Ὠ����ʼ�ӿ�����ϵ�ͳ�ʼ�û�����ϵ��

###The initial coordinate system
###��ʼ����ϵ

The initial **viewport coordinate system** is a coordinate system established on the viewport, with the origin at the top left corner of the viewport at point (0, 0), the positive x-axis pointing towards the right, the positive y-axis pointing down, and one unit in the initial coordinate system equals one "pixel" in the viewport. This coordinate system is similar to the coordinate system established on an HTML element with a CSS box model.

��ʼ**�ӿ�����ϵ**��һ���������ӿ��ϵ�����ϵ��ԭ��(0,0)���ӿڵ����Ͻǣ�X������ָ���ң�y������ָ���£���ʼ����ϵ�е�һ����λ�����ӿ��е�һ��"����"���������ϵͳ������ͨ��CSS��ģ����HTMLԪ���Ͻ���������ϵ��

The initial **user coordinate system** is the coordinate system established on the SVG canvas. This coordinate system is initially identical to the viewport coordinate system��it has its origin at the top left corner of the viewport with the positive x-axis pointing towards the right, the positive y-axis pointing down. Using the `viewBox` attribute, the initial user coordinate system��also known as **the current coordinate system**, or **user space in use**��can be modified so that it is not identical to the viewport coordinate system anymore. We'll talk about modifying it in the next section.

��ʼ**�û�����ϵ**�ǽ�����SVG�����ϵ�����ϵ���������ϵһ��ʼ���ӿ�����ϵ��ȫһ��-���Լ���ԭ��λ���ӿ����Ͻǣ�x������ָ���ң�y������ָ���¡�ʹ��`viewBox`���ԣ���ʼ�û�����ϵͳ-Ҳ��**��ǰ����ϵ**����**ʹ���е��û��ռ�**-���Ա�����ӿ�����ϵ��һ��������ϵ��������һ�½���������θı�����ϵ��

For now, we won't specify a `viewBox` attribute value. The user coordinate system of the SVG canvas is identical to that of the viewport.

������Ϊֹ�����ǻ�û������`viewBox`����ֵ��SVG�������û�����ϵͳ���ӿ�����ϵͳ��ȫһ����

In the following image, the viewport coordinate system "ruler" is grey, and that of the user coordinate system (the `viewBox`) is blue. Since they are both identical at this point, the two coordinate systems overlap.

��ͼ�У��ӿ�����ϵ��"���"�ǻ�ɫ�ģ��û�����ϵ��`viewBox`��������ɫ�ġ��������������ʱ����ȫ��ͬ��������������ϵͳ�غ��ˡ�

![](svg/initial-coordinate-systems.jpg)

The parrot in the above SVG has a bounding box that is 200 units (200 pixels in this case) in width and 300 units in height. The parrot is drawn on the canvas based on the initial coordinate system.

����SVG�е����ĵ����߽���200����λ�������������200�����أ����300����λ�ߡ����Ļ��ڳ�ʼ����ϵ�ڻ����л��ơ�

*A new user space (i.e., a new current coordinate system) can also be established by specifying **transformations** using the `transform` attribute on a container element or graphics element. We'll talk about transformations in the second part of this article, and then in more details in the third and last part.*

*���û��ռ䣨�����µ�ǰ����ϵ��Ҳ����ͨ��������Ԫ�ػ�ͼ��Ԫ����ʹ��`transform `����������**�任**�����ǽ�����ƪ���µĵڶ��������۹��ڱ任�����ݣ�����ϸ���ڵ������ֺ���󲿷������ۡ�*

##`viewBox`

I like to think of the `viewBox` as the "real" coordinate system. After all, it is the coordinate system used to draw the SVG graphics onto the canvas. This coordinate system can be smaller or bigger than the viewport, and it can be fully or partially visible inside the viewport too.

��ϲ����`viewBox`���Ϊ����ʵ������ϵ�����ȣ�����������SVGͼ�λ��Ƶ������ϵ�����ϵ���������ϵ���Դ����ӿ�Ҳ����С���ӿڣ����ӿ��п�������ɼ��򲿷ֿɼ���

In the previous section, this coordinate system��the user coordinate system��was identical to the viewport coordinate system. The reason for that is that we did not specify it to be otherwise. That's why all the positioning and drawing seemed to be done relative to the viewport coordinate system. Because once we created a viewport coordinate system (using `width` and `height`), the browser created a default user coordinate system that is identical to it.

��֮ǰ���½���������ϵ-�û�����ϵ-���ӿ�����ϵ��ȫһ������Ϊ����û�а�����������������ϵ�������Ϊʲô���еĶ�λ�ͻ��ƿ������ǻ����ӿ�����ϵ�ġ���Ϊ����һ�������ӿ�����ϵ��ʹ��`width`��`height`���������Ĭ�ϴ���һ����ȫ��ͬ���û�����ϵ��

You specify your own user coordinate system using the `viewBox` attribute. If the user coordinate system you choose has the same aspect ratio (ratio of height to width) as the viewport coordinate system, it will stretch to fill the viewport area (we'll talk examples in a minute). However, if your user coordinate system does not have the same aspect ratio, you can use the `preserveAspectRatio`attribute to specify whether or not the entire system will be visible inside the viewport or not, and you can also use it to specify how it is positioned inside the viewport. We'll get into details and lots of examples for this case in the next section. In this section, we'll stick to examples where the aspect ratio of the `viewBox` matches that of the viewport��in these examples, `preserveAspectRatio` has no effect.

�����ʹ��`viewBox`���������Լ����û�����ϵ�������ѡ����û�����ϵͳ���ӿ�����ϵͳ��߱ȣ��߱ȿ���ͬ��������������Ӧ�����ӿ�����һ���������Ǿ����������ӣ���Ȼ�����������û�����ϵ��߱Ȳ�ͬ���������`preserveAspectRatio`��������������ϵͳ���ӿ����Ƿ�ɼ�����Ҳ�����������������ӿ�����ζ�λ�����ǻ����¸��½���������һ�����ϸ�ں����ӡ�����һ�������ֻ����`viewBox`�Ŀ�߱ȷ����ӿڵ����-����Щ�����У�`preserveAspectRatio`������Ӱ�졣

Before we get into the examples, we'll go over the syntax of `viewBox`.

������������Щ����ǰ�����ǻع�һ��`viewBox`���﷨��

###The `viewBox` syntax
###`viewBox`�﷨

The `viewBox attribute` takes four parameters as a value: `<min-x>, <min-y>, width` and `height`.

`viewBox`���Խ����ĸ�����ֵ��������`<min-x>, <min-y>, width` �� `height`��

	viewBox = <min-x> <min-y> <width> <height>

The` <min-x>` and `<min-y>` values determine the upper left corner of the viewbox, and the `width` and `height` determine the width and height of that viewport. Note here that the width and height of the viewport need not be the same as the width and height set on the parent `<svg>` element. A negative value for `<width>` or `<height>` is invalid. A value of zero disables rendering of the element.

`<min-x>` �� `<min-y>` ֵ����viewbox�����Ͻǣ�`width`��`height`�����ӿڵĿ�ߡ�����Ҫע���ӿڵĿ�߲�һ���͸�`<svg>`Ԫ�صĿ��һ����`<width>`��`<height>`ֵΪ�����ǲ��Ϸ��ġ�ֵΪ0�Ļ����ֹԪ�ص���Ⱦ��

*Note that the width of the viewport can also be set in CSS to any value. For example, setting `width: 100%` will make the SVG viewport fluid in a document. Whatever value of the `viewBox`, it will then be mapped to the computed width of the outer SVG element.*

*ע���ӿڵĿ��Ҳ������CSS������Ϊ�κ�ֵ�����磺����`width:100%`����SVG�ӿ����ĵ�������Ӧ������`viewBox`��ֵ�Ƕ��٣�����ӳ��Ϊ���SVGԪ�ؼ�����Ŀ��ֵ��*

An example of setting `viewBox` would look like the following:

����`viewBox`���������£�

	<!-- The viewbox in this example is equal to the viewport, but it can be different -->
	<svg width="800" height="600" viewbox="0 0 800 600">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

If you've read about the `viewBox` somewhere before, you may have come across a few definitions saying that you can use the `viewBox` attribute to transform the SVG graphic by scaling or translating it. This is true. I'm going to go further and say that you can even crop the SVG graphic using `viewBox`.

�����֮ǰ�������ط�������`viewBox`����Ҳ��ῴ��һЩ����˵�������`viewBox`����ͨ�����Ż��߱仯ʹSVGͼ�α任��������ġ��ҽ�����̽�����Ҹ�������������ʹ��`viewBox`���и�SVGͼ�Ρ�

The best way to understand the `viewBox` and differentiate it from the viewport is by visualizing it. So let's start with some examples. We'll start with examples where th aspect ratio of the viewbox is the same as the aspect ratio of the viewport, so we won't need to dig into `preserveAspectRatio` yet.

���`viewBox`���ӿ�֮�������õķ���������۲졣���������ǿ�һЩ���ӡ����ǽ���viewbox��viewport�Ŀ�߱���ͬ�����ӿ�ʼ���������ǻ�����Ҫ�����˽�`preserveAspectRatio`��

###`viewBox` with aspect ratio equal to the viewport's aspect ratio
###��viewport��߱���ͬ��`viewBox`

We'll start with a simple example. The `viewbox` in this example will be half the size of the viewport. We won't change the origin of the viewbox in this one, so both `<min-x>` and `<min-y>` will be set to zero. The width and height of the viewbox will be half the width and height of the viewport. This means that we're preserving the aspect ratio.

���Ǵ�һ���򵥵����ӿ�ʼ����������е�`viewbox`�ĳߴ����ӿڳߴ��һ�롣��������������ǲ��ı�viewbox��ԭ�㣬����`<min-x>`��`<min-y>`�����ó�0��viewbox�Ŀ����viewport��ߵ�һ�롣����ζ�����Ǳ��ֿ�߱ȡ�

	<svg width="800" height="600" viewbox="0 0 400 300">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

So, what does `viewbox="0 0 400 300"` exactly do?
���ԣ�`viewbox="0 0 400 300"`������ʲô���أ�

* It specifies a specific region of the canvas spanning from a top left point at (0, 0) to a point at (400, 300).
* The SVG graphic is then **cropped** to that region.
* The region is **scaled up** (in a zoom-in-like effect) to fill the entire viewport.
* The user coordinate system is mapped to the viewport coordinate system so that��in this case��one user unit is equal to two viewport units.

* ��������һ���ض�������canvas������Ͻǵĵ�(0,0)����(400,300)��
* SVGͼ���������**����**��
* ����**����**����������Ч���������������ӿڡ�
* �û�����ϵ��ӳ�䵽�ӿ�����ϵ-�����������-һ���û���λ���������ӿڵ�λ��

The following image shows the result of applying the above viewbox to the `<svg>` canvas in our example. The grey units represent the viewport coordinate system, and the blue coordinate system represents the user coordinate system established by the `viewBox`.

�����ͼƬչʾ�������������а������viewboxӦ�õ�`<svg>` �����е�Ч������ɫ��λ�����ӿ�����ϵ����ɫ����ϵ����`viewbox`�������û�����ϵ��

![](svg/viewbox-400-300-crop.jpg)

Anything you draw on th SVG canvas will be drawn relative to the new user coordinate system.

�κ���SVG�����л������ݶ��ᱻ��Ӧ���µ��û�����ϵ�С�

*I like to visualize the SVG canvas with a `viewBox` the same way as Google maps. You can zoom in to a specific region or area in Google maps; that area will be the only area visible, scaled up, inside the viewport of the browser. However, you know that the rest of the map is still there, but it's not visible because it extends beyond the boundaries of the viewport��it's being clipped out.*

*��ϲ����Google��ͼһ��ͨ��`viewBox`��SVG�������󻯡���Google��ͼ����������ض��������ţ����������Ψһ�ɼ��ģ�������������ӿ��а��������ӡ�Ȼ������֪����ͼ��ʣ�ಿ�ֻ���������ǲ��ɼ���Ϊ�������ӿڵı߽�-�������ˡ�*

Now let's try changing the `<min-x>` and `<min-y>` values. We'll set both to `100`. They can be any number you want. The width and height ratio will also be the same as width and height ratio of the viewport.

�������������Ÿı�`<min-x>`��`<min-y>`��ֵ��������Ϊ`100`����������ó��κ�����Ҫ��ֵ����߱Ȼ��Ǻ��ӿڵĿ�߱�һ����


	<svg width="800" height="600" viewbox="100 100 200 150">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

The effect of applying `viewBox="100 100 200 150"` is also a crop effect like the one in the previous example. The graphic is cropped and scaled up to fill the entire viewport area.

���`viewBox="100 100 200 150"`��Ч����֮ǰ������һ�����ǲ��е�Ч����ͼ�α�����Ȼ�����������������ӿ�����

![](svg/viewbox-200-150-crop.jpg)

Again, the user coordinate system is mapped to the viewport coordinate system��200 user units are mapped to 800 viewport units so that every user unit is equal to four viewport units. This results in a zoom-in effect like the one you can see in the above screenshot.

��һ�Σ��û�����ϵ��ӳ�䵽�ӿ�����ϵ-200�û���λӳ��Ϊ800�ӿڵ�λ���ÿ���û���λ�����ĸ��ӿڵ�λ��������㿴���������ǷŴ��Ч����

Also note, at this point, that specifying non-zero values for the `<min-x>` and `<min-y>` values has a transformation effect on the graphic; more specifically, it is as though the SVG canvas was translated by 100 units to the top and 100 units to the left (`transform="translate(-100 -100)"`).

����ע�⣬�����ʱ��Ϊ`<min-x>`��`<min-y>`������0��ֵ��ͼ���б任��Ч���������ر���ǣ�SVG ������������������100����λ����������100����λ��`transform="translate(-100 -100)"`����

Indeed, as the specification states, **"the effect of the `viewBox` attribute is that the user agent automatically supplies the appropriate transformation matrix to map the specified rectangle in user space to the bounds of a designated region (often, the viewport)"**.

��ȷ����Ϊ�淶˵����**��`viewBox`���Ե�Ӱ�������û������Զ�����ʵ��ı任���������û��ռ��о���ľ���ӳ�䵽ָ������ı߽磨ͨ�����ӿڣ���**��

This is just a fancy way of saying what we already mentioned before: the graphic is cropped and then **scaled** to fit into the viewport. The spec then goes on to add a note: **"in some cases the user agent will need to supply a translate transformation in addition to a scale transformation. For example, on an outermost svg element, a translate transformation will be needed if the viewBox attributes specifies values other than zero for `<min-x>` or `<min-y>`.)"**

����һ���ܰ���˵������֮ǰ�Ѿ��ᵽ�����ݵķ�����ͼ�α�����Ȼ��**����**����Ӧ�ӿڡ����˵�����������һ��ע�ͣ�**����һЩ������û����������ű任֮����Ҫ����һ���ƶ��任�����磬��������svgԪ���ϣ����viewBox���Զ�`<min-x>`��`<min-y>`������0ֵ����ô����Ҫ�ƶ��任����**

To demonstrate the translation transformation even better, let's try applying negative values (-100) to `<min-x>` and `<min-y>`. The translation effect would be then similar to `transform="translate(100 100)"`; meaning that the graphic will be translated to the bottom and to the right after being cropped and scaled. If were to revisit the second to last example with a crop size of 400 by 300, and then add the new negative `<min-x>` and `<min-y>` values, this would be our new code:

Ϊ�˸�����ʾ�ƶ��任�����������Ÿ�`<min-x>`��`<min-y>`���-100���ƶ�Ч������`transform="translate(100 100)"`������ζ��ͼ�λ����и�����ź��ƶ������·����ع˵����ڶ������гߴ�Ϊ400*300�����ӣ�����µ���Ч`<min-x>`��`<min-y>`ֵ���µĴ������£�

	<svg width="800" height="600" viewbox="-100 -100 300 200">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

The result of applying the above `viewBox` transformation to the graphic is shown in the following image:

��ͼ���������`viewBox` transformation�Ľ������ͼ��ʾ��

![](svg/viewbox-400-300-crop-translate.jpg)

Note that, unlike the `transform` attribute, the automatic transformation that is created due to a `viewBox` does not affect the `x, y, width` and `height` attributes on the element with the `viewBox` attribute. Thus, in the example above which shows an `svg` element which has attributes `width, height` and `viewBox`, the `width` and `height` attributes represent values in the coordinate system that exists before the `viewBox` transformation is applied. You can see this in the above examples as the initial (grey) viewport coordinate system remains unaffected even after using the `viewBox` attribute on the `<svg>`.

ע�⣬��`transform`���Բ�ͬ����ΪviewBox�Զ���ӵ�tranfomation����Ӱ����`vewBox`���Ե�Ԫ�ص�`x`,`y`,��͸ߵ����ԡ���ˣ�������������չʾ�Ĵ���`width`,`height`��`viewBox`���Ե�`svg`Ԫ�أ�`width`��`height`���Դ������`viewBox` �任֮ǰ������ϵ�е�ֵ������������������Կ�����ʼ����ɫ��viewport����ϵ������`<svg>`��ʹ����`viewBox`���Ժ���Ȼû��Ӱ�졣

On the other hand, like the `transform` attribute, it does establish a new coordinate system for all other attributes and for descendant elements. You can also see that in the above examples as the user coordinate system established is a new one��it does not remain as the initial user coordinate system which was identical to the viewport coordinate system before the `viewBox` was used. And any descendants of the `<svg>` will be positioned and sized in the **new** user coordinate system, not the initial one.

��һ���棬��`tranform`����һ�������������������Ժͺ��Ԫ�ؽ�����һ���µ�����ϵ���㻹���Կ��������������У��û�����ϵ���½�����-�����Ǳ������ʼ�û�����ϵ��ʹ��`viewBox`ǰ���ӿ�����ϵһ�����κ�`<svg>`����������**��**���û�����ϵ�ж�λ��ȷ���ߴ磬�����ǳ�ʼ����ϵ��

Our last `viewBox` example is similar to the previous ones, but instead of cropping the canvas, we're going to extend it inside the viewport and see how it affects the graphic. We're going to specify a viewbox with a width and height that are larger than those of the viewport, while also maintaining the aspect ratio of the viewport. We'll deal with different aspect ratios in the next section.

���һ��`viewBox`�����Ӻ�ǰһ�����ƣ������������и�������ǽ���viewport����չ�����������Ӱ��ͼ�Ρ����ǽ�����һ����߱��ӿڴ��viewBox������Ȼ����viewport�Ŀ�߱ȡ���������һ�������۲�ͬ�Ŀ�߱ȡ�

In this example, we'll make the viewbox 1.5 times the size of the viewport.

����������У����ǽ�viewbox�ĳߴ���Ϊviewport��1.5����

	<svg width="800" height="600" viewbox="0 0 1200 900">
	    <!-- SVG content drawn onto the SVG canvas -->
	</svg>

What will happen now is that the user coordinate system is going to be scaled up to 1200x900. It will then be mapped to the viewport coordinate system so that every 1 unit in the user coordinate system is equal to `viewport-width / viewBox-width` horizontally, and `viewport-height / viewBox-height` units vertically in the viewport coordinate system. This means that, in this case, every one x-unit in the user coordinate system is equal to 0.66 x-units in the viewport coordinate system, and every one user y-unit is mapped to 0.66 viewport y-units.

�����û�����ϵ�ᱻ�Ŵ�1200*900�����ᱻӳ�䵽�ӿ�����ϵ���û�����ϵ�е�ÿһ����λˮƽ�����ϵ����ӿ�����ϵ�е�`viewport-width / viewBox-width`����ֱ�����ϵ���`viewport-height / viewBox-height`������ζ�ţ�����������£�ÿһ���û�����ϵ�е�x-units����viewport����ϵ�е�0.66��x-units��ÿ���û�y-unitӳ���0.66��viewport y-units��

Of course, the best way to understand this is to visualize the result. The viewbox is scaled so that it fits inside the viewport as shown in the following image. And because the graphic is drawn on the canvas based on the new user coordinate system, not the viewport coordinate system, it will look smaller inside the viewport.

��Ȼ�������Щ��õķ����ǰѽ���Ӿ�����viewBox�����ŵ���Ӧ��ͼ��ʾ��viewport����Ϊͼ���ڻ���������µ��û�����ϵ���Ƶģ��������ӿ�����ϵ�������������ӿ�С��

![](svg/viewbox-1200-900.jpg)

So far, all of our examples have been in conformity with the viewport's height to width aspect ratio. But what happens if the height and width specified in the `viewBox` have a different aspect ratio than that of the viewport's? For example, suppose we set the dimensions of the viewbox to be 1000x500. The aspect ratio of height to width is no longer the same as that of the viewport. The result of using `viewBox = "0 0 1000 500"` in our example looks like the following:

��ĿǰΪֹ���������е����ӵĿ�߱ȶ����ӿ�һ�¡��������`viewBox`�������Ŀ�߱Ⱥ��ӿ��еĲ�һ���ᷢ��ʲô�أ����磬�������ǰ��ӿڵĳߴ���Ϊ1000*500����߱Ȳ��ٺ��ӿڵ�һ������������ʹ��`viewBox="0 0 1000 500"`�Ľ������ͼ��

![](svg/viewbox-1000-500.jpg)

The user coordinate system and hence the graphic is positioned inside the viewport so that:

* The entire viewbox fits inside the viewport.
* The aspect ratio of the viewbox is preserved. The viewbox was not stretched to cover the viewport area.
* THe viewbox is centered inside the viewport both vertically and horizontally.

�û�����ϵ�����ͼ�����ӿ��ж�λ��

* ����viewbox��Ӧ�ӿڡ�
* ����viewbox�Ŀ�߱ȡ�viewboxû�б������������ӿ�����
* viewbox���ӿ���ˮƽ��ֱ���С�

This is the default behavior. What controls this behavior? And what if we want to change the position of the viewbox inside the viewport? This is where the `preserveAspectRatio` attribute comes in.

����Ĭ�ϱ��֡�����ʲô���Ʊ����أ����������ı��ӿ���viewbox��λ���أ������Ҫ�õ�`preserveAspectRatio`�����ˡ�

##The `preserveAspectRatio` Attribute
##`preserveAspectRatio`����

The `preserveAspectRatio` attribute is used to force a uniform scaling for the purposes of preserving the aspect ratio of a graphic.

`preserveAspectRatio`����ǿ��ͳһ���ű�������ͼ�εĿ�߱ȡ�

If you define a user coordinate system with an aspect ratio different from that of the viewport's, and if the browser were to stretch the viewbox to fit into the viewport as we've seen in previous examples, the difference in aspect ratios will cause the graphic to be distorted in either direction. So if the viewbox in the last example were to be stretched to fill the viewport in both directions, the graphic would look like so:

������ò�ͬ���ӿڵĿ�߱ȶ����û�����ϵ�������������֮ǰ�������п������������������viewbox����Ӧ�ӿڣ���߱ȵĲ�ͬ�ᵼ��ͼ����ĳЩ������Ť�������������һ�������е�viewbox�������������з�������Ӧ�ӿڣ�ͼ�ο��������£�

![](svg/viewbox-1000-500-stretched.jpg)

The distortion is also clearly visible (and unwanted, of course) when using a viewbox value of `0 0 200 300`, which would be smaller than the dimensions of the viewport. I chose this value in particular so that the viewbox matches the size of the bounding box of the parrot. If the browser were to stretch the graphic to fill the entire viewport, it would look like the so:

����viewbox����`0 0 200 300`��ֵʱŤ���Զ��׼�����Ȼ��ܲ����룩�����ֵС���ӿڳߴ硣�ҹ���ѡ������ߴ�Ӷ���viewboxƥ�����ı߽���ӵĳߴ硣������������ͼ������Ӧ�����ӿڣ���������������������

![](svg/viewbox-200-300-stretched.jpg)

The `preserveAspectRatio` attribute allows you to force uniform scaling of the viewbox, while maintaining the aspect ratio, and it allows you to specify how to position the viewbox inside the viewport if you don't want it to be centered by default.

`preserveAspectRatio`������������ڱ��ֿ�߱ȵ������ǿ��ͳһviewbox�����űȣ��������������Ĭ�Ͼ������������viewbox���ӿ��е�λ�á�

###The `preserveAspectRatio` syntax
###`preserveAspectRatio`�﷨

The official syntax for `preserveAspectRatio` is:
`preserveAspectRatio`�Ĺٷ��﷨�ǣ�

	preserveAspectRatio = defer? <align> <meetOrSlice>?

It is usable on any element that establishes a new viewport (we'll get into these in the next parts of the series).

�����κν�����viewport��Ԫ���϶���Ч�����ǻ������ϵ�е���һ��������������⣩��

The `defer` argument is optional, and is used only when you're applying `preserveAspectRatio` to an `<image>`. It is ignored when used on any other element. Since `<image>` it outside the scope of this article, we'll skip the `defer` option for now.

`defer`�����ǿ�ѡ�ģ�����ֻ�е�����`<image>`�����`preserveAspectRatio`�ű��õ��������κ�����Ԫ����ʱ�����ᱻ���ԡ�`<images>`��������ƪ���µ����۷�Χ��������ʱ����`defer`���ѡ�

The `align` parameter indicates whether to force uniform scaling and, if so, the alignment method to use in case the aspect ratio of the `viewBox` doesn't match the aspect ratio of the viewport.

`align`���������Ƿ�ǿ��ͳһ����������ǣ����뷽������`viewBox`�Ŀ�߱Ȳ�����viewport�Ŀ�߱ȵ��������Ч��

If the `align` value is set to `none`, for example:

���`align`ֵ��Ϊ`none`�����磺

	preserveAspectRatio = "none"

The graphic will be scaled to fit inside the viewport without maintaining the aspect ratio, just like we saw in the last two examples.

ͼ�β��ڱ��ֿ�߱ȶ�����������Ӧ�ӿڣ����������������������п�����������

All other values of `preserveAspectRatio` force uniform scaling while preserving the viewbox's aspect ratio, and specify how to align the viewbox inside the viewport. We'll get into the values of `align` shortly.

��������`preserveAspectRatio`ֵ���ڱ���viewbox�Ŀ�߱ȵ������ǿ�����죬����ָ�����ӿ�����ζ���viewbox�����ǻ��̽���`align`��ֵ��

The last argument, `meetOrSlice` is also optional, and it defaults to `meet`. This argument specifies whether or not the entire `viewBox`should be visible inside the viewport. If provided, it is separated from the `align` parameter by one or more spaces. For example:

���һ�����ԣ�`meetOrSlice`Ҳ�ǿ�ѡ�ģ�Ĭ��ֵΪ`meet`�����������������`viewBox`���ӿ����Ƿ�ɼ�������ǣ�����`align`����ͨ��һ�������ո�ָ������磺

	preserveAspectRatio = "xMinYMin slice"

These values may seem foreign at first. To make understanding them easier and make them more familiar, you can think of the `meetOrSlice` value as being similar to the `background-size` values `contain` and `cover`; they work pretty much the same. `meet` is similar to `contain`, and `slice` is similar to `cover`. Here are the definitions and meaning of each value:

��Щֵ��һ�ۿ�����Ҳ���İ����Ϊ�������Ǹ�����������Ϥ������԰�`meetOrSlice`��ֵ�����`background-size`��`contain`��`cover`ֵ;���Ƿǳ����ơ�`meet`������`contain`��`slice`������`cover`��������ÿ��ֵ�Ķ���ͺ��壺

####*meet (The default value)*
####*meet��Ĭ��ֵ��*

Scale the graphic as much as possible while maintaining the following two criteria:

������������׼�ྡ��������Ԫ�أ�

* aspect ratio is preserved
* the entire `viewBox` is visible within the viewport

* ���ֿ�߱�
* ����`viewBox`���ӿ��пɼ�

In this case, if the aspect ratio of the graphic does not match the viewport, some of the viewport will extend beyond the bounds of the `viewBox` (i.e., the area into which the `viewBox` will draw will be smaller than the viewport). (See the last example of The viewBox section.) In this case, the boundaries of the `viewBox` are contained inside the viewport such that the boundaries *meet*.

���������£����ͼ�εĿ�߱Ȳ������ӿڣ�һЩ�ӿڻᳬ��`viewBox`�ı߽磨��`viewBox`���Ƶ������С���ӿڣ�������viewBoxһ�ڲ鿴�������ӡ������������£�`viewBox`�ı߽类������viewport��ʹ�ñ߽�*����*��

*This value is similar to `background-size: contain`. The background image is scaled as much as possible while preserving its aspect ratio and making sure it fits entirely into the background painting area. If the aspect ratio of the background is not the same as that of the element it is being applied to, parts of the background painting area will not be covered by the background image.*

*���ֵ������`background-size: contain`������ͼƬ�ڱ��ֿ�߱ȵ�����¾��������Ų�ȷ�����ʺϱ�������������������ĳ���Ⱥ�Ӧ�õ�Ԫ�صĳ���Ȳ�һ�������ֱ������������û�б���ͼƬ���ǡ�*

####slice
####��Ƭ

Scale the graphic so that the `viewBox` covers the entire viewport area, while maintaining its aspect ratio. The `viewBox` is scaled **just enough** to cover the viewport area (in both dimensions), but it is not scaled any more than needed to achieve that. In other words, it is scaled to the smallest size such that the width and height of the viewBox can completely cover the viewport.

�ڱ��ֿ�߱ȵ�����£�����ͼ��ֱ��`viewBox`�����������ӿ�����`viewBox`�����ŵ�**����**�����ӿ�����������ά���ϣ������������������κγ��������Χ�Ĳ��֡�������֮�������ŵ�viewBox�Ŀ�߿���������ȫ�����ӿڡ�

In this case, if the aspect ratio of the viewBox does not match the viewport, some of the viewBox will extend beyond the bounds of the viewport (i.e., the area into which the viewBox will draw is larger than the viewport). This will result in part of the `viewBox` being *sliced off*.

����������£����viewBox�Ŀ�߱Ȳ��ʺ��ӿڣ�һ����viewBox����չ�����ӿڱ߽磨����viewBox���Ƶ��������ӿڴ󣩡���ᵼ�²���`viewBox`����Ƭ��

*You can think of this as being similar to background-size: cover. In the case of a background image, the image is scaled while preserving its intrinsic aspect ratio (if any), to the smallest size such that both its width and its height can completely cover the background positioning area.*

*����԰�������Ϊbackground-size: cover���ڱ���ͼƬ������У�ͼƬ�ڱ��ֱ����߱ȣ���Σ�����������ŵ���߿�����ȫ���Ǳ�����λ�������С�ߴ硣*

So, `meetOrSlice` is used to specify whether or not the `viewBox` will be completely contained inside the viewport, or if it should be scaled as much as needed to cover the entire viewport, even if this means that a part of the viewbox will be "sliced off".

���ԣ�`meetOrSlice`����������`viewBox`�Ƿ�ᱻ��ȫ�������ӿ��У��������Ƿ�Ӧ�þ��������������������ӿڣ�������ζ�Ų��ֵ�viewbox�ᱻ����Ƭ����

For example, if we were to apply `viewBox` size of 200x300, and using both the `meet` and `slice` values, keeping the `align` value set to the default by the browser, the result for each value will look like the following:

���磬�����������`viewBox`�ĳߴ�Ϊ200*300������ʹ����`meet`��`slice`ֵ������`align`ֵΪ�����Ĭ�ϣ�ÿ��ֵ�Ľ���ῴ�������£�

![](svg/viewbox-200-300-meet-vs-slice.jpg)

The `align` parameter takes one of nine values, or the `none` value. Any value other than `none` is used to uniformly scale the image preserving its aspect ratio, **and** it is also used to align the `viewBox` inside the viewport.

`align`����ʹ��9��ֵ�е�һ������Ϊ`none`���κγ�`none`֮���ֵ���������ֿ�߱�����ͼƬ��**����**���������ӿ��ж���`viewBox`��

The `align` values works similar to the way `background-position` works when used with percentage values. You can think of the viewBox as being the background image. The way the positioning with `align` differs from `background-position` is that instead of positioning a specific point of the viewbox over a corresponding point of the viewport, it aligns specific "axes" of the viewBox with corresponding "axes" of the viewport.

��ʹ�ðٷֱ�ֵʱ��`align`ֵ������`background-position`������԰�viewBox��������ͼ��ͨ��`align`��λ��`background-position`�Ĳ�ͬ���ڣ���ͬ��ͨ��һ�����ӿ���صĵ�������һ���ض���viewboxֵ�����Ѿ����viewBox���ᡱ�Ͷ�Ӧ���ӿڵġ��ᡱ���롣

In order to understand the meaning of each of the `align` values, we're going to first introduce each of the "axes".

Ϊ�����ÿ��`align`ֵ�ĺ��壬���ǽ����Ƚ���ÿһ�����ᡱ��

Remember the `<min-x>` and `<min-y>` values of the `viewBox`? We're going to use each of these to define the "min-x" axis and "min-y" axis on the `viewBox`. Additionally, we're going to define two axes "max-x" and "max-y", which will be positioned at `<min-x> + <width>` and `<min-y> + <height>`, respectively. And last but not least, we'll define two axes "mid-x" and "mid-y", which are positioned at `<min-x> + (<width>/2)` and `<min-y> + (<height>/2)`, respectively.

���ǵ�viewBox��`<min-x>`��`<min-y>`ֵ�����ǽ�ʹ������������`viewBox`�е�"min-x"��"min-y"�ᡣ���⣬���ǽ����������ᡰmax-x���͡�max-y��������ͨ��`<min-x> + <width>` �� `<min-y> + <height>`����λ��������Ƕ���������"mid-x"��"mid-y"������`<min-x> + (<width>/2)` �� `<min-y> + (<height>/2)`����λ��

Did that make things more confusing? If so, have a look at the following image to see what each of those axes represents. In the image, both `<min-x>` and `<min-y>` are set to their default 0 values. The `viewBox` is set to `viewBox = "0 0 300 300"`.

�������ǲ�����������������أ�����������������ǿ�һ�������ͼƬ����һ��ÿ���������ʲô��������ͼƬ�У�`<min-x>`�� `<min-y>`ֵ������Ϊ0��`viewBox`������Ϊ`viewBox = "0 0 300 300"`��

![](svg/viewbox-x-y-axes.jpg)

The dashed grey lines in the above image represent the mid-x and mid-y axes of the viewport. We're going to use those to align the mid-x and mid-y of axes of the `viewBox` for some values. For the viewport, the min-x value is equal to 0, the min-y value is also 0, the max-x value is equal to the width of the `viewBox`, the max-y value is equal to its height, and the mid-x and mid-y represent the middle values of the width and height, respectively.

����ͼƬ�еĻ�ɫ���ߴ����ӿڵ�mid-x��mid-y�ᡣ���ǽ������Ǹ�һЩֵ������`viewBox`��mid-x��mid-y�ᡣ�����ӿڣ�min-x��ֵ����0��min-yֵҲ����0��max-xֵ����`viewBox`�Ŀ�ȣ�max-y��ֵ���ڸ߶ȣ�mid-x��mid-y�����˿�Ⱥ͸߶ȵ��м�ֵ��

The alignment values are:
�����ȡֵ������

**none**

Do not force uniform scaling. Scale the graphic content of the given element non-uniformly (without preserving aspect ratio) if necessary such that the element's bounding box exactly matches the viewport rectangle.

��ǿ��ͳһ���š������Ҫ�Ļ����ڲ�ͳһ���������ֿ�߱ȣ�����������Ÿ���Ԫ�ص�ͼ������ֱ��Ԫ�صı߽����ȫƥ�����ӿھ��Ρ�

*In other words, the `viewBox` is stretched or shrunk as necssary so that it fills the entire viewport exactly, disregarding the aspect ratio. The graphic may be distorted.*

*���仰˵������б�Ҫ�Ļ�`viewBox`���������������ȫ��Ӧ�����ӿڣ����ܿ�߱ȡ�ͼ��Ҳ���Ť����*

(Note: if `<align>` is none, then the optional `<meetOrSlice>` value is ignored.)
��ע�⣺���`<align>`��ֵ��none����ѡ��`<meetOrSlice>`ֵ��Ч����

####*xMinYMin*

Force uniform scaling.

Align the `<min-x>` of the element's `viewBox` with the smallest X value of the viewport.

Align the `<min-y>` of the element's `viewBox` with the smallest Y value of the viewport.

*Think of this as being similar to `backrgound-position: 0% 0%;`.*

####*xMinYMin*

ǿ��ͳһ����

�ӿ�X�����Сֵ����Ԫ��`viewBox`��`<min-x>`��

�ӿ�Y�����Сֵ����Ԫ��viewBox��`<min-y>`��

*��������Ϊ`backrgound-position: 0% 0%;`��*

####*xMinYMid*

Force uniform scaling.

Align the `<min-x>` of the element's `viewBox` with the smallest X value of the viewport.

Align the midpoint Y value of the element's `viewBox` with the midpoint Y value of the viewport.

*Think of this as being similar to `backrgound-position: 0% 50%;`.*

####*xMinYMid*
ǿ��ͳһ���š�

�ӿ�X�����Сֵ����Ԫ��`viewBox`��`<min-x>`��

�ӿ�Y����м�ֵ������Ԫ�ص�viewBox���м�ֵ��

*��������Ϊ`backrgound-position: 0% 50%;`��*

####*xMinYMax*
Force uniform scaling.

Align the `<min-x>` of the element's `viewBox` with the smallest X value of the viewport.

Align the `<min-y>+<height>` of the element's `viewBox` with the maximum Y value of the viewport.

*Think of this as being similar to `backrgound-position: 0% 100%;`.*

####*xMinYMax*
ǿ��ͳһ���š�

�ӿ�X�����Сֵ����Ԫ��`viewBox`��`<min-x>`��

�ӿ�X������ֵ����Ԫ�ص�`viewBox`��`<min-y>+<height>`��

*��������Ϊ`backrgound-position: 0% 100%;`��*

####*xMidYMin*
Force uniform scaling.

Align the midpoint X value of the element's `viewBox` with the midpoint X value of the viewport.

Align the `<min-y>` of the element's `viewBox` with the smallest Y value of the viewport.

*Think of this as being similar to `backrgound-position: 50% 0%;`.*

####*xMidYMin*
ǿ��ͳһ���š�

�ӿ�X����м�ֵ����Ԫ�ص�`viewBox`��X���м�ֵ��

�ӿ�Y����м�ֵ����Ԫ�ص�`viewBox`�� `<min-y>`��

*��������Ϊ`backrgound-position: 50% 0%;`��*

####*xMidYMid (The default value)*

Force uniform scaling.

Align the midpoint X value of the element's `viewBox` with the midpoint X value of the viewport.

Align the midpoint Y value of the element's `viewBox` with the midpoint Y value of the viewport.

*Think of this as being similar to `backrgound-position: 50% 50%;`.*

####*xMidYMid (Ĭ��ֵ)*

ǿ��ͳһ���š�

�ӿ�X����м�ֵ����Ԫ�ص�`viewBox`��X���м�ֵ��

�ӿ�Y����м�ֵ����Ԫ�ص�`viewBox`��Y���м�ֵ��

*��������Ϊ`backrgound-position: 50% 50%;`��*

####*xMidYMax*

Force uniform scaling.

Align the midpoint X value of the element's `viewBox` with the midpoint X value of the viewport.

Align the `<min-y>+<height>` of the element's `viewBox` with the maximum Y value of the viewport.

*Think of this as being similar to `backrgound-position: 50% 100%;`.*

####*xMidYMax*
ǿ��ͳһ���š�

�ӿ�X����м�ֵ����Ԫ�ص�`viewBox`��X���м�ֵ��

�ӿ�Y������ֵ����Ԫ�ص�`viewBox`��`<min-y>+<height>`��

*��������Ϊ`backrgound-position: 50% 100%;`��*

####*xMaxYMin*
Force uniform scaling.

Align the `<min-x>+<width>` of the element's `viewBox` with the maximum X value of the viewport.

Align the `<min-y>` of the element's `viewBox` with the smallest Y value of the viewport.

*Think of this as being similar to `backrgound-position: 100% 0%;`.*

####*xMaxYMin*

ǿ��ͳһ���š�

�ӿ�X������ֵ����Ԫ�ص�`viewBox`�� `<min-x>+<width>`��

�ӿ�Y�����Сֵ����Ԫ�ص�`viewBox`��`<min-y>`��

*��������Ϊ`backrgound-position: 100% 0%;`��*


####*xMaxYMid*
Force uniform scaling.

Align the `<min-x>+<width>` of the element's `viewBox` with the maximum X value of the viewport.

Align the midpoint Y value of the element's `viewBox` with the midpoint Y value of the viewport.

*Think of this as being similar to `backrgound-position: 100% 50%;`.*

####*xMaxYMid*
ǿ��ͳһ���š�

�ӿ�X������ֵ����Ԫ�ص�`viewBox`�� `<min-x>+<width>`��

�ӿ�Y����м�ֵ����Ԫ�ص�`viewBox`��Y���м�ֵ
��

*��������Ϊ`backrgound-position: 100% 50%;`��*

####*xMaxYMax*

Force uniform scaling.

Align the `<min-x>+<width>` of the element's `viewBox` with the maximum X value of the viewport.

Align the `<min-y>+<height>` of the element's `viewBox` with the maximum Y value of the viewport.

*Think of this as being similar to `backrgound-position: 100% 100%;`.*

####*xMaxYMax*
ǿ��ͳһ���š�

�ӿ�X������ֵ����Ԫ�ص�`viewBox`�� `<min-x>+<width>`��

�ӿ�Y������ֵ����Ԫ�ص�`viewBox`�� `<min-y>+<height>`��

*��������Ϊ`backrgound-position: 100% 100%;`��*

So, using the `align` and `meetOrSlice` values of the `preserveAspectRatio` attribute, you can specify whether or not to scale the `viewBox` uniformly, how to align it inside the viewport, and whether or not it should be entirely visible inside the viewport.

���ԣ�ͨ��ʹ��`preserveAspectRatio`���Ե�`align`��`meetOrSlice`ֵ������������Ƿ�ͳһ����`viewBox`���Ƿ���ӿڶ��룬���ӿ����Ƿ������ɼ���

Sometimes, and depending on the size of the `viewBox`, some values may have similar results. For example, in the `viewBox="0 0 200 300"` example from earlier, some alignments are identical using different `align` values. The value of `meetOrSlice` is set to `meet`in this case so that the entire `viewBox` is contained inside the viewport.

��ʱ��ȡ����`viewBox`�ĳߴ磬һЩֵ���ܻᵼ�����ƵĽ��������������`viewBox="0 0 200 300"`�������У�һЩ������ȫ���˲�ͬ��`align`ֵ����ʱ���Ҫ����`meetOrSlice`��ֵΪ`meet`����֤`viewBox`������viewport�ڡ�

![](svg/viewbox-meet-align-same.jpg)

If we were to change the `meetOrSlice` value to `slice`, we'd get different results for different values. Notice how the viewBox is stretched so that it covers the entire viewport. The x-axis is stretched so that the 200 units cover the viewport's 800 units. In order for this to happen, and to maintain the aspect ratio of the viewbox, the y-axis gets "sliced off" at the bottom, but you can image it extending below the viewport's height.

������ǰ�`meetOrSlice`��ֵ�ĳ�`slice`����ͬ��ֵ���ǽ��õ���ͬ�Ľ����ע��viewBox��������������������ӿڵġ�x�ᱻ���쵽��200��λ�������ӿ�800��λ��Ϊ�˴ﵽ���Ŀ�ģ����ұ���viewbox�Ŀ�߱ȣ�y���ڵײ��������С���������������������ӿ��и߶��ϵ����졣

![](svg/viewbox-slice-align-same.jpg)

Of course, different `viewBox` values will also look different from the 200x300 we're using here. For the sake of brevity, I won't get into more examples, and I'll leave you to play with an interactive demo I created to help you better visualize how the `viewBox` and different `preserveAspectRatio` values work together when different values are used. You can check the interactive demo out by visiting the link in the next section.

��Ȼ����ͬ��`viewBox`ֵ��������ͬ�����������õ�200*300��Ϊ�˱��ּ�࣬���ǲ����оٸ�������ӣ�����Կ��Ҵ�����һЩ������ʾ����������õ��������`viewBox`��`preserveAspectRatio`�ڲ�ֵͬ�µ�Ч�����������һ�½��в鿴������ʾ���ӵ����ӡ�

But before we move to that, I just want to note that the mid-x, mid-y, max-x, and max-y values change if the values of the `<min-x>` and `<min-y>` change. You can play with the interactive demo and change these values to see how the axes and thus the alignment of the viewBox changes accordingly.

��������֮ǰ������Ҫ������ע�����`<min-x>` �� `<min-y>`ֵ�ı䣬��ômid-x, mid-y, max-x, �� max-y��ֵҲ�ᷢ���ı䡣������ڻ�����ʾ�иı���Щֵ���鿴���Լ��������`viewBox`�Ķ��뷽ʽ�ĸı䡣

The following image shows the effect of using `viewBox = "100 0 200 300"` on the position of the alignment axes. We're using the same example as earlier, but instead of having the `<min-x>` value be set to zero, we're setting it to 100. You can set them to any number value you want. Notice how the min-x, mid-x, and max-x axes change. The `preserveAspectRatio` used here is the default `xMinYMin meet`, which means that the mid-* axes are aligned with the middle axes of the viewport.

����ͼƬչʾ�˶�λ���λ��Ϊ`viewBox = "100 0 200 300"`ʱ��Ч������֮ǰ��һ�������ӣ��������ǰ�`<min-x>`��ֵ��Ϊ100������֮ǰ��0����������ó��κ�����Ҫ��ֵ��ע��min-x, mid-x, �� max-x������α仯�ġ�����ʹ�õ�`preserveAspectRatio`ֵΪĬ�ϵ�`xMinYMin meet`����ζ��mid-*����ӿ�����м���롣

![](svg/viewbox-axes-changed-min-x-min-y.jpg)

##The Interactive Demo
##������ʾ

The best way to understand how the viewport, `viewBox`, and different `preserveAspectRatio` values work and interact together is by visualizing them.

Ҫ���viewport, `viewBox`, �Լ���ͬ��`preserveAspectRatio`ֵ����ι�������÷����ǿ��ӻ�����ʾ��

For that purpose, I created a simple interactive demo that allows you to change the values of these attributes and see the result of the new values live.

�������Ŀ�ģ��Ҵ�����һ���򵥵Ļ�����ʾ������Ըı���Щ���Ե�ֵ���鿴��ֵ���µĽ����

![](svg/viewbox-demo-screenshot.jpg)

<a class="button" href="http://sarasoueidan.com/demos/interactive-svg-coordinate-system/index.html">Check the interactive demo out.</a>

I hope you found this article useful in understanding the SVG viewport, `viewBox`, and `preserveAspectRatio` concepts. If you'd like to learn more about SVG coordinate systems, like nesting coordinate systems, establishing new ones, and transformations in SVG, stay tuned for the remaining parts of this series. You can subscribe to the RSS (link below) or follow me on Twitter to stay updated. Thank you very much for reading!

��ϣ����ƪ�����ڰ��������SVG viewport, `viewBox`, �� `preserveAspectRatio` ����ʱ�����á��������Ҫ�˽�������SVG����ϵ�����ݣ�����Ƕ������ϵ������һ���µ�����ϵ�Լ�SVG�еı任�������Ķ���һϵ�н������Ĳ��֡������ͨ��RSS���ģ����������棩������Twitter�Ϲ�ע����ȡ������Ϣ����л����Ķ���