---
title: TypeScript--面向对象特性(07)-接口
categories:
  -TypeScript
---
用来建立某种代码约定，使得其它开发者在调用某个方法或者创建新的类时必须遵循接口所定义的代码约定，在JavaScript中没有接口这个概念，在typescript中提供两个关键字来支持接口。一个是interface，用来声明一个接口，另外一个是implements，用来申明某一个类实现了某一个接口，下面我们讲讲第一个interface
```javascript
interface Person{
    name: string,
    age:number
}
class Man{
    constructor(public people: Person) {
        
    }
}
var p1 = new Man({
    name: "tang quan kun",
    age:24
})
//这种方法ts会报错
var p2 = new Man({
    name: "tang quan kun",
    age: 24,
    work:"do work"
})
```
由上面可以看出，实例化p1是正确的是，而实例化p2就是错误的，那是因为当实例化对象的时候传入的参数必须满足接口Person里面的所有参数类型及属性，如果传入的参数不满足定义的接口的类型就会报错
下面我们讲讲implements
```javascript
interface Person{
    todo()
}
//这样写ts不会报错
class Man implements Person{
    todo() {
        console.info("i an is man")
    }
}
//这样会报错
class Woman implements Person{

}
```
为什么在定义类Man时不会报错，而在定义Woman时会报错，因为当一个类实现一个接口的时候，必须要实现接口里面方法，如果不能实现接口里面方法就会报错