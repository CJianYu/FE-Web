### 实现一个函数 compose([fn1,fn2,fn3..]) 转成 fn3(fn2(fn1()))

```javascript
function compose() {
    var args = arguments;
    var start = args.length - 1;
    return function() {
        var i = start;
        var result = args[start].apply(this, arguments);
        while (i--) result = args[i].call(this, result);
        return result;
    };
};
```

### 了解鉴权么

https://juejin.im/post/6844903927100473357

### css实现三角形

```css
.caret {
  width: 0;
  height: 0;
  border-top: 50px solid black;
  border-right: 50px solid transparent;
  border-bottom: 50px solid transparent;
  border-left: 50px solid transparent;
}
```

### 页面下雪效果

https://codepen.io/alphardex/pen/dyPorwJ

### async await的并行

如果想并行执行，我们应该先生成所有需要使用的Promise实例：

```javascript
;(async ()=>{
    let namePromise = getName()
    let idPromise = getId()              // 先生成所有 promise 实例
    let name = await namePromise
    let id = await idPromise
    alert(`name:${name}, id:${id}`)
})()
```

或者使用Promise.all

```javascript
;(async ()=>{
    var result = await Promise.all([getName(), getId()])
    alert(`name:${result[0]}, id:${result[2]}`)
})()
```

### requestAnimationFrame

https://javascript.ruanyifeng.com/htmlapi/requestanimationframe.html

### vue-loader实现原理

### target和currentTarget的区别

**currentTarget始终是监听事件者，而target是事件的真正发出者**。

### 求sum(1)(2)(3)...(n)()

```javascript
function add (...args) {
    //求和
    return args.reduce((a, b) => a + b)
}

function currying (fn) {
    let args = []
    return function temp (...newArgs) {
        if (newArgs.length) {
            args = [
                ...args,
                ...newArgs
            ]
            return temp
        } else {
            let val = fn.apply(this, args)
            args = [] //保证再次调用时清空
            return val
        }
    }
}

let addCurry = currying(add)
// 注意调用方式的变化
console.log(addCurry(1)(2)(3)(4, 5)())  //15
console.log(addCurry(1)(2)(3, 4, 5)())  //15
console.log(addCurry(1)(2, 3, 4, 5)())  //15


// add(1); 	// 1
// add(1)(2);  	// 3
// add(1)(2)(3)；  // 6
// add(1)(2, 3);   // 6
// add(1, 2)(3);   // 6
// add(1, 2, 3);   // 6
function add(...args) {
  let sum = 0;
  const innerAdd = (...args) => {
    args.forEach(i => (sum += i));
    return innerAdd;
  };
  innerAdd.toString = () => sum;
  return innerAdd(...args);
}

// ES6写法  
function add () {  
    let args = [...arguments];  
    let fn = function(){  
        return add.apply(null, args.concat([...arguments]))  
    }  
     fn.toString = () => args.reduce((a, b) => a + b)  
    return fn;  
} 



// 第一步，先实现加和运算
            var add = function (a, b) {
                return a + b;
            }

            var currying = function (fn, defineVal = 0) {
                return function (...args) { // 第一次调用的是这个函数
                    // 每次执行前先进行和的初始化
                    var sum = defineVal;

                    function func(...argts) { // 第二次之后调用的是这个函数
                        if (args.length === 0) {
                            return func.toString();
                        } else {
                            argts.unshift(sum);
                            sum = argts.reduce(fn);
                            return func;
                        }
                    }
                    func.toString = () => sum;
                    return func(...args);
                }
            }

            var add = currying(add);
            console.info(add(1)); // => 1
            console.info(add(1)(2)); // => 3
            console.info(add(1)(2)(3)); // => 6
            console.info(add(1, 2)(3)); // => 6
            console.info(add(1)(2, 3)); // => 6
            console.info(add(1, 2, 3)); // => 6
            console.info(add(1, 2, 3)(4)); // => 10
```

## 我的

### 热更新（HMR）原理

### 多路复用具体怎么实现的

### 讲一下https的加密（握手）过程

1. 客户端使用https的url访问web服务器,要求与服务器建立ssl连接
2. web服务器收到客户端请求后, 会将网站的证书(包含公钥)传送一份给客户端
3. 客户端收到网站证书后会检查证书的颁发机构以及过期时间, 如果没有问题就随机产生一个秘钥
4. 客户端利用公钥将会话秘钥加密, 并传送给服务端, 服务端利用自己的私钥解密出会话秘钥
5. 之后服务器与客户端使用秘钥加密传输

### 怎么把jsx的组件渲染到template

### 为啥要刷新操作呢

看https://drive.google.com/drive/u/0/folders/1g5xqW6L5fXZzjBkkwZ0QjWCyq5pm9DKA

### 说一下你做过的项目中你觉得你做的好的地方

### Vue-router是如何实现的，history模式用到的API

### 手写深拷贝

