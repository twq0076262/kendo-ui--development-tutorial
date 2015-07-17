# [Kendo UI 开发教程(8): Kendo UI 特效概述](http://www.imobilebbs.com/wordpress/archives/4612)

Kendo UI Fx 提供了一个丰富，可扩展，性能经过优化的工具集合用来完成 HTML 元素的过渡显示。每种特效近可能的使用 CSS Transition ，对于一些老版本浏览器使用修改属性的方法作为补充。所有动画可以反向显示从而可以方便的实现元素的显示和隐藏。 本篇介绍了 Kendo UI 特效的概要，完整的文档可以参考 [API](http://docs.telerik.com/kendo-ui/api/javascript/effects/common) 文档

# 准备开始

所有 Kendo UI 特效都是通过 kendo.fx JQuery 选择器封装来创建，每个封装支持显示多种特效。例如：

```

<div id="foo">
    I will be animated
</div>

<script>
    var effectWrapper = kendo.fx($("#foo"));
    var fadeOutEffect = effectWrapper.fadeOut();
    fadeOutEffect.play();
</script>

```

和 jQuery 方法一样，kendo UI fx 也支持方法链，比如上面代码可以简化为：

```

<div id="foo">
    I will be animated
</div>

<script>
    kendo.fx($("#foo")).fadeOut().play();
</script>

```

# 指定特效显示的方向指定特效显示的方向

大部分特效可以指定多个方向。可以通过特效构造方法的第一个参数来指定方向，或者通过调用构造方法的快捷方法来指明方向。比如下面三种方法的效果是一样的。

大部分特效可以指定多个方向。可以通过特效构造方法的第一个参数来指定方向，或者通过调用构造方法的快捷方法来指明方向。比如下面三种方法的效果是一样的。

```

<div id="foo">
    I will be animated
</div>

<script>
    var fadeOut1 = kendo.fx($("#foo")).fadeOut();
    var fadeOut2 = kendo.fx($("#foo")).fade("out");
    var fadeOut3 = kendo.fx($("#foo")).fade().direction("out");

    //Call .play() to run any of the above animations
</script>
```

组合特效
可以将多个特效组合中一起。比如：

```
<div id="foo">
    I will be faded out and zoomed out.
</div>

<script>
    var effectWrapper = kendo.fx($("#foo"));
    var fadeOutEffect = effectWrapper.fadeOut();
    fadeOutEffect.add(effectWrapper.zoomOut());
    fadeOutEffect.play();
    // Calling reverse will zoom in and fade in.
</script>
```

组合特效也可以同时应用到多个元素，这时需要通过 $when 方法。比如下面代码：

```

<div id="foo">
    I will fade out.
</div>
<div id="baz">
    I will also fade out.
</div>

<script>
    //Use jQuery Deferred to chain multiple effects
    var eleFoo = $("#foo"),
        eleBaz = $("#baz");

    $.when(kendo.fx(eleFoo).fadeOut().play(),
                kendo.fx(eleBaz).fadeOut().play()).then(function(){
            //This will be called when both animations are done
            alert("Both elements faded!");
        });
</script>
```

# Kendo UI 支持的特效种类
Kendo UI 支持下面几种特效，具体请参见其文档

- [Expand](http://docs.kendoui.com/api/framework/fx/expand)
- [Fade](http://docs.kendoui.com/api/framework/fx/fade)
- [Flip](http://docs.telerik.com/kendo-ui/api/javascript/effects/flip)
- [PageTurn](http://docs.telerik.com/kendo-ui/api/javascript/effects/pageturn)
- [SlideIn](http://docs.telerik.com/kendo-ui/api/javascript/effects/pageturn)
- [Tile](http://docs.kendoui.com/api/framework/fx/tile)
- [Transfer](http://docs.kendoui.com/api/framework/fx/transfer)
- [Zoom](http://docs.kendoui.com/api/framework/fx/zoom)

Tags: [JavaScript](http://www.imobilebbs.com/wordpress/archives/tag/javascript),[jQuery](http://www.imobilebbs.com/wordpress/archives/tag/jquery),[Kendo UI](http://www.imobilebbs.com/wordpress/archives/tag/kendo-ui)
 