---
title: TypeScript--字符串新特性(01)
categories:
  -TypeScript
---
Welcome to [TypeScript](http://www.typescriptlang.org/)! If you want know more , please Check [more](http://www.typescriptlang.org/) In this article , I shall describe some of grammar about TypeScript,刚开始准备写英文的，但是觉得麻烦，并且英文也不是太好，还是写中文吧，废话就不多说了，直接堆码，如果有写的不对或者不好的地方，希望大家多多指教

## 第一节 字符串新特性
### 多行字符串
传统js，如果你双引号想给一个字符串换行的话，必要用用 + 进行串起来，
``` javascript
	var content = "hello"
		      +"TypeScript"
```
然而在ts中，引入了一个新的多行字符串，用一个双撇号去声明一个字符串，就是键盘上tab键上面那个号
```typesctipt
	var content = `hello
	            Typescript`
```
我们可以通过TypeScript官网中的在线环境进行ts和js装换，[ts和js的转换](http://www.typescriptlang.org/play/index.html)
![](/img/01/string.png)
### 字符串模板
所谓的字符串模板就是在一个多行表达式中插入一个变量或者一个方法
``` javascript
	var content = "tang quang kun";
	var getName = function () {
    return "tang quan kun";
	}
	console.log(`hello ${content}`)
	console.log(`hello ${getName()}`)
```
![](/img/01/string2.png)
从上面的ts转换到js的可以看到，是如何转换的
注意：如果字符串模板不是在双撇号中，而是在双引号中会以普通字符串进行解析
![](/img/01/string3.png)
使用字符串模板的一个好处
```javascript
var content = "tang quang kun";
var getName = function () {
    return "tang quan kun";
}
var text = `<div>
        <h1>可以使用字符串模板直接添加值值</h1>
        <span>${content}</span> 
        <span>${getName()}</span> 
    </div>
`
```
无论是开发速度或者可读性都不js要好的多
### 自动拆分字符串
所谓自动拆分字符串，就是当你再用字符串模板去调用一个方法的时候，这个字符串模板表达式的值会自动赋给被调用方法中的参数
``` javascript
function test(template, name, gender) {
    console.log(template);
    console.log(name)
    console.log(gender)
}

var myName = "tang quan kun";
var getGender = function(){
    return "男";
}
test`my name is ${myName},my gender is ${getGender()}`
```
![](/img/01/string4.png)
从打印的结果可以看,其中第一个打印的是一个字符串的数组，第二打印的是tang quan kun 第三个打印的是 男，第一个参数template接收是传入的字符串，第二个为拆分的${myName}，第三个为拆分是${getGender}


