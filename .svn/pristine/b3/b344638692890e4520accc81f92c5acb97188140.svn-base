---
title: JavaScript--函数和对象的关系(01)
categories:
  -JavaScript
---
函数和对象的关系，我们可以通过instanceof来判断

```javascript
var fun = function(){}
console.info(fun instanceof Object) //true

```

函数是一种对象，但是又不像数组是对象的一种，数组就行是对象中的一个子集，但是函数跟对象的关系比较复杂，就像鸡生蛋蛋生鸡一样

```javascript
var fun = function(){
  this.name="tang quan kun";
  this.age = 24
}
var fun1 = new fun()
```
我们从上面可以看出对象可以通过函数创造的，其实所有的对象都是函数创造的,但是有些人说不是这样的

```javascript
var obj = {
  name:"tang quan kun ",
  age:24
}
var arr = [1,5,6]
```

上面的对象就不是通过函数来创造的,上面的只是平时一些快捷的方法进行创建，它的真实面貌其实是下面这样来的

```javascript
var obj = new Object()
	obj.name = "tang quan kun";
    obj.age = 24;
var arr = new Array()
    arr[0] = 1
    arr[1] = 5
    arr[2] = 6
```

然而Object和Array又是函数类型

```javascript
console.info(typeof(Object))  //function
console.info(typeof(Array))   //function
```

所以说对象都是通过函数来创建，但是函数又是对象，这是为什么呢？这个原因我们通过prototype原型来解释