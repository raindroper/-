# 前端开发规范 #

> 本规范为本人经验及网络资料梳理整合而来，如有疏漏和错误请及时提出。

- [命名篇](#common)
- [html篇](#html)
- [css篇](#css)
- [js篇](#js)
- [vue篇](#vue)

----------

<h2 id="common">命名篇</h2>
> 驼峰命名法：
> Pascal Case 大驼峰式命名法：首字母大写。eg：StudentInfo、UserInfo、ProductInfo
Camel Case 小驼峰式命名法：首字母小写。eg：studentInfo、userInfo、productInfo

### 文件资源命名 ###

- 文件名不得含有空格
- 文件名建议只使用小写字母，不使用大写字母。( 为了醒目，某些说明文件的文件名，可以使用大写字母，比如README、LICENSE。 )
- 文件名包含多个单词时，单词之间建议使用半角的连词线 ( - ) 分隔。
- 引入资源使用相对路径，不要指定资源所带的具体协议 ( http:,https: ) ，除非这两者协议都不可用。

		<script src="//cdn.com/vue.min.js"></script>

### 变量命名 ###

**小驼峰**

**类型（前缀为名词）+对象描述的方式**

	let dialogTitle = "dialogTitle"

### 函数 ###

**小驼峰**

**前缀为动词**

动词 | 含义 | 返回值
------------ | ------------- | ------------
can | 判断是否可执行某个动作 ( 权限 )  | 函数返回一个布尔值。true：可执行；false：不可执行
has | 判断是否含有某个值  | 函数返回一个布尔值。true：含有此值；false：不含有此值
is | 判断是否为某个值  | 函数返回一个布尔值。true：为某个值；false：不为某个值
get | 获取某个值   | 函数返回一个非布尔值
set | 	设置某个值  | 无返回值、返回是否设置成功或者返回链式对象

	function getName() {
		return this.name;
	}

### 常量 ###

**全部大写**

**使用大写字母和下划线，下划线用以分割单词**

	const MAX_COUNT = 10
	const url = 'http://www.baidu.com'

### 函数（方法）注释 ###

	/** 
	* 函数说明 
	* @关键字 
	*/

<h2 id="html">html篇</h2>

### 脚本加载 ###

所有浏览器中：

	<html>
		<head>
			<link rel="stylesheet" href="main.css">
	  	</head>
	  	<body>
	   		<!-- body goes here -->
	
	   		<script src="main.js" async></script>
	  	</body>
	</html>

只需兼容现代浏览器：

	<html>
	  <head>
	    <link rel="stylesheet" href="main.css">
	    <script src="main.js" async></script>
	  </head>
	  <body>
	    <!-- body goes here -->
	  </body>
	</html>

### 语义化 ###

> 语义化是指：根据元素其被创造出来时的初始意义来使用它。
> 
> 意思就是用正确的标签干正确的事，而不是只有div和span。

合理使用header nav article p footer aside section ul ol

### alt标签不为空 ###

`<img>`标签的 alt 属性指定了替代文本，用于在图像无法显示或者用户禁用图像显示时，代替图像显示在浏览器中的内容。

### 结构、表现、行为三者分离 ###

尽量在文档和模板中只包含结构性的 HTML；而将所有表现代码，移入样式表中；将所有动作行为，移入脚本之中。

在文档和模板中也尽量少地引入样式和脚本文件

- 不使用超过一到两张样式表
- 不使用超过一到两个脚本（学会用合并脚本）
- 不使用行内样式（`<style>.no-good {}</style>`）
- 不在元素上使用 style 属性（`<hr style="border-top: 5px solid black">`）
- 不使用行内脚本（`<script>alert('no good')</script>`）
- 不使用表象元素（`i.e. <b>, <u>, <center>, <font>, <b>`）
- 不使用表象 class 名（`i.e. red, left, center`）

### HTML只关注内容 ###

- HTML只显示展示内容信息
- 不要引入一些特定的 HTML 结构来解决一些视觉设计问题
- 不要将`img`元素当做专门用来做视觉设计的元素
- 样式上的问题应该使用css解决

<h2 id="css">css篇</h2>

### id和class的命名 ###

ID和class的名称总是使用可以反应元素目的和用途的名称，或其他通用的名称，代替表象和晦涩难懂的名称

反例：

	.fw-800 {
	  font-weight: 800;
	}
	
	.red {
	  color: red;
	}

推荐：

	.heavy {
	  font-weight: 800;
	}
	
	.important {
	  color: red;
	}

### 合理的使用ID ###

一般情况下ID不应该被用于样式，并且ID的权重很高，所以不使用ID解决样式的问题，而是使用class

### css选择器中避免使用标签名 ###

从结构、表现、行为分离的原则来看，应该尽量避免css中出现HTML标签，并且在css选择器中出现标签名会存在潜在的问题。

### 使用子选择器 ###

这可能会导致疼痛的设计问题并且有时候可能会很耗性能。

不推荐：

	.content .title {
	  font-size: 2rem;
	}

推荐：

	.content > .title {
	  font-size: 2rem;
	}

### 尽量使用缩写属性 ###

尽量使用缩写属性提高代码效率和可读性，比如font属性。

反例：

	border-top-style: none;
	font-family: palatino, georgia, serif;
	font-size: 100%;
	line-height: 1.6;
	padding-bottom: 2em;
	padding-left: 1em;
	padding-right: 1em;
	padding-top: 0;

推荐：

	border-top: 0;
	font: 100%/1.6 palatino, georgia, serif;
	padding: 0 1em 2em;

### 0后面不带单位 ###

省略0后面的单位

<h2 id="js">JS篇</h2>

### 避免全局命名空间污染 ###

防止全局命名空间被污染，我们通常的做法是将代码包裹成一个 IIFE(Immediately-Invoked Function Expression)，创建独立隔绝的定义域。也使得内存在执行完后立即释放。

IIFE 还可确保你的代码不会轻易被其它全局命名空间里的代码所修改（i.e. 第三方库，window 引用，被覆盖的未定义的关键字等等）。

推荐：

	// We declare a IIFE and pass parameters into the function that we will use from the global space
	(function(log, w, undefined){
	  'use strict';
	
	  var x = 10,
	      y = 100;
	
	  // Will output 'true true'
	  log((w.x === undefined) + ' ' + (w.y === undefined));
	
	}(window.console.log, window));

推荐IIFE写法：

	(function(){
	  'use strict';
	
	  // Code goes here
	
	}());

### 严格模式 ###

ECMAScript 5 严格模式可在整个脚本或独个方法内被激活。它对应不同的 javascript 语境会做更加严格的错误检查。严格模式也确保了 javascript 代码更加的健壮，运行的也更加快速。

严格模式会阻止使用在未来很可能被引入的预留关键字。

你应该在你的脚本中启用严格模式，最好是在独立的 IIFE 中应用它。避免在你的脚本第一行使用它而导致你的所有脚本都启动了严格模式，这有可能会引发一些第三方类库的问题。

### 变量声明 ###

使用let，const来声明变量

### 使用箭头函数 ###

使用箭头函数 => 来声明函数

### 使用严格等于 ###

使用 === 精确的比较操作符，避免js的类型转换造成的困扰

### 为函数的参数设置默认值 ###
	
	function setCourse(courseName = 'chinese') {
		return courseName
	}

### 不使用eval() 函数 ###

eval()函数的作用是返回任意字符串，当作js代码来处理。会带来安全隐患

### this关键字 ###

只在对象构造器、方法和在设定的闭包中使用 this 关键字。

- 在构造函数中
- 在对象的方法中（包括由此创建出的闭包内）

<h2 id="vue">vue</h2>

### 组建名为多个单词 ###

> 组件名应该始终是多个单词的，根组件 App 除外。

正例：

	export default {
	  name: 'TodoItem',
	  // ...
	}

### 组件数据 ###

> 组件的 data 必须是一个函数。
> 
> 当在组件中使用 data 属性的时候 (除了 new Vue 外的任何地方)，它的值必须是返回一个对象的函数。

正例：

	// In a .vue file
	export default {
	  data () {
	    return {
	      foo: 'bar'
	    }
	  }
	}
	// 在一个 Vue 的根实例上直接使用对象是可以的，
	// 因为只存在一个这样的实例。
	new Vue({
	  data: {
	    foo: 'bar'
	  }
	})

### Prop定义 ###

> Prop 定义应该尽量详细。
> 
> 在你提交的代码中，prop 的定义应该尽量详细，至少需要指定其类型。

	props: {
	  status: String
	}
	// 更好的做法！
	props: {
	  status: {
	    type: String,
	    required: true,
	    validator: function (value) {
	      return [
	        'syncing',
	        'synced',
	        'version-conflict',
	        'error'
	      ].indexOf(value) !== -1
	    }
	  }
	}

###  为v-for设置键值 ###

> 总是用 key 配合 v-for。
> 
> 在组件上_总是_必须用 key 配合 v-for，以便维护内部组件及其子树的状态。甚至在元素上维护可预测的行为，比如动画中的对象固化 (object constancy)，也是一种好的做法。

	<ul>
	  <li
	    v-for="todo in todos"
	    :key="todo.id"
	  >
	    {{ todo.text }}
	  </li>
	</ul>

### 避免 v-if 和 v-for 用在一起 ###

> 永远不要把 v-if 和 v-for 同时用在同一个元素上。
> 
> - 为了过滤一个列表中的项目 (比如 v-for="user in users" v-if="user.isActive")。在这种情形下，请将 users 替换为一个计算属性 (比如 activeUsers)，让其返回过滤后的列表。
> - 为了避免渲染本应该被隐藏的列表 (比如 v-for="user in users" v-if="shouldShowUsers")。这种情形下，请将 v-if 移动至容器元素上 (比如 ul, ol)。

正例：

	<ul v-if="shouldShowUsers">
	  <li
	    v-for="user in users"
	    :key="user.id"
	  >
	    {{ user.name }}
	  </li>
	</ul>

反例：

	<ul>
	  <li
	    v-for="user in users"
	    v-if="shouldShowUsers"
	    :key="user.id"
	  >
	    {{ user.name }}
	  </li>
	</ul>


### 为组件样式设置作用域 ###

> 对于应用来说，顶级 App 组件和布局组件中的样式可以是全局的，但是其它所有组件都应该是有作用域的。
> 
> 这条规则只和单文件组件有关。你不一定要使用 scoped 特性。设置作用域也可以通过 CSS Modules，那是一个基于 class 的类似 BEM 的策略，当然你也可以使用其它的库或约定。
> 
> 不管怎样，对于组件库，我们应该更倾向于选用基于 class 的策略而不是 scoped 特性。  
> 
> 这让覆写内部样式更容易：使用了常人可理解的 class 名称且没有太高的选择器优先级，而且不太会导致冲突。

	<template>
	  <button class="c-Button c-Button--close">X</button>
	</template>
	
	<!-- 使用 BEM 约定 -->
	<style>
	.c-Button {
	  border: none;
	  border-radius: 2px;
	}
	
	.c-Button--close {
	  background-color: red;
	}
	</style>

### 组件文件 ###

> 要有能够拼接文件的构建系统，就把每个组件单独分成文件。
当你需要编辑一个组件或查阅一个组件的用法时，可以更快速的找到它。

### 单文件组件文件的大小写 ###

> 单文件组件的文件名应该要么始终是单词大写开头 (PascalCase)，要么以中划线分割单词

	components/
	|- MyComponent.vue

	components/
	|- my-component.vue

### 基础组件名 ###

> 应用特定样式和约定的基础组件 (也就是展示类的、无逻辑的或无状态的组件) 应该全部以一个特定的前缀开头，比如 Base、App 或 V。

正例：

	components/
	|- BaseButton.vue
	|- BaseTable.vue
	|- BaseIcon.vue

反例：

	components/
	|- MyButton.vue
	|- VueTable.vue
	|- Icon.vue

### 单例组件名 ###

> 只应该拥有单个活跃实例的组件应该以 The 前缀命名，以示其唯一性。
> 
> 这不意味着组件只可用于一个单页面，而是每个页面只使用一次。这些组件永远不接受任何 prop，因为它们是为你的应用定制的，而不是它们在你的应用中的上下文。如果你发现有必要添加 prop，那就表明这实际上是一个可复用的组件，只是目前在每个页面里只使用一次。

### 紧密耦合的组件名 ###

> 和父组件紧密耦合的子组件应该以父组件名作为前缀命名。
> 
> 如果一个组件只在某个父组件的场景下有意义，这层关系应该体现在其名字上。因为编辑器通常会按字母顺序组织文件，所以这样做可以把相关联的文件排在一起。

正例：

	components/
	|- TodoList.vue
	|- TodoListItem.vue
	|- TodoListItemButton.vue
	components/
	|- SearchSidebar.vue
	|- SearchSidebarNavigation.vue

### 组件名中的单词顺序 ###

> 组件名应该以高级别的 (通常是一般化描述的) 单词开头，以描述性的修饰词结尾。

	components/
	|- SearchButtonClear.vue
	|- SearchButtonRun.vue
	|- SearchInputQuery.vue
	|- SearchInputExcludeGlob.vue
	|- SettingsCheckboxTerms.vue
	|- SettingsCheckboxLaunchOnStartup.vue

### 模板中简单的表达式 ###

> 组件模板应该只包含简单的表达式，复杂的表达式则应该重构为计算属性或方法。
> 
> 复杂表达式会让你的模板变得不那么声明式。我们应该尽量描述应该出现的是什么，而非如何计算那个值。而且计算属性和方法使得代码可以重用。

### scoped 中不要使用元素选择器 ###

> 元素选择器应该避免在 scoped 中出现。
> 
> 在 scoped 样式中，类选择器比元素选择器更好，因为大量使用元素选择器是很慢的。

### 不要使用隐性的父子组件通信 ###

> 应该优先通过 prop 和事件进行父子组件之间的通信，而不是 this.$parent 或改变 prop。


