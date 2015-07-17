# [Kendo UI 开发教程(7): Kendo UI 模板概述](http://www.imobilebbs.com/wordpress/archives/4608)

Kendo UI 框架提供了一个易用，高性能的 JavaScript 模板引擎。通过模板可以创建一个 HTML 片段然后可以和 JavaScript 数据合并成最终的 HTML 元素。

Kendo 模板侧重于 UI 显示，支持关键的模板功能，着重于性能而不是语法上的方便。

模板语法
Kendo 模板使用了一种称为“#”的语法形式，使用这种语法，#用来表明模板中的某个部分可以使用 JavaScript 数据来替代。

用三种方式使用 # 语法：

1. 显示字面量 #=#
2. 显示HTML元素 #：#
3. 执行任意的Javascript代码  #if() {# …#}#

注意：如何你的模板中包含有“#”字符，不是用来绑定的部分，你必须使用转义字符，否则会引起模板编译错误。 你可以通过“\\#”转义需要显示“#”的地方。

# 显示原始数据

显示数据的本来的形式是使用模板的一个最基本的用法，使用 Kendo UI 模板，可以使用如下类似的代码：

```

var template = kendo.template("<div id='box'>#= firstName #</div>")

```

上面代码创建了“编译”过的嵌入式模板，使用这个模板可以用来显示数据，比如下面的代码

```
<div id="example"></div>
<script>
	var template = kendo.template("<div id='box'>#= firstName #</div>");
	var data = { firstName: "Todd" }; //A value in JavaScript/JSON
	var result = template(data); /Pass the data to the compiled template
	$("#example").html(result); //display the result
</script>

```

通过模板与数据的合并，最终显示“Todd”。

# 显示 HTML 数据

如果你需要显示经过 HTML 编码过的数据，使用 Kendo UI 模板可以自动处理这些编码过的 HTML 元素，但需要使用不同的语法 #: …#,例如：

```

var template = kendo.template("<div id='box'>#: firstName #</div>");

```

完整的示例如下：

```

<div id="example"></div>
<script>
	var template = kendo.template("<div id='box'>#: firstName #</div>");
	var data = { firstName: "<b>Todd</b>" }; //Data with HTML tags
	var result = template(data); //Pass the data to the compiled template
	$("#example").html(result); //display the resulting encoded HTML Output (<b>Todd</b>)
</script>

```

这个例子的显示结果为

```

<b>Todd </b>

```

而不是 Todd，如果需要显示 Todd ，则需要使用#= # 语法，显示 HTML 编码的一个主要作用是当你无需再模板中显示 HTML 标记，而是把整个标记和其内容作为字符串显示出来。

使用外部模板和表达式
在模板中也可以使用表达式，Kendo UI 支持者模板中执行 JavaScript 代码，在模板中使用 JavaScript 代码的方法是在 JavaScript 语句的前后加上#，比如下面模板显示一组列表：

```

<script id="javascriptTemplate" type="text/x-kendo-template">
<ul>
# for (var i = 0; i < data.length; i++) { #
	<li>#= data[i] #</li>
# } #
</ul>
</script>

```

然后为了使用这个模板，可以通过模板的 id ,通过 kendo.template 创建这个模板，然后和数据合并，比如：

```
<div id="example"></div>

<script id="javascriptTemplate" type="text/x-kendo-template">
	<ul>
	# for (var i = 0; i < data.length; i++) { #
		<li>#= data[i] #</li>
	# } #
	</ul>
</script>

<script type="text/javascript">
	//Get the external template definition using a jQuery selector
	var template = kendo.template($("#javascriptTemplate").html());

	//Create some dummy data
	var data = ["Todd", "Steve", "Burke"];

	var result = template(data); //Execute the template
	$("#example").html(result); //Append the result
</script>

```

![](images/20.jpg)

可以看到模板执行了 JavaScipt 的 for 循环，并且我们使用了外部模板，外部模板的定义使用 type=”text/x-kendo-template”来定义，并通过其id来访问这个外表模板。
在模板中也可以定义变量，使用这个自定义变量的方法和使用字面量的方法类似。比如定义一个变量 myCustomVariable

```

<script id="javascriptTemplate" type="text/x-kendo-template">
	# var myCustomVariable = "foo"; #
	<p>
		#= myCustomVariable #
	</p>
</script>

```

# 嵌入式模板 vs 外部模板 

Kendo UI 模板可以使用嵌入式模板和外部模板：

- inline: 使用 JavaScript 字符串定义
- external: 使用 HTML Script 块定义
 

嵌入式模板使用比较简单的情况，对于比较复杂的模板一般使用外部模板。外部模板的定义的基本格式如下：

```

 <script type="text/x-kendo-template" id="myTemplate">
	<!--Template content here-->
</script>

```

外部模板必须定义一个 id,这样你才可以通过 id 来访问这个模板： 

```

//extract the template content from script tag
var templateContent = $("#myTemplate").html(); 
//compile a template
var template = kendo.template(templateContent);

```

使用外部模板，你可以使用任意合法的 HTML 元素和 JavaScirpt，只需语法正确，比如：

```

<ul id="users"></ul>

<script type="text/x-kendo-template" id="myTemplate">
	#if(isAdmin){#
		<li>#: name # is Admin</li>
	#}else{#
		<li>#: name # is User</li>
	#}#
</script>

<script type="text/javascript">
	var templateContent = $("#myTemplate").html();
	var template = kendo.template(templateContent);

	//Create some dummy data
	var data = [
		{ name: "John", isAdmin: false },
		{ name: "Alex", isAdmin: true }
	];

	var result = kendo.render(template, data); //render the template

	$("#users").html(result); //append the result to the page
</script>

```

![](images/21.jpg)

Tags: [JavaScript, Kendo UI](http://www.imobilebbs.com/wordpress/archives/tag/kendo-ui)