---
title: TypeScript--面向对象特性(08)-模块
categories:
  -TypeScript
---
模块可以帮助开发者将代码分割为可重用的单元。开发者可以自己决定将模块中的那些资源（类 方法 变量）暴露出去，暴露出去的资源就可以供其它模块儿调用。模块在ts就是文件的意思，一个模块就是一个文件，在模块中有两个关键字那就是export（导出） 和import（导入），这根es6中有点像，这两个关键字用来控制模块暴露和引入，一个模块可以暴露出资源也可以引用资源,下面来看一个demo
moduleA.ts
```javascript
export var age:number = 24;
var name:string = "tang quan kun "


export function fun1(){
	console.info("a")
} 

function fun2(){

}

export class A{

}
class B{

}
```
moduleB.ts
```javascript
import { age,fun1,A} from './moduleA';
console.info(age)

fun1()

var b = new A()


export function fun3(){
	
}
```
在moduleB.ts文件中通过import关键字引入了模块moduleA.ts中暴露出来的方法、属性、类，然后在moduleB.ts中就可以用这些方法，并且在moduleB.ts中也可以通过export暴露出一个函数fun3

