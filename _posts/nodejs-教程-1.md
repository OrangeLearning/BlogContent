---
title: nodejs 教程(1)
date: 2017-09-30 01:05:42
tags:  [nodejs]
category: [web技术]
---
# Nodejs教程

## 回调函数

### 使用回掉函数的理由
为什么要有回调函数，看一个例子：
```js
var fs = require("fs");
var data = fs.readFileSync('input.txt');
console.log(data.toString());
console.log("程序执行结束!");
```
这个程序在一般`C++`中没什么问题，但是在网络应用中就不方便了，所以为了效率起见，我们一般使用下面的非阻塞代码：

```js
var fs = require("fs");
fs.readFile('input.txt', function (err, data) {
    if (err) return console.error(err);
    console.log(data.toString());
});
console.log("程序执行结束!");
```

### callback hell
但是，一定要注意不要频繁使用回调函数，因为这个东西会使得代码逻辑一片混乱，嵌套过深，可读性和可维护性都非常糟糕。
比如下面这个：
```js
req.models.vote.create(record, funtion(err, result){
    // 回调函数B
    if (err) {
        // blablabla...
        // 对B执行结果的异常处理
    }
    req.models.xxx.find(..,function(err,result){
        // 回调函数C
        if (err){
            // 对C执行结果的异常处理
        }
        req.models.xxx.find(..,function(err,result){
            // 回调函数D
            if (err) {..}
        })
    })
})
```

这个就是`callback hell`，但是为了代码的可维护性，于是使用中间件。
而很多的模块就是使用中间件进行操作的。这也是模块化的一个重要操作。
```js
// 【router.js】
var test = require('./test.js')
app.post('/',test.a,test.b) ;

// 【test.js】
module.exports.a = function(req,res,next){ //必须有这三个变量
    req.models.vote.create(record, funtion(err, result){
    // 回调函数B
    if (err) {
        // blablabla...
        // 对B执行结果的异常处理
        return res ; //返回http请求，不进入下一单元
    }
    // 一些非异步的操作..
    next() ; 
    // 如果后面还有中间件，则next表示传给下个中间件
    }
} ;
module.exports.b = function(req,res,next){
    req.models.vote.create(record, funtion(err, result){
    // 回调函数B
    if (err) {
        // blablabla...
        // 对B执行结果的异常处理
        return res ; 
    }
    // 一些非异步的操作..
    return res ;
    // 如果是最后一个中间件，则不能有next函数，不然会导致无响应
    }
} ;
```

### 关于next函数
[next函数](http://blog.csdn.net/xyr05288/article/details/51890738)

`next()`函数主要是用来确保所有注册的中间件被一个接一个的执行，那么我们就应该在所有的中间件中调用next函数，但有一个特例，如果我们定义的中间件终结了本次请求，那就不应该再调用next函数，否则就可能会出问题，我们来看段代码

(中间件这里先说一下，就是app.use()注册的中间件)
```js
// next()的内部机制
function next(err) {
    ... //此处源码省略
    // find next matching layer
    var layer;
    var match;
    var route;

    while (match !== true && idx < stack.length) {
      layer = stack[idx++];
      match = matchLayer(layer, path);
      route = layer.route;

      if (typeof match !== 'boolean') {
        // hold on to layerError
        layerError = layerError || match;
      }

      if (match !== true) {
        continue;
      }
      ... //此处源码省略
    }
    ... //此处源码省略
    // this should be done for the layer
    if (err) {
        layer.handle_error(err, req, res, next);
    } else {
        layer.handle_request(req, res, next);
    }
  }
```

## NodeJs 事件循环
> 下面再说