---
title: angualar--指令(独立的scope)
categories:
  -angular1.x.x
---
下面来看一下demo
```html
<!DOCTYPE html>
<html lang="en" ng-app="app">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<script src="angular.js"></script>
</head>
<body>
	<angular></angular>
	<angular></angular>
	<angular></angular>
</body>
<script type="text/javascript">
var app =  angular.module('app', [])
app.directive('angular',function(){
	return {
		 restrict: 'AE', 
		 template:'<div><input type="text" ng-model="text" />输出{{text}}</div>'
	};
});
</script>
</html>
```
看一看输出的结果
![](/img/angular/03/01.gif)
从上面的结果中可以看出，当一个input输入时，其它的也都跟着变了，因为scope不是独立的作用域，要做到独立scope的话很简单,只需要加一个scope就行了
```javascript
var app =  angular.module('app', [])
app.directive('angular',function(){
	return {
		 restrict: 'AE', 
		 scope:{}, //独立scope
		 template:'<div><input type="text" ng-model="text" />输出{{text}}</div>'
	};
});
```
scope的绑定策略
![](/img/angular/03/02.png)
1、首先我们来看第一个@,先看看demo
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
		<angular flavor={{text}}></angular>
	</div>
</body>
<script type="text/javascript">
var app =  angular.module('app', [])
app.controller('Ctrl', ['$scope', function($scope){
	$scope.text = "angular"
}])
app.directive('angular',function(){
	return {
		 restrict: 'AE', 
		 scope:{
		 	flavor:'@'
		 },
		 template:'<div>{{flavor}}</div>'
	};
});
</script>
</html>
```
输出的结果![](/img/angular/03/03.png)，可以从上面的例子中看出把控制器Ctrl中的值传递到模块angular中，在使用@的时候要注意传递的时候不是一对象进行传递的，而是以字符串传递
2、下面来看看下一个 "=" 这中绑定，这种绑定是双向进行绑定的。下面我们来看一下代码
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
		第一个
		<br>
		<input type="text" ng-model="text">
		<br>
		第二个
		<br>
		<angular flavor="text"></angular>
	</div>
</body>
<script type="text/javascript">
var app =  angular.module('app', [])
app.controller('Ctrl', ['$scope', function($scope){
	$scope.text = "angular"
}])
app.directive('angular',function(){
	return {
		 restrict: 'AE', 
		 scope:{
		 	flavor:'='
		 },
		 template:'<input type="text" ng-model="flavor" />'
	};
});
</script>
</html>
```
下面看看输出的结果
![](/img/angular/03/04.gif)
从结果中我们可以看到，
当改变控制器里面的值后，指令里面也跟着改变了，当改变了指令里面的值后，控制器里面的值也改变了，这就是"="的作用。
3、最后我们来看看"&"这个符号，首先还是先来看一下例子
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
		<angular getName = "get(name)"></angular>
		<angular getName = "get(name)"></angular>
		<angular getName = "get(name)"></angular>
	</div>
</body>
<script type="text/javascript">
var app =  angular.module('app', [])
app.controller('Ctrl', ['$scope', function($scope){
	$scope.get = function(name){
		console.log("scope才用&演示结果"+ name)
	}
}])
app.directive('angular',function(){
	return {
		 restrict: 'AE', 
		 scope:{
		 	getname:'&'
		 },
		 template:'<input type="text" ng-model="username" />'+
		 		  '<button ng-click="getname({name:username})">调用</button>'
	};
});
</script>
</html>
```
下面看看输出的结果
![](/img/angular/03/05.gif)
在这儿要注意一点儿的时候，当函数的接受参数的时候，在上面的demo中get函数需要接收一个name的参数，所以我们在getname中传递一个对象{name:username},username就是我们在输入框中输入的值，name就是传递的参数。还有就是在getName中采用的是驼峰命名的，下面在绑定的时候记得要全部小写
这就是@、=、&的不同用法，@主要是传递的是字符串，=主要用作双向绑定，&传递来自父scope方便调用。