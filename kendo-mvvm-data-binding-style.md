# [Kendo UI 开发教程(19): Kendo MVVM 数据绑定(八) Style](http://www.imobilebbs.com/wordpress/archives/4658)

Style 绑定可以通过 ViewModel 绑定到 DOM 元素 CSS 风格属性，例如：

```

<span data-bind="style: {color: priceColor, fontWeight: priceFontWeight},
             text: price"></span>

<script>
var viewModel = kendo.observable({
    price: 42,
    priceColor: function() {
        var price = this.get("price");

        if (price <= 42) {
            return "#00ff00";
        } else {
            return "#ff0000";
        }
    },
    priceFontWeight: function() {
        var price = this.get("price");

        if (price <= 42) {
            return "bold";
        } else {
            return ""; //will reset the font weight to its default value
        }
    }
});

kendo.bind($("span"), viewModel);
</script>

```

这个例子显示：

```

<span style="color: #00ff00; font-weight: bold">42</span>

```

42

要注意的是 CSS 属性的名称，如果 CSS 名称中含有连字符（-），比如 font-weight, font-size ,background-color 等，在使用时需要省略到连字符，使用 camel 风格的命名，如 fontWeight, fontSize,backgroundColor 等。

Tags: [JavaScript](http://www.imobilebbs.com/wordpress/archives/tag/javascript), [Kendo UI](http://www.imobilebbs.com/wordpress/archives/tag/kendo-ui)