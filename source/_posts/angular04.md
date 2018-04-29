---
title: angualar--service与Provider
categories:
  -angular1.x.x
---
在前面我们提到过，最好不去复用controller里面的代码，我们要把里面相同的代码抽出来然后放到service里面
## 首先我们看一下$http服务
我们先看一下http 的例子
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
		<ul>
			<li ng-repeat="list in lists">
				<label>名字</label>：{{list.name}}
				<label>年龄</label>:{{list.age}}
			</li>
		</ul>
	</div>
</body>
<script type="text/javascript">
var app =  angular.module('app', [])
app.controller('Ctrl', ['$scope','$http',function($scope,$http){
	$http({
		method:'GET',
		url:'data.json',
	}).success(function(data,status,headers,config){
		$scope.lists = data
	}).error(function(data,status,headers,config){
		
	})
}])

</script>
</html>
```
其中data.json为
```json
[{
	"name":"张三丰",
	"age":24
},{
	"name":"张无忌",
	"age":25
},{
	"name":"赵敏",
	"age":19
}]
```
输出的结果
![](/img/angular/04/01.png)
其中http请求有很多配置，可以到文档里面去看
## 使用factory封装自己的http服务
下面我们先来看一一个列子
```html
<!DOCTYPE html>
<html lang="en" ng-app="app">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
	<script src="angular.js"></script>
	<script src="text.js"></script>
</head>
<body>
	<div ng-controller="Ctrl">
		<ul>
			<li ng-repeat="list in lists">
				<label>名字</label>：{{list.name}}
				<label>年龄</label>:{{list.age}}
			</li>
		</ul>
	</div>
</body>
</html>
```
text.js文件
```javascript
var app =  angular.module('app', [])
//封装自己的service
app.factory('CtrlService', ['$http','$q',function($http,$q){
	return {
		getData:function(){
			return $http({
				method:'GET',
				url:'data.json',
			})  //return 一个promise
		}
	}
}])
app.controller('Ctrl', ['$scope','CtrlService',function($scope,CtrlService){
	CtrlService.getData().success(function(responseData,status,headers,config){
							$scope.lists = responseData

						}).error(function(responseData,status,headers,config){})
}])

```
输出的结果
![](/img/angular/04/01.png)我们把http请求封装在factory中，封装成自己的一个service，这样controller就处理业务逻辑,不同的controller都可以调用这个service
service的特性：
	1、service都是单例的
	2、service由$injector负责实例化
	3、service在整个应用的生命周期中存在，可以用来共享数据
	4、在需要使用的地方利用依赖注入机制注入service
	5、自定义的service需要写在内置的service后面
	6、内置service的命名以$符号开头，自定义service应该避免
其中service、provider、factory本质都是provider,只是里面的写法和参数不同
## angular中的 constant、value、service、factory、provider的常用几种方法
