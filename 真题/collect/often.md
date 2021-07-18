### 原型和原型链

![image-20201011091756637](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201011091756637.png)

### 闭包

什么是闭包： 函数嵌套函数时，内层函数引用了外层函数作用域下的变量，并且内层函数在全局环境下可访问，就形成了闭包。

应用场景：闭包这个概念为 JavaScript 中访问函数内变量提供了途径和便利。比如我们可以利用闭包实现“模块化”，可以使用闭包实现单例模式。

### 说说你了解的http请求头

常见的上下文头部：

User-Agent：描述发起HTTP请求的客户端，服务器可以依据它来返回最合适此浏览器显示的页面 ；

Referer：浏览器对来自某一页面的请求自动添加的头部

代理相关：

X-Forwarded-For用来记录代理服务器的IP；

X-Real-IP用户传递用户IP；

Max-Forwards用来限制Proxy代理服务器最大转发次数，仅对TRACE/OPTIONS方法有效；

Via指明经过对代理服务器名称及版本

范围请求：

Range

### 双向绑定原理

vue数据双向绑定是通过数据劫持结合发布者-订阅者模式的方式来实现的。
![image-20201021203554572](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201021203554572.png)

from： http://element-ui.cn/article/show-135434.aspx

### 说说做的的比较好的项目

我之前做的营销美的通，是一个Hybrid app，采用的是token的鉴权方式，登录之前是客户端的，登录之后是H5应用。整个应用分为首页跟模块页，我做的就是相应的H5模块。

### 如果写一本前端的书，你怎么列目录

