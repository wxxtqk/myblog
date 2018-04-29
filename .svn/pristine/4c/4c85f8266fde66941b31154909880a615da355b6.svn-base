---
title: angualar--directive的用法
categories:
  -angular1.x.x
---
## directive的基本用法
首先我们来看一下简单的例子
```html
<!DOCTYPE html>
<html lang="en" ng-app="app">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<script src="angular.js"></script>
</head>
<body>
	<div>
		<angular></angular>
	</div>
</body>
<script type="text/javascript">
angular.module('app', []).directive('angular',function(){
	return {
		 restrict: 'E', // E = Element, A = Attribute, C = Class, M = Comment
		 template: '<div>hello,angular</div>',
		// templateUrl: '', 这里是html的模板的路径，如果需要的文本比较长的话，可以把模板单独提出来放在一个文件中
		 replace: true,
		// transclude: true,
		// compile: function(tElement, tAttrs, function transclude(function(scope, cloneLinkingFn){ return function linking(scope, elm, attrs){}})),
		link: function($scope, iElm, iAttrs, controller) {
			
		}
	};
});
</script>
</html>
```
在页面上的输出结果为
![](/img/angular/02/01.png)
在directive中，我看来详细的看一下里面配置
1、restrict中总共有四个，分别是E表示Element（元素）、A表示Attribute(属性)、C表示Class(表示html类)、M表示Comment(注释),下面我把代码做一下相应的调整
```html
<!DOCTYPE html>
<html lang="en" ng-app="app">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<script src="angular.js"></script>
</head>
<body>
	<div>
		<angular></angular>
		<div class="angular"></div>
		<div angular></div>
		<!--记住下面的注释要打空格-->
		<!-- directive:angular -->
		<div></div>
	</div>
</body>
<script type="text/javascript">
angular.module('app', []).directive('angular',function(){
	return {
		 restrict: 'EACM', // E = Element, A = Attribute, C = Class, M = Comment
		 template: '<div>hello,angular</div>',
		// templateUrl: '', 这里是html的模板的路径，如果需要的文本比较长的话，可以把模板单独提出来放在一个文件中
		 replace: true,
		// transclude: true,
		// compile: function(tElement, tAttrs, function transclude(function(scope, cloneLinkingFn){ return function linking(scope, elm, attrs){}})),
		link: function($scope, iElm, iAttrs, controller) {
			
		}
	};
});
</script>
</html>
```
![](/img/angular/02/02.png)
angular中，在restrict中最常用的是E和A这两个属性，其中C和M很少用，特别是C会产生混乱。
2、replace属性为true时，会替换directive指向的元素;为false时将directive的内容作为子元素插入到directive指向的元素。默认为false，
下面看看replace为false时，最后生成的文档结构
![](/img/angular/02/03.png)
在replace为false时，注释是没有被生成渲染出来的，
当replace为true时，最后生成文档的样式
![](/img/angular/02/04.png)
3、transclude表示变换
```html
	<angular>
		<div>如果我们想把这段文字和div也保存并显示出来的话，我们用replace是无法实现的，这就要要用到了transclude了</div>
	</angular>
```
下面我们来看代码
```html
<!DOCTYPE html>
<html lang="en" ng-app="app">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<script src="angular.js"></script>
</head>
<body>
	<div>
		<angular>
			<div>如果我们想把这段文字和div也保存并显示出来的话，我们用replace是无法实现的，这就要要用到了transclude了</div>
		</angular>
	</div>
</body>
<script type="text/javascript">
angular.module('app', []).directive('angular',function(){
	return {
		 restrict: 'E', 
		 template: '<div>hello,angular<div ng-transclude></div></div>',
		 transclude: true,
		link: function($scope, iElm, iAttrs, controller) {
			
		}
	};
});
</script>
</html>
```
显示出来的结果
![](/img/angular/02/05.png)
我们从上面的代码中可以看到，在template中有个ng-transclude，这就是把angular元素里面的值变换到这儿，然后让在页面上显示出来，从而不会被替换掉
4、compile与link函数
![](/img/angular/02/06.png)
从上面这张图片中可以清楚的看出关系，一般不会自己自定义compile函数，因为那样会覆盖掉本身的compile函数，一般是写link函数
## 指令与控制器之间的交互
```html
<!DOCTYPE html>
<html lang="en" ng-app="app">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<script src="angular.js"></script>
</head>
<body>
	<div ng-controller="Ctrl">
		<angular>测试link函数</angular>
	</div>
</body>
<script type="text/javascript">
var app = angular.module('app', [])
app.controller('Ctrl', ['$scope', function($scope){
	$scope.text = function(){
		console.info("测试成功")
	}
}])
app.directive('angular',function(){
	return {
		 restrict: 'E', 
		 link:function(scope,element,attr){
		 	element.bind("mouseenter",function(){
		 		//scope.text() 
		 		scope.$apply("text()")
		 	})
		 }
	};
});
</script>
</html>
```
当鼠标移上去的时候，在控制台上打印出
![](/img/angular/02/07.png)
操作DOM元素最好在link函数上操作
如果有两个angular元素呢
```html
	<div ng-controller="Ctrl">
		<angular>测试link函数</angular>
	</div>
	<div ng-controller="Ctrl2">
		<angular>测试link2函数</angular>
	</div>
```
这样的话我们用刚开始上面的方法就不行了，就要用到指令了，下面我们来看一下代码
```html
<!DOCTYPE html>
<html lang="en" ng-app="app">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<script src="angular.js"></script>
</head>
<body>
	<div ng-controller="Ctrl">
		<angular textTwo="text()">测试link函数</angular>
	</div>
	<div ng-controller="Ctrl2">
		<angular textTwo="text2()">测试link2函数</angular>
	</div>
</body>
<script type="text/javascript">
var app = angular.module('app', [])
app.controller('Ctrl', ['$scope', function($scope){
	$scope.text = function(){
		console.info("测试成功")
	}
}])
app.controller('Ctrl2', ['$scope', function($scope){
	$scope.text2= function(){
		console.info("测试2成功")
	}
}])
app.directive('angular',function(){
	return {
		 restrict: 'E', 
		 link:function(scope,element,attrs){
		 	element.bind("mouseenter",function(){
		 		//scope.text() 
		 		//scope.$apply("text()")
		 		scope.$apply(attrs.texttwo)//注意一下，如果属性是用驼峰法写的，调用的时候要写成的小写，列如textTwo ，在调用的时候要写成texttwo
		 	})
		 }
	};
});
</script>
</html>
输出的结果

```
![](/img/angular/02/08.png)我们通过attrs去获取里面方法
指令之间的交互[见慕课网大漠穷秋](http://www.imooc.com/video/3083)
