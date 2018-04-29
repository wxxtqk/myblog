---
title: angualar--基本应用
categories:
  -angular1.x.x
---
## 如何使用angular中control
在angular中，最好不好使用controller里面在嵌套controller，最好用一个服务，
借用慕课网中老师的图片[慕课](http://www.imooc.com/video/2685)
![](/img/angular/01/01.png)
而我们应该这样去做，把公用的部分写在service中，然后让控制去调用它，而不是去继承
![](/img/angular/01/02.png)
在使用controller使用过程中的注意点
1、不要试图去复用controller，一般一个控制器字负责一小块儿试图：其一因为一般只负责一小块儿的视图，所以复用的意义不大，还有一个就是controller里面写着大量的业务逻辑，复用后可用性也不高，并除非分的很细.
2、最好不要在controller进行DOM操作，因为控制里面主要是写业务逻辑的，angular如果要操作DOM的话，可以封装在另外一个组件(directive),如果要操作DOM的话，将会是非常的慢的，会去渲染，重新布局，所以angular建议不直接操作DOM元素
3、不要在controller中做数据格式化，因为angular中有比较好的表单控件
4、不要在controller中做数据的过滤操作，因为angular中有很好的的$filter服务
5、一般来说，controller是不会相互调用的，控制器之间的交互会通过事件进行。
## 数据模型
下面来看一个简单的例子
```html
<!DOCTYPE html>
<html lang="en" ng-app>
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<script src="angular.js"></script>
</head>
<body>
	<div>
		<input ng-model="text">
		<p>{{text}},world</p>
	</div>
</body>
</html>
```
![](/img/angular/01/03.gif)
从上面的代码和结果中，我们可以看到页面中除了引入了angular.js外，没有引入其它的js，但是为什么我在input中输入，下面p标签的值也跟着变化呢？那是因为当如果angularjs后，js启动起来，会去找ng-app，当找到ng-app后，然后就会认为ng-app这个标签里面所有的内容都归angular去管，然后就会去找这个标签里面所有的指令，然后对该指令进行编译操作，当找到ng-model后，会把text生成数据模型，这个数据模型挂着$rootScope（根）下，只要是在这个root下都可以进访问，所以下面的{text}就可以访问了
## 视图
在angular里中一般会用到directive来实现视图
首先我们在HTML页面中自定义一个标签,html代码
```html
	<hello-world></hello-world>
```
directive指令中的js代码
```javascript
	var app  = angular.module("app",[])
	app.directive("helloword",function(){
		return {
			restrict:'E',
			template:"<div>hello,world</div>",
			replace:true
	}
	})
```
我们在HTML代码中定义了一个hello-world标签，然后用directive去实现它，在directive中第一个参数就是helloword就是对应的hello-world标签，然后把hello-world标签替换成template里面的值,所以在页面上会会看到的是 "hello,world"
## $scope(我理解成作用域)
在里面总共有两个，一个是$scope(当前controller下的作用域能够访问)，一个就是$rootScope(当前controller一下的都可以访问)，angular里面的作用域是以树形结构。在angular中有两个事件传播，一个是$emit,一个是$broadcast,emit事件是可以同级和向上传播，而broadcast是同级和向下传播，这两个事件可以详细百度一下
下面看看最主要的$scope
1、$scope是一个对象
2、$scope会提供一些方法例如$watch()和$apply()
3、$scope是表达式的执行环境（或者叫作用域）
4、$scope是一个树形结构的，与DOM标签平行
5、子$scope对象会继承父$scope上的属性和方法
6、每个angular应用只有一个根$scope对象（一般位于ng-app上）
7、$scope可以传播时间，类似DOM事件，可以向上也可以向下
8、$scope不仅是MVC的基础，也是后面实现双数据绑定的基础
10、可以用angular.element($0).scope()进行调试，也可以在浏览器中装一个插件进行调试
## ng-bind 用法
如果在网速比较慢的情况下，有时候会看到 {} 这边模型绑定的大括号，所以此时用ng-bind 话就不会让用户看到，一般在首页用ng-bind