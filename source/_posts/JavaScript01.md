---
title: JavaScript--对象(01)
categories:
  -JavaScript
---
1、“一切都是对象”,在js中"一切都是对象"，并不是所有都是对象，值类型就不是对象

下面我们通过typeof函数输出所有的类型

```javascript
console.info(typeof(x))    //undefined

  console.info(typeof(true))   //boolean

  console.info(typeof("hyData")) //string

  console.info(typeof(100))   //number

  console.info(typeof(function(){}))  //function

  console.info(typeof([1,2,3,5,6]))   //object

  console.info(typeof({"name":"hy","age":4}))  //object
 
  console.info(typeof(null))     //object

  console.info(typeof(new Number(10)))   //object
```

其中string number boolean undefined 是值类型，其余都是对象，都是引用类型 ，

[​值类型和引用类型的区别]: http://www.cnblogs.com/lxq1990/archive/2012/11/04/2754226.html



值类型与引用类型的区别，我们以连锁店和连锁店钥匙来理解

（1）值类型：变量的交换等于在一个新的地方安装总店的规范开了一个连锁店，各自经验互不影响

demo

```javascript
var str1 = "tang quan kun";
var str2 = str1;
str1="tqk"
console.info(str2) //tang quan kun
```

把一个值类型str1的值传给str2时，实际上是个str2分配了一个地址和内存，所以改变str1的值时，str2不受影响

（2）引用类型：变量的交换等同于一个店在配了一把钥匙给老板娘，老板跟老板娘共同管理这家店，相互之间会有影响

demo

```javascript
var obj1 ={
  "name":"tang quan kun",
  "age":24
} 
var obj2 = obj1
console.info(obj2.name)  //tang quan kun
obj1.name = "tqk"
console.info(obj2.name)   //tqk
```

从上面可以看出，只要是改变了obj1后，obj2也会跟着改变，那是因为在obj2 = obj1时，没有给obj2开辟一个空间，而是把obj2指向了obj1

如果要判读一个值类型为什么类型用typeof判读，如果判读一个引用类型为什么类型用instanceof进行判断

```javascript
  var fun = function(){} ;
  console.info(fun instanceof Function )  //true
  console.info(fun instanceof Object )    //true
```

2、对象就是若干属性的集合，js不像java或者c++那样要new一个class出来，不像那么严格，js的对象可以任意的扩展 ，下面一个demo

```javascript
  var obj = {
  	  age:4,
  	  name:function(){
  	  	console.info("hyData")
  	  },
  	  other:{
  	  	"name":"xxx",
  	  	"year":2017
  	  }
  }
```

其中obj是一个自定义对象，里面的name、age、other是属性，other又是一个 对象，里面有name、year属性。下面以函数为例子

```javascript
  var fn = function(){
  	console.info("come in")
  };
  fn.name = "hyData";
  fn.age = function(){
  	console.info(4)
  };
  fn.other ={
  	"name":"xxx",
  	"year":2017
  };
```

上面的fn函数就被作为对象赋值了name、age、other属性。我们调用的时候可以以fn.other 这样调用，这样做的用处很多，例如jQuery中的get请求，$.get(...)