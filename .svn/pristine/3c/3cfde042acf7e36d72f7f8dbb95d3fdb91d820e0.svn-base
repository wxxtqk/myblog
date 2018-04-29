---
title: TypeScript--表达式与循环(04)
categories:
  -TypeScript
---
主要是箭头表达式和for of循环
## 第一节 箭头表达式
### 箭头表达式
用来声明匿名函数，消除传统匿名函数的this指针问题，(这儿有点儿争议)，下面我们来看一个简单demo
![](/img/04/01.png)
从上面的ts和js对比结果可以看出，ts定义一个匿名函数，然后返回num1和num2相加，这里没有用到return，如果要是多行的要写大括号和return的
![](/img/04/02.png)
匿名函数有几种方法类型，第一种是没有任何参数的
```javascript
var sum = () => {
    console.info("tang quan kun ")
}
转化为js
var sum = function () {
    console.info("tang quan kun ");
};
```
第二种只有一个参数
```javascript
var sum = num => {
    console.info(num)
}
转化为的js
var sum = function (num) {
    console.info(num);
};

```
下面来看一个简单的例子
```javascript
var arr = [1, 2, 3, 4, 5, 6]
console.info(arr.filter(val=>val%2==0)) //[2,4,6]
//转化为的js
var arr = [1, 2, 3, 4, 5, 6];
console.info(arr.filter(function (val) { return val % 2 == 0; }));
```
这个filter参数就是一个匿名函数，接受一个参数,对接收的val进行判断，如果是偶数就返回true，并把这个值留在数组里面，奇数都被过滤掉了这样不仅是缩短了代码量，并且最大的一个好处就是解决了this指针的问题，在传统的js代码里，this老爱容易搞晕
下面来举一个传统的js关键字出现的一些问题
```javascript
function getName(name: string) {
    this.name = name
    setInterval(function () {
       console.info("this name is:"+this.name) 
    },1000)
}
var start = new getName("tang quan kun")
```
![](/img/04/03.png)
可以从结果中看到，打印出来出来的this.name什么都没有，但是按照我们逻辑打印出来的this.name应该是tang quan kun，我们实例一个getName对象，并传一个 tang quan kun ，所以this.name应该是有值，下面我们换一种方法来
```javascript
function getName(name: string) {
    this.name = name
    setInterval(()=> {
       console.info("this name is:"+this.name) 
    },1000)
}
var start = new getName("tang quan kun")
```
![](/img/04/04.png)
现在打印出来的就有值了，仔细对比一下上面两段代码，我们只是把setInterval里面的匿名函数进行了一个小的修改，把传统的匿名函数改成了箭头的函数，这样做的结果就符合我想要的结果
## 第一节 新的循环
### 新的循环
在做新的循环（ for of）的时候，我们先来看看传统的js的用到的循环，forEach 、for in 进行比较
```javascript
	var arr = [1, 2, 3, 4]
	arr.name = "tang quan kun"  //这种写法在ts会报错，但是编译成js是可以运行的
	arr.forEach(val=>console.info(val)) //[1,2,3,4]
```
从上面打印出来的结果可以知道，对数组做的name是没有打印出来的，那是因为forEach会循环数组里面的元素，但是会把里面属性跟忽略掉，所以打印出来就是[1,2,3,4],还有就是forEach函数运行起来后，是不能够跳出来，不像其他函数一样满足某个条件可以break
```javascript
var arr = [1, 2, 3, 4]
arr.name = "tang quan kun"
for (var n in arr) {
    console.info(n) [0,1,2,3,name]
}
```
为什么打印出来是[0,1,2,3,name],因为for in便利的数组里面的属性的名字，而不是值，因为不管是数组或者对象都是以一个键值对形式存在，for in循环是循环的键值对（key）这儿就不多介绍，如果要用for in获取值可以通过以下方法
```javascript
var arr = [1, 2, 3, 4]
arr.name = "tang quan kun"
for (var n in arr) {
    console.info(arr[n]) //[1,2,3,4,tang quan kun]
}
```
下面我们来一个新的循环for of ，它跟forEach有点儿一样，唯一不同的就是可以打断，可以break
```javascript
var arr = [1, 2, 3, 4]
arr.name = "tang quan kun"
for (var n of arr) {
    console.info(n) //[1,2,3,4]
}
```
这打印出来跟forEach一样的结果，下面来看看break
```javascript
var arr = [1, 2, 3, 4]
arr.name = "tang quan kun"
for (var n of arr) {
    if (n >2) {
        break
    }
    console.info(n) //[1,2]
}
```
上面当大于2的时候就跳出了，for of也可以对字符串进行循环
```javascript
var str = "tang quan kun"
for (var n of str){
    console.info(n)
} 
```
打印出的结果
![](/img/04/05.png)
