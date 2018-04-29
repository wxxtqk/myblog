---
title: TypeScript--参数新特性(02)
categories:
  -TypeScript
---
Welcome to [TypeScript](http://www.typescriptlang.org/)! If you want know more , please Check [more](http://www.typescriptlang.org/) In this article , I shall describe some of grammar about TypeScript,刚开始准备写英文的，但是觉得麻烦，并且英文也不是太好，还是写中文吧，废话就不多说了，直接堆码，如果有写的不对或者不好的地方，希望大家多多指教
## 第一节 参数类型
### 参数类型
在参数名称后面使用冒号来指定参数的类型
1、指定字符串型
```javascript
	let myName: string = "tang quang kun"
	    myName = 12 //error
```
如果后面在对myName赋其它类型的值则会有一个错误的提示

2、类型推断机制
```javascript
	let myName = "tang quang kun"
	    myName = 12 // error 
```
虽然没有对myName定义一个类型，但是刚开始给它赋值的类型为string，所有后面myName的类型九尾string，后面在给它赋值number就会报错
如果想声明一个类型，既可以是string，又可以是number类型或者其它类型，我们就用any来声明
```javascript
	let myName:any = "tang quang kun"
	    myName = 12 // true 
```
3、其它类型声明
```javascript
let age: number = 24;   
let gender: boolean = true; 

function test(): void{
    //void 声明不需要返回值值，如果有return返回值就会报错
}
```
4、函数的声明
test函数返回一个字符串声明
```javascript
function test(): string{
    return "tang quan kun"
}
```
想要函数test返回相应类型，把string改为相应的类型即可

5、函数参数的声明
```javascript
function test(name:string): string{
    return name
}
test("tang quan kun") //true
test(24) //error
}
```
可以对函数传入的参数类型声明
6、自定义类型
在ts中可以通过class或者接口来声明自己自定义的类型
```javascript
class Person{
    name: string;
    age:number
    
}
let tangqk: Person = new Person();
tangqk.name = "tang quan kun";
tangqk.age = 24;
```
## 第二节 默认参数
### 默认参数
在参数声明后面用等号来指定参数的默认值
```javascript
	let name:string = "tang quan kun";
```
如何给方法的变量指定默认值
```javascript
function test(a: string, b: string, c: string = "zzz") {
    console.log(a)
    console.log(b)
    console.log(c)
}
test("xxx","yyy")
```
运行的结果如下
![](/img/01/string5.png)
注意：只能够把指定默认值得参数方式最后面，如果不放在最后面会报错误，以下的写法是错误的
```javascript
function test(a: string, c: string = "zzz", b: string) {
    console.log(a)
    console.log(b)
    console.log(c)
}
test("xxx","yyy")
```
## 第三节 可选参数
### 可选参数
在方法的后面用问号来标明此参数为可选参数
```javascript
function test(a: string, b?: string, c: string = "zzz") {
    console.log(a)
    console.log(b)
    console.log(c)
}
test("yyy")
```
输出的结果如下
![](/img/01/string6.png)
因为b元素为可选元素，所以用test("yyy")调用不会报错，c有默认值