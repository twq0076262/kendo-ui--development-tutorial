# [Kendo UI 开发教程(11): Kendo MVVM (二) ObservableObject 对象](http://www.imobilebbs.com/wordpress/archives/4630)

# 概述

Kendo MVVM 框架关键的一个部分为 ViewModel，它主要是通过 kendo.data.ObserableObject 来提供支持的。它可以监控改变（ UI 变化或是值的变化）并通知关心该变化的组件。 本篇以下 ViewModel 和  ObservableObject 代表同一对象。

为了创建一个 ObservableObject 对象，可以通过创建一个新 kendo.data.ObservableObject 实例或是使用 kendo.observable 方法，这两种方法效果相同。

例如：

```

var viewModel1 = new kendo.data.ObservableObject( {
  field1: "value1",
  field2: "value2"
});

var viewModel2 = kendo.observable( {
  field1: "value1",
  field2: "value2"
});

```

kendo.bind 方法内部实现时自动将给定的 ViewModel 对象转换为一个 ObservableObject 对象，除非传入的参数类型已经是一个 ObservableObject 对象。

注：如果某个 ViewModel 对象在初始后以后还会使用到（在调用 kendo.bind 之前或之后），则必须使用 kendo.observable 方法或是 new kendo.data.ObservableObject 来创建一个 ViewModel 对象。比如：

```

var viewModel = kendo.observable({
name: "John Doe"
});

viewModel.set("name", "Jane Doe"); // use the View-Model object after initialization

```

如果 ViewModel 对象在初始化后不再访问这个对象，那么你可以使用普通 的JavaScript 对象，此时 kendo.bind 方法不会把原始的 ViewMode 对象转化为 kendo.data.ObservableObject. 例如，下面的代码出错：

```

var viewModel = {
   name: "John Doe"
};

kendo.bind(document.body, viewModel);

/*
The following statement  will fail because the View-Model
is not an instance of kendo.data.ObservableObject.
*/
viewModel.set("name", "Jane Doe");

```

因此强烈建议总是使用 kendo.observable 来初始化一个 ViewModel 对象。

# 读取 ObservableObject

使用 get 方法来读取 ObservableObject 对象的属性。例如：

```
var viewModel = kendo.observable({
 name: "John Doe"
});

var name = viewModel.get("name");
alert(name); // shows "John Doe"

```

get 也支持读取嵌套的属性，例如：

```
var viewModel = kendo.observable({
 person: {
     name: "John Doe"
 }
});
var personName = viewModel.get("person.name");
alert(personName); // shows "John Doe"

```

# 设置 ObservableObject 属性

使用 set 方法来设置 ObservableObject 属性，例如：

```

var viewModel = kendo.observable({
    name: "John Doe"
});

viewModel.set("name", "Jane Doe"); //set the "name" field to "Jane Doe"

var name = viewModel.get("name");
alert(name); // shows "Jane Doe"

```

同样，set 也支持设置嵌套的属性，例如：

```

var viewModel = kendo.observable({
 person: {
     name: "John Doe"
 }
});

viewModel.set("person.name", "Jane Doe");

var personName = viewModel.get("person.name");
alert(personName); // shows "Jane Doe"

```

创建关联属性（或者成为计算后属性）
在应用中常常需要把某个 ViewModel 的属性重新格式成适合 View 显示的形式，在这种情况可以通过创建一个新的关联属性来实现，比如：

```

<span data-bind="text: fullName"></span>
<script>
var viewModel = kendo.observable({
    firstName: "John",
    lastName: "Doe",
    fullName: function() {
        return this.get("firstName") + " " + this.get("lastName");
    }
});

kendo.bind($("span"), viewModel);
</script>

```

在这个例子中 fullName 为一关联属性，它依赖于 firstName 和 lastName， 使用 set 修改 firstName 或是 LastNam e后，FullName 的值也随之变化。

要注意的是 fullName 的实现，对 firstName,和 lastName 的访问，是通过 get 方法来实现的，如果使用下面的方法：

```

var viewModel = kendo.observable({
    firstName: "John",
    lastName: "Doe",
    fullName: function() {
        return this.firstName + " " + this.lastName;
    }
});

```

上面代码直接使用 this.firstName 来访问 ObserableObject 的属性，在这种情况下，fullName 不会跟踪 firstName 和 lastName 的变化，此时改变 firstName 和 lastName，fullName 的值不变，因此建议总是使用 get 来访问某个属性。

Tags: [JavaScript](http://www.imobilebbs.com/wordpress/archives/tag/javascript), [Kendo UI](http://www.imobilebbs.com/wordpress/archives/tag/kendo-ui)