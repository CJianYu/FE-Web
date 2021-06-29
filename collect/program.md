### 实现深拷贝

```javascript
// isPlainObject 函数来自于  [JavaScript专题之类型判断(下) ](https://github.com/mqyqingfeng/Blog/issues/30)
var class2type = {};
var toString = class2type.toString;
var hasOwn = class2type.hasOwnProperty;

function isPlainObject(obj) {
    var proto, Ctor;
    if (!obj || toString.call(obj) !== "[object Object]") {
        return false;
    }
    proto = Object.getPrototypeOf(obj);
    if (!proto) {
        return true;
    }
    Ctor = hasOwn.call(proto, "constructor") && proto.constructor;
    return typeof Ctor === "function" && hasOwn.toString.call(Ctor) === hasOwn.toString.call(Object);
}


function extend() {
    // 默认不进行深拷贝
    var deep = false;
    var name, options, src, copy, clone, copyIsArray;
    var length = arguments.length;
    // 记录要复制的对象的下标
    var i = 1;
    // 第一个参数不传布尔值的情况下，target 默认是第一个参数
    var target = arguments[0] || {};
    // 如果第一个参数是布尔值，第二个参数是 target
    if (typeof target == 'boolean') {
        deep = target;
        target = arguments[i] || {};
        i++;
    }
    // 如果target不是对象，我们是无法进行复制的，所以设为 {}
    if (typeof target !== "object" && !isFunction(target)) {
        target = {};
    }

    // 循环遍历要复制的对象们
    for (; i < length; i++) {
        // 获取当前对象
        options = arguments[i];
        // 要求不能为空 避免 extend(a,,b) 这种情况
        if (options != null) {
            for (name in options) {
                // 目标属性值
                src = target[name];
                // 要复制的对象的属性值
                copy = options[name];

                // 解决循环引用
                if (target === copy) {
                    continue;
                }

                // 要递归的对象必须是 plainObject 或者数组
                if (deep && copy && (isPlainObject(copy) ||
                        (copyIsArray = Array.isArray(copy)))) {
                    // 要复制的对象属性值类型需要与目标属性值相同
                    if (copyIsArray) {
                        copyIsArray = false;
                        clone = src && Array.isArray(src) ? src : [];

                    } else {
                        clone = src && isPlainObject(src) ? src : {};
                    }

                    target[name] = extend(deep, clone, copy);

                } else if (copy !== undefined) {
                    target[name] = copy;
                }
            }
        }
    }

    return target;
};
```

### 继承

以前没有类型，所以大家模拟了很多继承的方法，但本质上都是两种的变体：

- 原型链继承

```
// 假设有一个需要继承的一个类型 Animal

function Cat() {}
Cat.prototype = new Animal
// 添加一个属性
Cat.prototype.name = 'cat'
```

- 构造继承

```
// 假设有一个需要继承的一个类型 Animal

function Cat(name){
  Animal.call(this)
  // 添加一个属性
  this.name = name || 'cat'
}
```

- 所以组合这两个东东：组合继承

```
// 假设有一个需要继承的一个类型 Animal

function Cat(name) {
  Animal.call(this)
  // 添加属性
  this.name = name || 'cat'
}
Cat.prototype = new Animal()
// 添加方法
Cat.prototype.say = function () {
  // TOOD
}
```

* 寄生组合继承：这种继承方式对组合继承进行了优化，组合继承缺点在于继承父类函数时调用了构造函数，我们只需要优化掉这点就行了。

```javascript
function Cat(name) {
  Animal.call(this)
  this.name = name || 'cat'
}
Cat.prototype = Object.create(Animal.prototype)
Cat.prototype.constructor = Cat
```

### 模拟实现call

```javascript
Function.prototype.myCall = function(context) {
  // 判断调用call的函数（也就是this）是否是函数
  if(typeof this === 'function') {
    throw new TypeError('Error')
  }
  context = context || window
  context.fn = this
  const args = [...argumments].slice(1)
  const result = context.fn(args)
  delete context.fn
  return result
}
```

实现说明：

* 当传入的函数为null的时候，this默认指向window
* 函数是可以有返回值的，这也是要有一个result的意义

### 模拟实现apply

```javascript
Function.prototype.myApply = function(context) {
  if(typeof this === 'function') {
    throw new TypeError('Error')
  }
  context = context || window
  context.fn = this
  let result
  if(arguments[1]) {
    result = context.fn(arguments[1])
  } else {
    result = context.fn()
  }
  return result
}
```

实现说明：

* 实现跟call的实现差不多，唯一的区别是传入的参数不一样

### 模拟实现bind

```javascript
Function.prototype.bind2 = function (context) {

    if (typeof this !== "function") {
      throw new Error("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var self = this;
    var args = Array.prototype.slice.call(arguments, 1);

    var fNOP = function () {};

    var fBound = function () {
        var bindArgs = Array.prototype.slice.call(arguments);
        return self.apply(this instanceof fNOP ? this : context, args.concat(bindArgs));
    }

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();
    return fBound;
}
```

### 模拟实现new

```javascript
function myNew() {
  let obj = {}
  // shift会改变原数组，所以arguments第一个元素会被去除，后面直接使用
  let Contructor = [].shift.call(arguments)
  // 继承
  obj.__proto__ = Contructor.prototype
  // 绑定this
  let result = Contructor.apply(obj, arguments)
  return typeof result === 'object'? result : obj
}
```

实现说明：

* 创建一个新对象
* 取出传入的第一个参数（构造函数）
* 将新对象的原型指向构造函数，使新对象可以访问构造函数原型中的属性
* 改变构造函数的this指向，使新对象可以访问构造函数的属性
* 确保返回的是对象

