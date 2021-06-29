一面：

（主要考查基础知识和编程基础）

1. http1和http2的区别（多路复用，头部压缩的原理）

多路复用，头部压缩，服务端push

多路复用原理： HTTP/2是基于二进制“帧”的协议，HTTP/1.1是基于“文本分割”解析的协议。

头部压缩原理：https://my.oschina.net/u/4226611/blog/4352779

2. 实现求和sum，支持sum(1), sum(1,2,3,4), sum(1)(2)(3),  console.log(sum(1)(2,3)(4)) = 10

https://github.com/Advanced-Frontend/Daily-Interview-Question/issues/134

7. chain = new Chain, chain.eat().sleep(5).eat().sleep(6).work()

```javascript
class Chain{
  task=Promise.resolve()
  eat() {
    this.task=this.task.then(_=>console.log('eat'))
    return this
  }
  work() {
    this.task=this.task.then(_=>console.log('work'))
    return this
  }
  sleep(t) {
    this.task=this.task.then(_=>new Promise(r=>{
      console.log('sleep', t)
        setTimeout(r, t)
      }))
      return this
  }
}
```

8. xss和csrf

9. html meta

10. 浏览器缓存的原理

11. 什么是跨域，跨域的解决方式 （jsonp，服务端设置access-control-allow-origin：跨域资源共享，反向代理，postMessage）

\12. 原型链

13.手势库实现介绍

14.vue 生命周期？ 在哪个生命周期里调用请求？

15.computed 和 watch 的区别和运用的场景

16.vue-router 有哪些模式

17.vue-router 的实现原理

18.axios baidu.com get { query: 'test' }

19.编写一下 _axios(method, url, data).then()

\20. CSS 实现一个梯形

21.BFC如何形成？ 有什么作用？

22.JS 的防抖和节流的概念？ 

23.防抖： 

节流： 

24.实现一个template 方法 template(str, data)  

'my name is {{name}}, age is {{age }}' 

{ name: 'tom', age: 16 }

my name is tom, age is 16





二面：（主要考查框架原理和业务场景提升性能的方法）

\1. vue实现数据绑定的原理

\2. vue data属性类型的数据响应（{},[]）

\3. vue key对性能的影响

\4. virtual dom的作用

\5. computed的缓存以及根据data属性响应的原理 (发布订阅模式)

\6. wap页面如何适配不同分辨率 （rem相关）

\7. 如何实现图片懒加载，除了通过getBoundingClientRect，百度图库如何懒加载

\8. 虚拟列表、无限列表的原理

\9. 优化页面的指标：如何定义首屏渲染时间，观察占用内存

\10. vue 3的变化

 

 

三面：

\1. 判断数组的方式

\2. instanceof

\3. dns查询的过程（迭代/递归）

\4. cookie在一级域名和二级域名的读取问题

\5. 服务端是怎么设置浏览器cookie

\6. domContentLoaded和window.onload的区别

\7. 回到顶部的动画js实现

\8. jsonp的原理和实现一个jsonp方法

\9. 缓存问题

\10. 小数精度问题

\11. 数组A，数字N，A中找到a,b使a+b=N

 

 

四面

\1. 讲项目，虚拟列表的实现方法

\2. wepack plugin的作用

\3. 性能优化的方案

\4. 字符串，得出最长的没有重复字符的子串长度

\5. 跨站脚本注入和跨站请求伪造

\6. computed是怎么随着data响应

\7. 个人规划和发展方向

8. 百度搜索通用组件应该怎么设计







一面：

\1. 怎么将一个异步方法promise化，以及实现promise.all()方法

\2. vue单页多页的区别，vue路由实现原理

\3. vue数据驱动视图原理？更新视图的过程是否是同步的操作？

\4. nodejs相关的应用（答：开发命令行工具、web服务，ssr，数据库操作等）

\5. vue项目开发环境如何配置？wepack-dev-server 热更新功能实现原理

\6. express、koa、redis等技术相关应用

\7. [1,2,3].map(parseInt) 执行结果

二面：

\1. css 单行和多行截断

\2. 给一个由域名组成的字符串进行按子域名分组的反转，比如 news.toutiao.com 反转成 com.toutiao.news 需要 in place 做，

3.其他技术问题都是穿插在我的业务项目里面的，有点针对实际情景给解决方案

 

三面：

\1. js实现依赖注入

\2. 接口攻击的方式和防御措施

\3. https握手过程

\4. 设计模式

\5. redux和 mobx的区别

\6. js多线程如何共享大的数据







笔试：

1、换行字符串格式化

2、屏幕占满和未占满的情况下，使footer固定在底部，尽量多种方法。

3、日期转化为2小时前，1分钟前等

4、多个bind连接后输出的值

5、原码，补码，反码

6、事件委托

7、输入一个日期 返回几秒前 几天前或者几月前；

