# [Kendo UI 开发教程(10): Kendo MVVM (一) 概述](http://www.imobilebbs.com/wordpress/archives/4626)

Model View ViewModel (MVVM)  是开发人员经常使用的一种设计模式，以实现数据模型（Model）和视图（View）的分离。MVVM 中的 ViewModel 部分负责把模型中的数据对象以某种方便的形式和 View 结合起来（通常是通过数据绑定的方式）。

Kendo MVVM 实现了 MVVN 设计模式，并且支持和 Kendo 框架的其它部分（如UI组件和数据源）的无缝连接。

# 准备开始

使用 MVVM 模式首先创建 ViewModel 对象，ViewModel 对象代表了可以使用 View 显示的数据对象，Kendo 框架中使用 kendo.observable 函数通过传入 JavaScript 对象的方法来定义一个 ViewModel 对象。比如：

```

var viewModel = kendo.observable({
    name: "John Doe",
    displayGreeting: function() {
        var name = this.get("name");
        alert("Hello, " + name + "!!!");
    }
});

```

然后使用 HTML 创建一个 View，这个 View 包含一个按钮和一个文本框。

```

<div id="view">
    <input data-bind="value: name" />
    <button data-bind="click: displayGreeting">Display Greeting</button>
</div>

```

其中文本框(input) 通 过data-bind 属性指明绑定到 ViewModel 对象的 name 域。 此时 name 域值发生变化将会反映到 UI 界面的 Input 输入框内容的变化。反之亦然，当 UI 输入框内容发生变化时，ViewModel 的 name 域也发生变化。
按钮的 click 事件绑定到 ViewModel 的 displayGreeting 方法。

最后，通过 bind 方法将 View 和 ViewModel 绑定起来。

kendo.bind($("#view"), viewModel);
完整的代码如下：

```

<!doctype html>
<html>
<head>
    <title>Kendo UI Web</title>
    <link href="styles/kendo.common.min.css" rel="stylesheet" />
    <link href="styles/kendo.default.min.css" rel="stylesheet" />
    <script src="js/jquery.min.js"></script>
    <script src="js/kendo.web.min.js"></script>

</head>
<body>
<div id="view">
    <input data-bind="value: name" />
    <button data-bind="click: displayGreeting">Display Greeting</button>
</div>

 <script>
     var viewModel = kendo.observable({
         name: "John Doe",
         displayGreeting: function () {
             var name = this.get("name");
             alert("Hello, " + name + "!!!");
         }
     });

     kendo.bind($("#view"), viewModel);
 </script>
</body>
</html>

```

# 数据绑定

数据绑定将 DOM 元素（或者 UI 组件）的属性绑定到 ViewModel 的某个属性或是方法。绑定通过设置 data-bind 属性，采用 “绑定名称 ： ViewModel 的属性或方法”的格式，也就是 value : name 的形式来指明。上面的例子使用了两种不同类型的绑定，value 和 click。 Kendo MVVM 也支持其它类型的绑定，如 source, html, attr ,visible,enable 等。 data-bind 也可以支持通过逗号分隔的属性列表。 Kendo MVVM 数据绑定也支持嵌套的 ViewModel 属性。

比如下例 把 div 绑定到 person.name:

```

<div data-bind="text: person.name">
</div>
<script>
var viewModel = kendo.observable({
    person: {
        name: "John Doe"
    }
});
kendo.bind($("div"), viewModel);
</script>

````

要注意的是 data-bindings 的值不是 Javascript 代码，不可以使用在 data-bindings 中使用 javascript 方法，比如

```

<div data-bind="text: person.name.toLowerCase()"></div>

```

要实现上面使用小写的功能，可以使用下面的实现：

```
<div data-bind="text: person.lowerCaseName"></div>

<script>
var viewModel = kendo.observable({
    person: {
        name: "John Doe",
        lowerCaseName: function() {
            return this.get("name").toLowerCase();
        }
    }
});
kendo.bind($("div"), viewModel);
</script>

```

Tags: [JavaScript](http://www.imobilebbs.com/wordpress/archives/tag/javascript), [Kendo UI](http://www.imobilebbs.com/wordpress/archives/tag/kendo-ui)