### 模拟实现instanceof

```javascript
function myInstanceof(left, right) {
  let prototype = right.prototype
  left = left.__proto__
  while(true) {
    if(left === null || left === underfined) {
      return false
    }
    if(left === prototype) {
      return true
    }
    left = left.__prototype__
  }
}
```

实现说明：

* 拿到对象（left）与类型（right）的原型
* 循环判断两者是否相等，直到left为null

### 防抖

```javascript
function debounce(fn, wait) {
  var timeout
  return function() {
    var context = this
    var args = arguments
    clearTimeout(timeout)
    if(!timeout) {
      timeout = setTimeout(function(){
        fn.apply(context, args)
      }, wait)
    }
  }
}

// 添加立即执行
function debounce(fn, wait， immediate) {
  var timeout
  return function() {
    var context = this;
    var args = arguments;
    if(timeout) clearTimeout(timeout)
    if(immediate){
      // ！timeout如果为true表示未执行过（timeout 是闭包变量，初始化时是 undefined ， setTimeout 返回的是定时器的 id ，一个 > 0 的数字，clearTimeout 不会改变 timeout 的值。若 timeout 经历过赋值，即执行过 setTimeout ，则 !timeout 为假）
      var callNow = !timeout
      timeout = setTimeout(function(){
      // 设置为null为了停止触发函数后callnow为true，从而能执行函数
        timeout = null 
      },wait)
      if(callNow) {
        fn.apply(context, args)
      }
    } else {
      timeout = setTimeout(function(){
        fn.apply(contxt, args)
      }, wait)
    }  
  }
}

// 添加取消与返回值
function debounce(func, wait, immediate) {

    var timeout, result;

    var debounced = function () {
        var context = this;
        var args = arguments;

        if (timeout) clearTimeout(timeout);
        if (immediate) {
            // 如果已经执行过，不再执行
            var callNow = !timeout;
            timeout = setTimeout(function(){
                timeout = null;
            }, wait)
            if (callNow) result = func.apply(context, args)
        }
        else {
            timeout = setTimeout(function(){
                func.apply(context, args)
            }, wait);
        }
        return result;
    };

    debounced.cancel = function() {
        clearTimeout(timeout);
        timeout = null;
    };

    return debounced;
}
```

### 节流

```javascript
// 使用定时器
function throttle(func, wait){
  var timeout
  return function(){
    var context = this
    var args = arguments
    if(!timout) {
      setTimeout(function(){
        timeout = null
        func.apply(context, args)
      }, wait)
    }
  }
}


// 完整版
function throttle(func, wait, options) {
    var timeout, context, args, result;
    var previous = 0;
    if (!options) options = {};

    var later = function() {
        previous = options.leading === false ? 0 : new Date().getTime();
        timeout = null;
        func.apply(context, args);
        if (!timeout) context = args = null;
    };

    var throttled = function() {
        var now = new Date().getTime();
        if (!previous && options.leading === false) previous = now;
        var remaining = wait - (now - previous);
        context = this;
        args = arguments;
        if (remaining <= 0 || remaining > wait) {
            if (timeout) {
                clearTimeout(timeout);
                timeout = null;
            }
            previous = now;
            func.apply(context, args);
            if (!timeout) context = args = null;
        } else if (!timeout && options.trailing !== false) {
            timeout = setTimeout(later, remaining);
        }
    };
    return throttled;
}
throttled.cancel = function() {
    clearTimeout(timeout);
    previous = 0;
    timeout = null;
}
```

### 数组去重

```javascript
// filter, array.concat()是为了复制一个新数组
function unique(array) {
  return array.concat().sort().filter((item, index, array) => {
    return !index || item !== array[index-1]
  })
}

// object键值对
function unique(array) {
  var obj = {}
  return array.concat().filter((item, index, array) => {
    return obj.hasOwnproperty(typeof item + stringigy(item))? false : (obj[typeof item + stringigy(item)] = true)
  })
}

// es6
var unique = (a) => [...new Set(a)]

// es6 map
function unique(array) {
  const seen = new Map()
  array.concat().filter(item => {
    return !seen.has(item) && seen.set(item, 1)
  })
}
```

### 类型判断

```javascript
var classType = {}
"Boolean Number String Function Array Date RegExp Object Error".split(' ').map((item, index) => {
  classType['[object ' + item + ']'] = item.toLowerCase()
})
function judgeType(item) {
  // 在 IE6 中，null 和 undefined 会被 Object.prototype.toString 识别成 [object Object],这里做个区分
  if (obj == null) {
    return obj + "";
  }
  return typeof(item) === 'object' || typeof(item) === 'function' ? classType[Object.prototype.toString.call(item)] || 'object' : typeof item
}
```

### 数组扁平化

```javascript
// 递归方法
function flatten(arr){
  if(!Array.isArray(arr)) {
    return
  }
  var result = []
  for(var i; i < arr.length; i++) {
    if(Array.isArray(arr[i])) {
      result.concat(flatten(arr[i]))
    } else {
      result.push(arr[i])
    }
  }
  return result
}

// 可以用reduce简化代码
function flatten(arr) {
  return arr.reduce((accumulate, currentItem) => {
    return accumulate.concat(Array.isArray(currentItem)? flatten(currentItem) : currentItem)
  })
}

// es6
function flatten(arr) {
   while(arr.some(item => { Array.isArray(item) })) {
     arr = [].concat(...arr)
   }
   return arr
}
```