8、153812.7 转化153,812.7；

9、用两种方法 一种是正则；

10、还有关于 bind的一道题；

11.实现一个 Promise.all

12.手写代码：给定一个数组，形如 [1, 1, 2 , 3, 3, 3, 3, 4, 6, 6]，给定一个数 n，例如 3，找出给定的数 n 在数组内出现的次数，要求时间复杂度小于 O(n)

 

一轮

1.dom react原理 

2.css布局 

3.js原型链继承

4.fetch取消

5.eventloop

6.instanceof

7.promise封装setstate

8.redux基本组成和设计单向数据流

9.https协议的过程

10.https获取加密密钥的过程

11.http的方法有哪几种

12.类式继承的方案

13.prototype继承的实现

14.数字千分位处理，正则和非正则都要实现

15.借用构造继承，几种组合继承方式

16.看编程代码说出运行结果：

Process.nextTick，setImmediate 和promise.then 的优先级

Process.nextTick，pronise, setImmediate的优先级

17.实现一个bind函数

18.千位加逗号

19.三个继承方式的优缺点

20.odejs的事件循环

21.bfc

22.css实现正方形div水平垂直居中

23.koa1的原理,继承

24.最后是一个写代码 处理有依赖的异步任务 加重试

25.自己实现bind 函数 

26.什么是闭包，

27..最长子序列

28..二叉树中序遍历5http握手原理

29.react 新版本的特性

30.多空格字符串格式化为数组

31.bind函数运行结果

32.点击table的td显示td内容

33.数字千分位处理

34.固定日期与当前时间格式化处理

35.上中下三栏布局

37.实现一个子类实例可以继承父类的所有方法

38.实现sum(1)(2)(3).valueOf()，实现这么一个sum函数，返回6

39.实现taskSum(1000,()=>{console.log(1)}).task(1200,()=>{console.log(2)}).task(1300,()=>{console.log(3)})，这里等待1s，打印1，之后等待1.2s，打印2，之后打印1.3s，打印3

31.Jsonp跨域

32.js原型继承 & 原型链

33.promise

34.二叉树搜寻算法，

35..算法：前端做并发请求控制

\36. 宏任务微任务

\37. libUA

38.. express ctx 中间键代码实现

39.. vue 发布订阅和虚拟dom代码实现

\40. 请实现如下的函数，可以批量请求数据，所有的 URL 地址在 urls 参数中，同时可以通过 max 参数控制请求的并发度，当所有请求结束之后，需要执行 callback 回调函数。发请求的函数可以直接使用 fetch 即可

41.二叉树遍历

42.并发请求最大值是 10，怎么处理队列

43.css 画出一个三角形

44.node 网关

45.csrf/xss 攻击原理

46.react diff 原理

47.事件循环

48.react diff算法，key的作用，setData的机制，事件合成

49.vue的v-model原理

50.实现一个方法，参数是一个generator函数，执行结果是执行完所有generator中的yield

51.获取页面所有img并且下载

52.两个同源tab之间的交互，数据同步

53.怎么将一个异步方法promise化，以及实现promise.all()方法

\54. vue单页多页的区别，vue路由实现原理

\55. vue数据驱动视图原理？更新视图的过程是否是同步的操作？

\56. nodejs相关的应用（答：开发命令行工具、web服务，ssr，数据库操作等）

\57. vue项目开发环境如何配置？wepack-dev-server 热更新功能实现原理

\58. express、koa、redis等技术相关应用

59.. [1,2,3].map(parseInt) 执行结果

60.实现一个 Promise.all

61.手写代码：给定一个数组，形如 [1, 1, 2 , 3, 3, 3, 3, 4, 6, 6]，给定一个数 n，例如 3，找出给定的数 n 在数组内出现的次数，要求时间复杂度小于 O(n)

62.Bind 方法手写实现

63.手写代码二叉树深度为n的遍历，遍历有哪几种方式

64.promise.then 的调用

65.promise.all()的实现原理

66.div的点击事件回调不执行的原因，具体的一种原因怎么定位问题

67.hybrid 实现bridge的方法

68.最有挑战的项目

69.小程序框架的实现原理

70.Bind 方法手写实现

71.手写代码二叉树深度为n的遍历，遍历有哪几种方式

72.promise.then 的调用

73.promise.all()的实现原理

74.div的点击事件回调不执行的原因，具体的一种原因怎么定位问题

75.hybrid 实现bridge的方法

76.最有挑战的项目

77.小程序框架的实现原理

78.vue-router路由监听的原理

79.webpack打包的原理，webpack有没有针对打包过程做一些优化提升打包速度

80.请实现如下的函数，可以批量请求数据，所有的 URL 地址在 urls 参数中，同时可以通过 max 参数，控制请求的并发度，实现max个请求执行完之后再执行下max个请求，当所有请求结束之后，需要执行 callback 回调函数。发请求的函数可以直接 使用 fetch 即可

