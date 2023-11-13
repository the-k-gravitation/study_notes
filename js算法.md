## 时间复杂度 Big O notation

- O(1)
- O(log n)
- O(n)
- O(n log n)
- O(n^2)
- O(n^3)
- O(2^n), O(n!), ...

### 复杂度的计算

取复杂度最高的一项作为总体复杂度，前面的常数忽略

1. n^3 + n^2 + 1 的时间复杂度是 n^3
2. 2n^2 + 3n + 6 的时间复杂度是 n^2

### 时间复杂度为O(1)的例子

时间复杂度为O(1)在计算时，一般忽略。

```javascript
if(i === 1)

a = 1
result = 3 + 4
result = 10000*100000
array.push('a')
array.pop()
map.set(1,1)
map.get(1,1)
```

### 时间复杂度为O(n)的例子

`for循环`， `while循环`（不使用二分搜索）

```javascript
for(let i = 0; i<n; i++)

let i=0; while(i<n)

let a = 0;
for(let i =0;i<n; i++){
  a += i;
}
```

### 时间复杂度为O(n^2)的例子

`嵌套for循环`， `嵌套while循环`

```javascript
let a = 0;
for(let i =0; i < n; i++) {
  for (let j =0; j < n; j++) {
    a += i;
  }
}
```

### 时间复杂度为O(log n) 和 O(n log n)的例子

#### 二分搜索(二分查找) log n

#### 排序 n log n

## 空间复杂度

### 空间复杂度为O(1)的例子

const a = 1;
let str = 'a';

### 空间复杂度为O(n)的例子

定义一个长度为n的数组
定义一个长度为n的set，map
用for循环生成一个长度为n的链表

### 空间复杂度为O(n^2)的例子

二维数组
一维数组每个元素存放一个长度为n的set或者map或者链表

## 算法实现

### 冒泡排序

```js
/**
 * 冒泡排序
 * @param {*} a
 */
function bubble(a) {
  let count = a.length - 1 // 用来表示总共要大轮几回
  while (true) {
    //用来记录一轮之后，最后进行交易的第一个数值在Array中的索引
    let last = 0
    for (let i = 0; i < count; i++) {
      if (a[i] > a[i + 1]) {
        swap(a, i, i + 1)
        last = i
      }
    }
    count = last
    if (count === 0) {
      // 当count == 0时，就不需要再进行大的轮了
      break
    }
  }
}

function swap(a, i, j) {
  const temp = a[i]
  a[i] = a[j]
  a[j] = temp
}

bubble([5, 2, 7, 4, 1, 3, 8, 9])
```

### 选择排序

每次从反序集中选择其中的最大值或者最小值

属于不稳定的排序算法

```js
function selection(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    // i 代表每轮选择最小元素要交换到目标索引
    let s = i // s 代表每轮选择最小元素的索引
    for (let j = s + 1; j < arr.length; j++) {
      if (arr[j] < arr[s]) {
        s = j
      }
    }
    if (s !== i) {
      swap(arr, s, i)
    }
    console.log(arr)
  }
}

function swap(a, i, j) {
  const temp = a[i]
  a[i] = a[j]
  a[j] = temp
}

selection([5, 3, 7, 2, 1, 9, 8, 4])
```

### 插入排序

### 希尔排序

### 快速排序

## LeetCode

### 1. 两数之和

<https://leetcode.cn/problems/two-sum/submissions/481845517/?envType=study-plan-v2&envId=top-100-liked>

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。
示例 1：

输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
示例 2：

输入：nums = [3,2,4], target = 6
输出：[1,2]
示例 3：

输入：nums = [3,3], target = 6
输出：[0,1]

提示：

2 <= nums.length <= 104
-109 <= nums[i] <= 109
-109 <= target <= 109
只会存在一个有效答案

进阶：你可以想出一个时间复杂度小于 O(n2) 的算法吗？

```java
//java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> hashtable = new HashMap<Integer, Integer>();
        for(int i=0; i<nums.length;i++){
            int index = target - nums[i];
            if(hashtable.containsKey(index)){
                return new int[]{i, hashtable.get(index)};
            }
            hashtable.put(nums[i], i);
        }
        return new int[0];
    }
}
```

```javascript
//javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let n = nums.length;
    let hashtable = new Map();
    for(let i = 0; i<n; i++) {
        let index = target - nums[i];
        if(hashtable.has(index)){
            return [i,hashtable.get(index)]
        }
        hashtable.set(nums[i],i)
    }
};
```

### 2. 有效的字母异位词

给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

注意：若 s 和 t 中每个字符出现的次数都相同，则称 s 和 t 互为字母异位词。

示例 1:

输入: s = "anagram", t = "nagaram"
输出: true
示例 2:

输入: s = "rat", t = "car"
输出: false

提示:

1 <= s.length, t.length <= 5 * 104
s 和 t 仅包含小写字母

```java
// java
class Solution {
    public boolean isAnagram(String s, String t) {
        if( s.length() != t.length()){
            return false;
        }

        char[] str1 = s.toCharArray();
        char[] str2 = t.toCharArray();
        Arrays.sort(str1);
        Arrays.sort(str2);
        return Arrays.equals(str1, str2);
    }
}
```

```javascript
// javascript
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function(s, t) {
    // if(s.length !== t.length) return false;

    // let str1 = [...s].sort().toString(); 
    // let str2 = [...t].sort().toString();
    // return str1 === str2;
    s.length == t.length && [...s].sort().join('') === [...t].sort().join('')
};
```

```javascript
// javascript
// 如果输入字符串包含 unicode 字符
var isAnagram2 = function (s, t) {
  if (s.length !== t.length) return false
  let table = new Map()
  for (let ch of s) {
    table.set(ch, (table.get(ch) || 0) + 1)
    console.log(ch, table.get(ch))
  }

  for (let ch of t) {
    table.set(ch, (table.get(ch) || 0) - 1)
    if (table.get(ch) < 0) return false
  }

  return true 
}
```
