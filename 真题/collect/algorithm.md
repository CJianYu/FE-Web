1. 懵逼的时候： 暴力？基本情况？
2. 找 最近重复子问题
3. If/else;   for while; recursion

### 递归代码模版

```javascript
function recur(level, program) {
  // terminate
  if(level > max_level) {
    return
  }
  // process current level（split your big problem)
  process(level, program)
  // drill down(subResult)
  recur(level+1, newProgram)
  // reverse state
}
```



我们先写两个公共的函数：

```javascript
// 检查数组是否为空
function checkArray(array) {
  if(!array) return
}

// 位置交换
function swap(array, left, right) {
  let rightValue = array[right]
  array[right] = array[left]
  array[left] = rightValue
}
```



1. 冒泡排序

```javascript
function bubbleSort(array) {
  checkArray(array)
  for(let i = array.length; i > 0; i--) {
    for(let j = 0; j < i; j++) {
      if(array[j] > array[j+1]) {
        swap(array, j, j+1)
      }
    }
  }
  return array
}
```

2. 插入排序

```javascript
// 取出未排序的元素，将该元素与已排序的列表中最大的元素比较，该元素更小则两者交换位置，继续与下一个元素比较
function insertSort(array) {
  checkArray(array) 
  for(let i = 1; i < array.length; i++) {
    for(let j = i - 1; j >= 0 && array[j] > array[j + 1]; j--) {
      swap(array, j, j + 1)
    }
  }
  return array
}
```

3. 选择排序

```javascript
function selectionSort(array) {
  checkArray(array)
  for(let i = 0; i < array.length - 1; i++) {
    let minIndex = i
    for(let j = i + 1; j < array.length; j++) {
      minIndex = array[j] < arry[minIndex] ? j : minIndex
    }
    swap(array, i, minIndex)
  }
  return array
}
```

4. 快速排序

```javascript
Array.prototype.quickSort = function() {
    const l = this.length
    if(l < 2) return this
    const basic = this[0], left = [], right = []
    for(let i = 1; i < l; i++) {
      const iv = this[i]
      iv > basic && right.push(iv) // to avoid repeatly element.
      iv < basic && left.push(iv)
    }
    return left.quickSort().concat(basic, right.quickSort())
}
const arr = [5, 3, 7, 4, 1, 9, 8, 6, 2];
const ascendArr = arr.quickSort()
```

5. 归并排序

把一个有 n 个记录的无需文件看成是由 n 个长度为 1 的有序子文件组成的文件，然后进行两两归并

![img](https://user-gold-cdn.xitu.io/2020/5/31/17268ebaae461abf?imageslim)

```typescript
function mergeSort(list: number[]): number[] {
  const len = list.length
  if(len < 2) {
    return list
  }
  const mid = Math.floor(len / 2)
  const left = list.slice(0, mid)
  const right = list.slice(mid)
  
  function merge(left: number[], right: number[]): number[] {
    const result: number[] = []
    
    while(left.length && right.length) {
      if(left[0] < right[0]) {
        result.push(left.shift())
      } else {
        result.push(right.shift())
      }
    }
    
    while(left.length) result.push(left.shift())
    
    while(right.length) result.push(right.shift())
    
    return result
  }
  
  return merge(mergeSort(left), mergeSort(right))
}
```



通讯录

```javascript
const arr4 = ["John Alpha", "Elle Cappa", "Allen Beta"];
arr4.sort((a, b) => a.split(' ')[1].localeCompare(b.split(' ')[1]));

sortData(data,field){//data原数据，field数据的拼音键名。
				let letter_reg = /^[A-Z]$/;
				let list = [];
				let letter = '';
				for (let i = 0; i < data.length; i++) {
					// 添加 # 分组，用来 存放 首字母不能 转为 大写英文的 数据
					list['#'] = [];
					// 首字母 转 大写英文
					letter = (data[i][field]).slice(0, 1).toUpperCase();
					// 是否 大写 英文 字母
					if (!letter_reg.test(letter)) {
						letter = '#';
					}
					// 创建 字母 分组
					if (!(letter in list)) {
						list[letter] = [];
					}
					// 字母 分组 添加 数据
					list[letter].push(data[i]);
				}
				// 转换 格式 进行 排序；
				let resault = [];
				for (let key in list) {
					resault.push({
						letter: key,
						list: list[key]
					});
				}
				resault.sort((a,b) => {
					return a.letter.charCodeAt(0) - b.letter.charCodeAt(0);
				});
				// # 号分组 放最后
				let last_arr = resault[0];
				resault.splice(0, 1);
				resault.push(last_arr);
			 
				// 转换 数据 格式
				let json_sort = {}
				for (let i = 0; i < resault.length; i++) {
					json_sort[resault[i].letter] = resault[i].list;
				}
			 
				return resault;
}
```

