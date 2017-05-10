---
title: this 的学习心得
date: 2017-05-10 22:30:54
tags: udacity javascript this 
---

## Javascript 中 THIS 的学习心得体会

***关于this***

关键词`this`使得我们可以仅创建一个函数对象，就可以将其作为方法用在一些其它的对象上。了解`this`关键字是一个非常重要的关键。

``` javascript
    const fn = function(a, b) {
        console.log(this) 
    }

    const obj = { method: fn }

    fn() // this === window , 

    obj.method() // this === obj

```

* 当函数被调用时，如果它的左边有一个点符号，那就意味着它是作为某个对象的属性被查找的， 函数被调用时它所查找的对象就是`this`绑定的内容。简言之，this总是指向调用它的对象，如果作为函数直接调用，`this`便指向`window`。

```javascript
    function example (a) {
        var fn = function() {
            console.log(this)
        }
       console.log(this)     
    }

    expample() // this === window

    example.fn() // this === example

```

setTimeout中的`this`，下面这个例子打印出的`this`为神马还是`window`

```javascript

    const obj = function() {
        const fn = function() {
            console.log(this)
        }
    }

    setTimeout(obj.fn, 1000) //this === window
```

打印出的`this`仍然是`window`原因在这里

* setTimeout中的是以回调函数来执行传入的函数对象， 所以它的执行方式就好像这样（模拟，非真实setTimeout的运行方式）
```javascript
    var timer = function(cb, ms) {
        delay(ms)
        cb() //回调函数在这里执行, 回调函数前没有点符号，这时的this当然就只能指向window
    }
```

* 如果想要在`setTimeout`的回调中使`this`指向对象要怎么做呢
```javascript
   const obj = function() {
       const name = 'obj'
       const fn = function() {
            console.log(this.name)
       }
   }

   setTimeout(function(){
       obj.fn() // 输出 "obj"
   }, 1000) 
```