81.vue双向绑定的原理

82.写一个eventBus

83.元素水平垂直居中

84.vuex mobox

85.小程序架构优化 日志系统

86.写一个eventBus

87.元素水平垂直居中

88.vuex mobox

89.小程序架构优化 日志系统

90.根据自己简历和做过的项目，问一系列相关问题：

l 闭包的输出值，考查闭包（看试题给结果）

l 浏览器缓存的方法有哪些，它们的优先级是怎样的 ？

l 状态码 304 是什么意思 ？

l 都说要减少 https 的请求，https 为什么慢 ？

l http2 与 http1 有什么区别

l click DOM 节点的 inner 与 outer 的执行机制，考查事件冒泡与事件捕获 （看试题给结果）

l for 循环中的 var 、let 与 const 区别，for( const i = 0;  i< 3; i++ ){ console.log(i); } 会输出什么结果 ？（看试题给结果）

l 有没有系统学习过 es6 或者看过 es6 的书 

l js 单线程、宏任务与微任务的执行顺序 （看试题给结果）

l 考查箭头函数的 this 与 普通函数的区别，this 的指向 （看试题给结果）

l vue 中 computed 与 watch 的内在是如何实现的 ？

l 接下来前端要深入的方向 ？

91.CSS 栅格布局

\92. CSS 伪类和伪元素

93.根据条件获取递归树中过的某一节点

94.JavaScript this 的指向；箭头函数的 this 指向

95.Promise / setTimeout 的执行顺序；实际考察知识点：对「事件队列 / 宏任务 / 微任务」的了解

 

二轮:

1.主要是围绕你的项目经历和技术，有一定的深度，主要还是要对项目全面熟悉；还有一个就是函数柯理化的编码实现

\2. 函数柯里化、Web安全、react性能优化、react算法原理	

3.上来直接让写一个autocomplete 组件，可能是想考察业务思考点；

4.后续的问题主要会接着业务场景问 扣实际场景 不问知识理论；

5.http网络协议 ；

6.tcp为什么是可靠的；

7.js设计模式；

8.solid原则；

9.柯里化；

\10. css 单行和多行截断

\11. 给一个由域名组成的字符串进行按子域名分组的反转，比如 news.toutiao.com 反转成 com.toutiao.news 需要 in place 做

12..其他技术问题都是穿插在我的业务项目里面的，有点针对实际情景给解决方案

13.实现一个 outsideclick 的 Hoc，触发时调用 子组件的 outsideclick 方法

14.手写一个 redux middleware

15.实现一个 outsideclick 的 Hoc，触发时调用 子组件的 outsideclick 方法

16.最近在做项目（痛点，难点，怎么解决）

17.ssr（ssr csr混合怎么处理）

18.小程序架构（带来的优缺点）

19.状态管理，异步编程（各个优缺点）

20.聊了过往的项目经历，询问具体的技术方案和细节实现

\21. 分割字符串；实际考察知识点：对「正则表达式」的了解

22.富文本编辑器的实现；

23.文件上传的实现；

24.网络安全：CSRF & XSS 是什么及防范措施

25.同源策略；跨域的实现方式

26.带超时，带防重名的 JSONP 的实现

 

 

三轮：

1.自己做得最有成就的项目

2.自己主动承担并是核心的项目

3.项目深度:比如现场实现vue的数据代理等

4.技术广度:什么是微前端等

5.职业发展

6..js实现依赖注入

\7. 接口攻击的方式和防御措施

\8. https握手过程

\9. 设计模式

\10. redux和 mobx的区别

\11. js多线程如何共享大的数据

12.问了redis数据结构和实现

13.问hashmap

14.浅拷贝深拷贝实现

15.小程序架构优化，

\16. 二叉树 ，diff算法，

\17. 页面渲染原理， 

18.图像算法 事件循环

19.长列表渲染， 前端安全

20.聊了过往的项目经历，询问具体的技术方案和细节实现

21.在现团队中担任的角色；觉得自己印象最深刻 / 最有亮点的项目经历

 

算法部分：

1. ['a','b'],['A','B'],['1','0']，输出['aA1','aA0','aB1','aB0','bA1','bA0','bB1','bB0']，算法的排列组合问题

```javascript
function permutate(arr) {
    // 第一次的结果就是二维数组的第0项
    let res = arr[0].slice();

    for (let i = 1; i < arr.length; i++) {
        const pre = res.slice();
        res = [];
        pre.forEach(item => {
            arr[i].forEach(curr => {
                res.push(item + curr)
            })
        });
    }
    console.log(res)
    return res;
}
```

2. 写一个方法输出 ABCDEFG 的值

3. 从排好序的两个链表中，找到相同的节点，并输出链表

 