---
title: TypeScript--函数新特性(03)
categories:
  -TypeScript
---
Welcome to [TypeScript](http://www.typescriptlang.org/)! If you want know more , please Check [more](http://www.typescriptlang.org/) In this article , I shall describe some of grammar about TypeScript,刚开始准备写英文的，但是觉得麻烦，并且英文也不是太好，还是写中文吧，废话就不多说了，直接堆码，如果有写的不对或者不好的地方，希望大家多多指教
## 第一节 Rest and Spread 操作符
### Rest and Spread 操作符
主要是用来声明任意数量的方法参数
```javascript
function test(...args) {
    args.forEach(function (arg) {
        console.log(arg)
    })
}

test(1, 2, 3)

test(5,6,9,7,5)
```
其中 ... 就是Rest and Spread 操作符,从上面的test(1, 2, 3)，test(5,6,9,7,5) 可以看出可以传多个参数进去
![](/img/02/string.png)
扩展，上面还有一个返过来的做法，它是es6的一个语法，目前这个版本的ts还不支持，后面估计会支持的
![](/img/02/string1.png)
如果用test(...args1)这种方法ts代码会报错,但是生成的js办法没有问题，我们来看一下打印出来的结果
![](/img/02/string2.png)
因为test函数接收a,b,c三个参数，第一次调用test()传入的是1,2两个参数,所以打印出来的是1,2, undefined ,第二次调用的时候是传入了7,8,9,10，由于test只接收三个参数，所以打印出来只有7,8,9
## 第二节 generator函数
### generator函数
控制函数的执行过程，手工暂停和恢复代码执行，在es5里面，如果调用一个方法后，不能够用什么方法让这样方式执行了一般停住了，但是在后面的es6中，新增了一个关键字yield,可以实现该方法，yield就像给代码打了一个断点，代码执行到yield的时候停住了，在调用yield的时候执行下一步,由于目前的ts版本还不支持，我们用另外一个编辑器来看一下简单的例子
![](/img/02/string3.png)
首先我们通过
```javascript
	function* toDo(){}
```
声明一个generator函数，申明generator函数很简单，只要在function后加 * 就可以了，通过上面的方法我们可以看出当第一次执行函数的时候打印出来是start。我们从toDo函数中看到有一个关键字yield，因为是申明了generator函数，所以后面调用函数的时候不能够直接toDo(),要先申明一个变量 var fun1 = toDo() 然后在fun1.next() 第一次fun1.next()的时候，函数执行到了yield然后就停住了，就不会往下面执行了，在执行一次fun1.next()就会往下一步执行。
![](/img/02/string4.png)
下面来一个比较复杂点儿generator函数，
```javascript
function* getPrice(stock){
	while(true){
		yield Math.random()*100;
	}
}
var priceGenerator = getPrice("ts")
var limitPrice = 15;
var price = 100;
while(price>limitPrice){
	price = priceGenerator.next().value;
	console.log(`the generator return ${price}`)
}
```
![](/img/02/string5.jpg)
当价格price大于limitPrice就会取一次值，通过yield来控制函数执行
## 第三节 destructuring析构表达式
### destructuring析构表达式
通过表达式将对象或数组拆解成任意数量的变量
1、第一种情况
```javascript
function test() {
    return {
        name1: "tang quan kun",
        gender: "男"
    }
}
//es5的写法

var name1 = test().name1
var gender = test().gender


//ts的析构表达式
var {name1,gender} = test()
```
注意：在var {name1,gender} = test()中，解析的var {name1,gender}中的字段名要跟test()中返回的字段名要一样，否则会报错，如果不想跟一样可以用
var {name2:name1,gender} = test()给name1定义一个别名
```javascript
function test() {
    return {
        name1: "tang quan kun",
        gender: "男"
    }
}
//es5的写法

var name1 = test().name1
var gender = test().gender


//ts的析构表达式
var {name2:name1,gender} = test()
```
2、获取的是一个对象
```javascript
function test() {
    return {
        name1: "tang quan kun",
        age:{
            lastage: 23,
            thisage:24
        }
    }
}
var {name1,age:{lastage}} = test()
console.log(name1)   //tang quan kun
console.log(lastage) //23
```
3、从数组中去取值
```javascript
var arry = [1, 2, 3, 4]
var [number1, number2] = arry
console.log(number1) //1
console.log(number2) //2
```
如果想取3和4
```javscript
var arry = [1, 2, 3, 4]
var [ , ,number1, number2] = arry
console.log(number1) //3
console.log(number2) //4
```
如果想取1和4
```javascript
var arry = [1, 2, 3, 4]
var [number1, , , number2] = arry
console.log(number1) //1
console.log(number2) //4
```
析构表达式结合前面的Rest and Spread 操作符
```javascript
var arry = [1, 2, 3, 4]
function todo([number1, number2, ...other]) {
    console.log(number1)  //1
    console.log(number2)  //2
    console.log(other)   //[3,4]
}
todo(arry)
```
把number1赋值为1 number2赋值为2 other赋值为一个数组[3,4]