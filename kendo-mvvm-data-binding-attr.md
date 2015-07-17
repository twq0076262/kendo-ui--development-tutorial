# [Kendo UI 开发教程(12): Kendo MVVM 数据绑定(一) attr](http://www.imobilebbs.com/wordpress/archives/4633)

Kendo UI MVVM 数据绑定支持的绑定属性有 attr, checked, click, custom , disabled,enabled, events, html, invisible, , style, text ,value, visible ，这些属性可以绑定到 DOM 元素或是 Kendo UI 组件的属性。本篇介绍 attr 绑定。
attr 支持把 ViewModel 的属性或方法绑定到 DOM 元素的某个属性， 比如设置 hyperlink 的 herf 和 title 属性， image 元素的 src 或 alt 属性。 其基本用法为
attr: { attribute1: field1, attribute2: field2 }
其中 attribute1 和 attribute2 为 DOM 元素的属性名称， 而 field1,field2 为 ViewModel 对象的值域（属性）的名称。
比如：

```

<img id="logo" data-bind="attr: { src: imageSource, alt: imageAlt }" />
<script>
var viewModel = kendo.observable({
    imageSource: "http://www.kendoui.com/image/kendo-logo.png",
    imageAlt: "Kendo Logo"
});

kendo.bind($("#logo"), viewModel);
</script>

```

在本例中，image 元素的 src 和 alt 属性被绑定到 viewModel 对象的  imageSource 和 imageAlt 属性。 当调用 kendo.bind 方法，image 元素和下面 HTML 元素等效：

```

<img id="logo" src="http://www.kendoui.com/image/kendo-logo.png" alt="Kendo Logo"" />

```

此时，如果修改 viewModel 的 imageSource 和 imageAlt 属性的值，页面上显示的图片也随之发生变化。

![](images/23.jpg)

注意：如果需要绑定到 DOM 元素的 value 或 checked 属性，你需要使用 Kendo MVVM 的 value 和 checked 绑定方法。

attr 绑定也支持设置 HTML5 数据属性绑定，例如：

```

<div data-bind="attr: { data-foo: fooValue, data-bar: barValue }"></div>

<script>
var viewModel = kendo.observable({
    fooValue: "foo",
    barValue: "bar"
});

kendo.bind($("div"), viewModel);
</script>

```

Tags: [JavaScript](http://www.imobilebbs.com/wordpress/archives/tag/javascript), [Kendo UI](http://www.imobilebbs.com/wordpress/archives/tag/kendo-ui)