一、js构造函数
---

```
function MathHandle(x,y){
    this.x = x
    this.y = y
}

MathHandle.prototype.add = function(){
    return this.x +  this.y
}

var m = new MathHandle(1,2)
console.log(m.add())
```

二、class基本语法
---

```
class MathHandle{
    constructor(x,y){
        this.x = x
        this.y = y
    }
    add(){
        return this.x + this.y
    }
}

const m = new MathHandle(1,2)
console.log(m.add())
```

三、语法糖
---

在上述两段代码中分别加入如下代码，运行。

```
console.log(typeof MathHandle) // 'function'
console.log(MathHandle.prototype.constructor === MathHandle) //true
console.log(m.__proto__ === MathHandle.prototype) //true
```

运行结果一致。我认为，class是构造函数的语法糖。

四、 继承
---

* 1、构造函数形式的继承

```
//动物
function Animal(){
    this.eat = function (){
        console.log('Animal eat')
    }
}

//狗
function Dog() {
    this.bark = function (){
        console.log('Dog bark')
    }
}

Dog.prototype = new Animal()

var hashiqi = new Dog()
hashiqi.bark()
hashiqi.eat()
```

* 2、class继承

```
class Animal {
    constructor(name){
        this.name = name
    }
    eat(){
        alert(this.name + ' eat')
    }
}

class Dog extends Animal {
    constructor(name){
        super(name) //super就是被继承的对象的constructer
    }
    say(){
        alert(this.name + ' say')
    }
}

const dog = new Dog('哈士奇')
dog.say()
dog.eat()
```

四、总结
---
1、class在语法上更贴近面向对象的写法。<br>
2、class实现继承更加易读易理解。
