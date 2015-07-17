# [Kendo UI 开发教程(17): Kendo MVVM 数据绑定(六) Html](http://www.imobilebbs.com/wordpress/archives/4652)

Html 绑定可以使用 ViewMod e 的属性来设置 DOM 元素的 innerHTML 属性。如果 ViewModel 的属性的数据类型不是字符串，比如（Text， Number 或者 Date),那么会调用 toString() 方法，将这些值转为字符串。
注意:如果需要设置 input,textarea 或是 select 的值，需要使用 value 绑定。
例如：

```

<span data-bind="html: name"></span>
<script>
var viewModel = kendo.observable({
    name: "John Doe"
});

kendo.bind($("span"), viewModel);
</script>

```

这个结果显示如下 html 元素：

```

<span>John Doe</span>

```

如果 ViewModel 的值包含 HTML 标记，这些标记和作为最后结果显示出来，比如：

```

<span data-bind="html: name"></span>
<script>
var viewModel = kendo.observable({
    name: "<strong>John Doe</strong>"
});

kendo.bind($("span"), viewModel);
</script>

```

显示如下：

**John Doe**

如果只想显示 ViewModel 的值，可以使用 text 绑定。

Tags: [JavaScript](http://www.imobilebbs.com/wordpress/archives/tag/javascript), [Kendo UI](http://www.imobilebbs.com/wordpress/archives/tag/kendo-ui)