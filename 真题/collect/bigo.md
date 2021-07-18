![image-20201007135522463](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201007135522463.png)

```javascript
// vue双向绑定原理
Vue 双向绑定，使用数据劫持和发布订阅模式实现的

深层次，其实就是问你vue数据绑定的原理：
1、使用Object.defineProperty进行数据劫持，把data对象，computed等里的所有属性进行数据劫持。数据劫持的意思可以看：JavaScript中的Object.defineProperty()函数
2、使用观察者模式，完成发布订阅。
1）、模板里使用data对象属性的dom对象都订阅。
2）、当data对象里的属性的值发生变化时，就会发布，发布时，就改变了dom里的内容。

// v-for key有什么用
diff算法中通过tag和key来判断，是否是sameNode；减少渲染次数，提升渲染性能
```



![image-20201007140133524](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201007140133524.png)

```css
// flex
// float
// 百分比
```

### ![image-20201007140157446](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201007140157446.png)

```javascript
var isPalindrome = function (x) {
  if (x < 0 || (x % 10 == 0 && x !== 0)) return false
  let reverseNum = 0
  while (x > reverseNum) {
    reverseNum = reverseNum * 10 + x % 10
    x = Math.floor(x / 10)
  }
  return x === reverseNum || Math.floor(reverseNum / 10) === x
}
```

![image-20201007135956766](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201007135956766.png)

```javascript
// 归纳法，对于个位出现的1：(n / 10) * 1 + (n % 10) >= 1 ? 1 : 0;
// 对于十位出现的1：(n / 100) * 10 + if (k > 19) 10 else if (k < 10) 0 else k - 10 + 1;
// 对于百位出现的1：(n / 1000) * 100 + if (k > 199) 10 else if (k < 100) 0 else k - 100 + 1;
// 最终归纳出: (n / (i * 10)) * i + if (k > 2 * i - 1) i else if (k < i) 0 else k - i + 1, 其中k = n % (i * 10);

var countDigitOne = function(n) {
    let count = 0;

    for (let i = 1; i <= n; i *= 10) {
        let divide = i * 10;
        let p = Math.floor(n / divide), k = n % divide, rest = 0;

        count += p * i;
        rest = (k > (2 * i - 1)) ? i : ((k < i) ? 0 : k - i + 1);
        count += rest;
    }
    return count;
};

链接：https://leetcode-cn.com/problems/number-of-digit-one/solution/gui-na-fa-jian-dan-si-lu-by-wanyuxuan/
```



![image-20201007140009053](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201007140009053.png)

```javascript
https://www.nowcoder.com/questionTerminal/f3efcb3984054fd1aef8942985800539

```



![image-20201007140023375](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201007140023375.png)

```javascript
// good bigo
```

![image-20201007140036041](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201007140036041.png)

```javascript
// [{a: 4}]
// [{a: 4}]
// [{a: 4}]
// [{a: 4}]
```

![image-20201007140047119](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201007140047119.png)

```javascript
// promise1
// then1-1
// promise2
// then2-1
// then1-2
// then2-2
```

![image-20201007140511320](/Users/jeffrey/Library/Application Support/typora-user-images/image-20201007140511320.png)

```javascript
function compareVersion(version1, version2) {
  let arr1 = version1.split('.');
  let arr2 = version2.split('.');
  let len = Math.max(arr1.length, arr2.length)
  for(let i = 0; i < len;i++) {
    let value1 = 0;
    let value2 = 0;
    if(i < arr1.length) {
      value1 = parseInt(arr1[i])
    }
    if(i < arr2.length) {
      value2 = parseInt(arr2[i])
    }
    if(value1 < value2) {
      return -1
    } else if(value1 > value2) {
      return 1
    }
  }
  return -1
}
```



### 九球问题

任取2组比较，若重量相等，则目标小球在另一组；   

若重量不等，则任意替换一组再进行比较，可以知晓目标小球所在组，以及目标小球重量比一般小球是重还是轻。   

对目标小球所在小组任取2个，若重量相等，则目标小球为另一个；若重量不等则可以根据之前获取的目标小球重量特征（比一般重或轻），找出目标小球。 

 共称3次。

### kmp算法

```javascript
const strStr = function(haystack, needle) {
    if (needle === "") return 0;
    if (haystack === "") return -1;
    let inc = [];
    // 计算偏移量
    for (let i = 0; i < needle.length; i++) {
        for (let j = 0; j <= i; j++) {
            if (needle[j] !== needle[i - j]) {
                inc[i] = j + 1;
                break;
            }
            if (j === i && needle[j] === needle[i - j]) {
                inc[i] = j + 1;
            }
        }
    }
    let i = 0;
    let l = needle.length
    while (i < haystack.length) {
        for (let j = 0; j < l; j++) {
            if (needle[j] !== haystack[i + j]) {
                i += inc[j];
                break;
            }
            if (j === l - 1 && needle[j] === haystack[i + j]) {
                return i;
            }
        }
    }
    return -1;
};
```



https://www.codenong.com/cs106774902/

https://leetcode-cn.com/problems/implement-strstr/

https://www.jianshu.com/p/46f843545159

http://yikaj.github.io/2015/04/01/KMP%E7%AE%97%E6%B3%95%E2%80%94%E2%80%94Javascript%E5%AE%9E%E7%8E%B0/