### 找出字符串中的最长回文串

思路：动态规划

```javascript
function longestPalindrome( s ) {
  if (!s) return;
  let n = s.length;
  let l = 0, r = 0;
  // 创建二维数组
  let arr = new Array(n);
  for (let i = 0; i < n; i++) {
      arr[i] = new Array(n);
  }
  for (let i = n-2; i >= 0; i--) {
      arr[i][i] = true;
      for (let j = i + 1; j < n; j++) {
          arr[i][j] = s.charAt(i) == s.charAt(j) && arr[i+1][j-1];
          if (arr[i][j] && r - l < j - i) {
              l = i;
              r = j;
          }
      }
  }
  return s.substring(l, r+1);
}
```

### 大数相加

```javascript
function add(a, b) {
  // 实现该函数
  let aList = a.split('').reverse()
  let bList = b.split('').reverse()
  let flag = 0 // 是否进位
  let max = Math.max(aList.length, bList.length)
  let result = []

  for (let i = 0; i < max; i++) {
    let temp = (+aList[i] || 0) + (+bList[i] || 0) + flag;
    flag = 0;
    if (temp > 10) {
      temp -= 10
      flag = 1
    }
    result.push(temp)
  }
  if (flag > 0) {
    result.push(1)
  }
  return result.reverse().join('')
}
```

### 实现一个方法，将传入对象的下划线命名方式全部换为驼峰式(考虑递归的场景)，比如：

```javascript
// before
const obj = {
  first_name: 'chen'
}

// after
const obj = {
  firstName: 'chen'
}
```

- 实现 Instance of
- 实现一个Lazyman
- 实现bind
- 实现debounce, throttle
- 实现深克隆
- 实现快速排序， 归并排序

方法：

### es6的模块管理 与 commonjs 的对比

### es6 Decorator

### es6+ 新特性

###  非递归实现树的后序遍历。

### Base64 的原理？编码后比编码前是大了还是小了。

所谓Base64，就是说选出64个字符----小写字母a-z、大写字母A-Z、数字0-9、符号"+"、"/"（再加上作为垫字的"="，实际上是65个字符）----作为一个基本字符集。然后，其他所有符号都转换成这个字符集中的字符。

第一步，将每三个字节作为一组，一共是24个二进制位。

第二步，将这24个二进制位分为四组，每个组有6个二进制位。

第三步，在每组前面加两个00，扩展成32个二进制位，即四个字节。

第四步，根据下表，得到扩展后的每个字节的对应符号，这就是Base64的编码值。

### http 302 301 307之间的区别

- 301 Moved Permanently
- 302 Found
- 303 See Other
- 307 Temporary Redirect

302 状态码表示目标资源临时移动到了另一个 URI 上。由于重定向是临时发生的，所以客户端在之后的请求中还应该使用原本的 URI。

服务器会在响应 Header 的 Location 字段中放上这个不同的 URI。浏览器可以使用 Location 中的 URI 进行自动重定向。

注意：由于**历史原因**，用户代理可能会在重定向后的请求中把 POST 方法改为 GET 方法。如果不想这样，应该使用 307（Temporary Redirect） 状态码。

307 的定义实际上和 302 是一致的，唯一的区别在于，307 状态码不允许浏览器将原本为 POST 的请求重定向到 GET 请求上。

### 301和302对于seo来说哪个更好 (301)

- 跨域是什么、如何解决
- jsonp有什么缺点
- 图片base64和外链的应用场景，各有什么优缺点(base64减少请求数，但是会增加额外的体积)
- http缓存机制
- https的握手过程是怎样的
- set/map的区别
- hook的局限性
- setState和hook的区别
- decorator的作用，编译后是怎样的(@decorator -> decorator(target)...)
- symbol是什么，一般用来做什么
- csrf 是什么 如何防范
- sql注入是什么，如何防范
- react 调用setState之后发生了什么
- nodejs事件循环机制
- pm2的原理，有哪些模式(cluster fork)
- docker和k8s有了解多少(k8s听过没用过)
- 移动端端一个元素拖动，如何实现和优化（节流、改变位置）

-`for in`/`for of` 看代码输出

- 几道看代码说输出（忘了具体题目了）
- 描述链表的反转怎样实现，复杂度多少

编程

- 实现`instanceOf`
- 实现一个对象被`for of`遍历
- 实现链表的添加、删除。复杂度多少

一面考的都是一些基础知识，需要一定牢固的基础知识准备才行

二面 时间 一面之后的下午

- 给了两段效果上都可以实现child 继承 parent，细节上的差别

  ```
  function child(){}
  function parent(){}
  child.prototype.__proto__ = parent.prototype
  child.prototype = new parent()
  复制代码
  ```

- 一些代码看输出的题目。考点有函数`this`指向的问题

- 如何监听html外链资源加载失败(面试官又追问了`onerror` 和`addEventListener`的error都能吗。面试官说onerror不行，具体我没试过...)

- `Mutation Observer`、`Intersection Observer`使用场景（Intersection听过没用过）

- `127.0.0.1`和`0.0.0.0`差别（一个只能通过`localhost` ，一个可以通过本机ip或者localhost都行）

- 利用promise js sleep函数实现

- jsx转换后是怎样的

- dva有了解吗

- `umi.js`有用过吗

- `req.pipe(res)`

- stream 如何处理数据消费和数据生产的速率不一致问题

- writeable stream `drain`事件是做什么的（这是和一个控制读写速率有关的事件）

二面考得比较细，问了很多看代码问输出的问题，也问了一些比较细节的问题，有些细节的地方确实实际也没接触过。

https://www.nowcoder.com/discuss/401007?type=2&order=0&pos=17&page=1&channel=-2&source_id=discuss_tag

https://www.nowcoder.com/discuss/463919