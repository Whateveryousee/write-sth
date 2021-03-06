# 前端面试JS方法的各种实现代码

在面试前端开发中，原生JavaScript能力的高低是占比很大的一个体现部分，不少考官会有要求现场写一些JS方法，以下整理了一些前端面试的各种方法，希望能帮到你。（以下代码不适用生产中，各位拿走需自行校对正确与否）

* 1.bind（改正）

```
Function.prototype.bind2 = function () {
    var self = this,args = arguments;
    return function () {
        self.apply(args);
    }

}
```

* 2.promise

```
class Promise {
     result: any;
     callbacks = [];
     failbacks = [];
     constructor(fn) {
         fn(this.resolve.bind(this), this.reject.bind(this));
     }
     resolve(res) {
         if (this.callbacks.length > 0) this.callbacks.shift()(res, this.resolve.bind(this), this.reject.bind(this));
     }
     reject(res) {
         this.callbacks = [];
         if (this.failbacks.length > 0) this.failbacks.shift()(res, this.resolve.bind(this), this.reject.bind(this));
     }
     catch(fn) {
         this.failbacks.push(fn);
     }
     then(fn) {
         this.callbacks.push(fn);
         return this;
     }

 }
```

* 3.new的实现

```
function create() {
    // 创建一个空的对象
    let obj = new Object()
    // 获得构造函数
    let Con = [].shift.call(arguments)
    // 链接到原型
    obj.__proto__ = Con.prototype
    // 绑定 this，执行构造函数
    let result = Con.apply(obj, arguments)
    // 确保 new 出来的是个对象
    return typeof result === 'object' ? result : obj
}
```

* 4.函数防抖

```
// func是用户传入需要防抖的函数
// wait是等待时间
const debounce = (func, wait = 50) => {
  // 缓存一个定时器id
  let timer = 0
  // 这里返回的函数是每次用户实际调用的防抖函数
  // 如果已经设定过定时器了就清空上一次的定时器
  // 开始一个新的定时器，延迟执行用户传入的方法
  return function(...args) {
    if (timer) clearTimeout(timer)
    timer = setTimeout(() => {
      func.apply(this, args)
    }, wait)
  }
}
```

* 5.函数节流（改正）

```
function throttle(method,delay){
    var timer=null;
    return function(){
        var context=this, args=arguments;
        if(timer) return;
        timer=setTimeout(function(){
            method.apply(context,args);
            timer = null;
        },delay);
    }
}
```

* 6.深拷贝

```
function deepClone(obj) {
    let result = typeof  obj.splice === "function" ? [] : {};
    if (obj && typeof obj === 'object') {
        for (let key in obj) {
            if (obj[key] && typeof obj[key] === 'object') {
                result[key] = deepClone(obj[key]);//如果对象的属性值为object的时候，递归调用deepClone,即在吧某个值对象复制一份到新的对象的对应值中。
            } else {
                result[key] = obj[key];//如果对象的属性值不为object的时候，直接复制参数对象的每一个键值到新的对象对应的键值对中。
            }

        }
        return result;
    }
    return obj;
}
```

* 7.extends实现

```
//子类  extends  父类
Function.prototype.extends = function(func, options){
    for(var key in func.prototype){
        this.prototype[key] = func.prototype[key];
    }
    for(var name in options){
        this.prototype[name] = options[name];
    }
}
```

* 8.单例模式

```
function A(name){
    // 如果已存在对应的实例
   if(typeof A.instance === 'object'){
       return A.instance
   }
   //否则正常创建实例
   this.name = name
   
   // 缓存
   A.instance =this
   return this
}
```

* 9.发布订阅模式

```
// 事件类
    class EventEmitter {
        constructor () {
            this.events = { } // 事件队列，保存着每一种事件的处理程序
        }
 
        on (type, callback) { // type 要绑定的事件名字， callback 处理程序
            if (this.events[type]) {// 如果事件队列中有这个事件
                // 将此次绑定的处理程序放入进去
                this.events[type].push(callback.bind(this))
                return false
            }
            // 如果没有这个事件，新建
            this.events[type] = [callback.bind(this)]
        }
 
        emit (type, ...args) {
            // 触发事件的时候如果没有事件，报错
            if (!this.events[type]) {
                console.error('type event is not found')
            }else {
                // 挨个执行队列中的处理程序
                this.events[type].forEach(callback => {
                    callback(...args)
                });
            }
        }
    }
 
 
    let bus = new EventEmitter()
 
    bus.on('play', (num1, num2) => {
        alert(123)
    })
 
    bus.on('play', (num1, num2) => {
        alert(456)
        alert(num1 + num2)
    })
 
    bus.emit('play', 1, 2)
```

[来自](http://caibaojian.com/js-interview-methods.html)
