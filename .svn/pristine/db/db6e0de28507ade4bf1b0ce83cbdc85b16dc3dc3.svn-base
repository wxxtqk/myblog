---
title: TypeScript--面向对象特性(06)-泛型
categories:
  -TypeScript
---
所谓的泛型就是参数化的类型，一般用来限制集合的内容
## 泛型
### 泛型
下面我们来看一个实际的例子
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
var arr: Array<Person> = []
arr[0] = new Person("tang quan kun") //不报错
arr[1] = new Man("tang quan kun", 24)  //不报错
arr[2] = 2 //报错
```
为什么arr[0] = new Person("tang quan kun") arr[1] = new Man("tang quan kun", 24) 都是true都是可以的呢，而arr[2] = 2是会报错，那是因为var arr: Array<Person> = [],其中<Person>就是这个数组的泛型，它指定了数组arr只能够存放Person,因为Man 和 Person都是Person类，而2不是Person类，所以会报错。