---
title: TypeScript--面向对象特性(05)-类
categories:
  -TypeScript
---
由于面向对象比较多，所以我这儿就分两个篇章来大致的讲一下面向对象特性，首先先讲讲类
## 类(class)
### 类(class) 类的定义
类是TypeScript的核心，使用TS开发时，大部分代码都是写在类里面的，这里我们会简单的介绍一下类的定义，构造函数，以及类的继承等等
下面我来看一下简单的一个类的定义
```javascript
//声明一个类
class Person {
    name: string;
    todo() {
        console.info("to do somethin")
    }
}
//实例化一个类
var p1 = new Person()
p1.name = "tang quan kun"
p1.todo()
```
首先我们通过class实例定义一个类，然后在通过关键字new实例化一个对象，实例化就可以调用里面方法，如果大家学过c++或者java的都知道，ts中的类也有访问控制符分别是public（所有类都可以访问）、private（只有本类可以访问）、protected（当前类和子类可以访问，后面继承会讲到），想必学过java的人都知道这几个，定义类的时候，默认就是public，跟上面的代码一样，下面来看看private
```javascript
//声明一个类
class Person {
    private name: string;
    protected age: number;
       todo() {
        console.info("to do somethin")
    }
}
//实例化一个类
var p1 = new Person()
p1.name = "tang quan kun" //如果name为private，这样直接访问会报错，只会在本类中可以访问，
p1.age = 24 //如果age为protected,这样直接访问也会出错，只有在本类或者之类可以访问
p1.todo()  //todo为public时，所有的都可以访问  
```
### 构造函数
  构造函数是类里面的一个特殊的方法，只有在类被实例化的时候会被调用，并且只调用一次，他就是constructor
```javascript
  //声明一个类
class Person {
    private name: string;
   //构造函数
    constructor(name: string) {
        this.name = name  
    };
       todo() {
        console.info(this.name)
    }
}
var p1 = new Person("tang quan kun")
p1.todo() // tang quan kun
```
这个类在被实例化的时候必要要传一个name进去，在实例化的时候就调用了constructor函数，所以后面打印出来就是 tang quan kun,在构造函数中的参数是必须要申明属性访问控制控制符的，上面的name的访问控制符为private
```javascript
//声明一个类
class Person {
   //构造函数
    constructor(name: string) {  //这种写法是错误的的，因为这样是没有声明name属性的，相当于类Person里面没有name属性
        this.name = name  
    };
       todo() {
        console.info(this.name)
    }
}
var p1 = new Person("tang quan kun")
p1.todo()

//声明一个类
class Person {
   //构造函数
    constructor(private name: string) {  //这种写法才是正确
        this.name = name  
    };
       todo() {
        console.info(this.name)
    }
}
var p1 = new Person("tang quan kun")
p1.todo()
```
### 类的继承
类的继承这儿设计到两个关键字那就是extends 和 super  extends 主要用来声明类的继承关系，super用来调用父类的构造方法或者函数
1、下面我们来看一下extends,extends用来声明一种继承关系，所谓继承关系就是是的关系，下面我们来看看一个例子
```javascript
class Person {
    constructor(private name: string) {
        this.name = name  
    };
       todo() {
        console.info(this.name)
    }
}

class Man extends Person{

}
var p1 = new Man("tang quan kun")
p1.todo() //tang quan kun
```
通过上面的列子可以看出，Man类通过extends继承了类Person,Man就继承了Person中所有的方法和属性。在继承的类Man中我们可以也可以增加新的方法和属性
![](/img/05/01.png)
从上面的例子可以看出Man可以自己进行扩展属性和方法
2、super的用法，super有两种用法，第一种是拿来调父类的构造函数，先看一个demo，
```javascript
class Person {
    constructor(protected name: string) {
        this.name = name  
        console.info("i an is class Person")
    };
       todo() {
        console.info(this.name)
    }
}
class Man extends Person{
    constructor(name: string, age: number) {
        super(name)  //运用super调用父类的构造函数
        this.age = age
        console.info("i an is class Man")
    }
    age: number;
    work() {
    }
}
var p1 = new Man("tang quan kun", 24)
```
打印出来的结果
![](/img/05/02.png)
在构造Man这个类的时候会通过super调用Person类的构造方法，这是super的一个用法，另外一个用法就是用个super调用父类的方法
```javascript
class Person {
    constructor(protected name: string) {
        this.name = name  
        console.info("i an is class Person")
    };
       todo() {
        console.info("在Person中执行的")
    }
}
class Man extends Person{
    constructor(name: string, age: number) {
        super(name)  //运用super调用父类的构造函数
        this.age = age
        console.info("i an is class Man")
    }
    age: number;
    work() {
        super.todo()  //运用super调用父类的方法
        this.todoafter()
    }
    private todoafter() {
        console.info("在Man执行的")
    }
}
var p1 = new Man("tang quan kun", 24)
p1.work()
```
打印出来的结果
![](/img/05/03.png)
我们可以从上面的结果中可以看出,super的两种方法，一种是调用父类的构造方法，一种是调用父类的方法或者属性