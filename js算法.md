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

### 1.两数之和

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
            // 将 原来的 nums 的 索引 和 值，反过来存入到 hashtable中
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

### 2.两数相加

给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例 1：

输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
示例 2：

输入：l1 = [0], l2 = [0]
输出：[0]
示例 3：

输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]

提示：

每个链表中的节点数在范围 [1, 100] 内
0 <= Node.val <= 9
题目数据保证列表表示的数字不含前导零

```javascript
//javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */

function ListNode(val, next) {
  this.val = val === undefined ? 0 : val
  this.next = next === undefined ? null : next
}

const l1 = new ListNode(2)
l1.next = new ListNode(4)
l1.next.next = new ListNode(3)
const l2 = new ListNode(5)
l2.next = new ListNode(6)
l2.next.next = new ListNode(4)

const l3 = addTwoNumbers(l1, l2)
console.log(l3)

/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function(l1, l2) {
    let dummy = new ListNode();
    let curr = dummy;
    let carry = 0;

    while(l1 !== null || l2 !== null) {
        let sum =0;
        if(l1!==null) {
            sum += l1.val;
            l1 = l1.next;
        }

        if(l2 !== null) {
            sum += l2.val;
            l2 = l2.next;
        }

        sum += carry;

        curr.next = new ListNode(sum % 10);
        carry = Math.floor(sum/10);
        curr = curr.next;
    }

    if(carry>0){
        //如果最后 carry不为零，表示最后还有进位。
        curr.next = new ListNode(carry);
    }

    return dummy.next;
};
```

### 3.无重复字符的最长子串

给定一个字符串 s ，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:

输入: s = "abcabcbb"
输出: 3
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。

提示：

0 <= s.length <= 5 * 104
s 由英文字母、数字、符号和空格组成

```javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function (s) {
  const set = new Set()

  let i = 0,
    j = 0,
    maxLength = 0

  if (s.length === 0) return 0

  for (let i = 0; i < s.length; i++) {
    if (!set.has(s[i])) {
      set.add(s[i])
      maxLength = Math.max(maxLength, set.size)
    } else {
      while (set.has(s[i])) {
        set.delete(s[j])
        j++
      }
      set.add(s[i])
    }
  }

  return maxLength
}
```

### 5.最长回文子串

给你一个字符串 s，找到 s 中最长的回文子串。

如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。

示例 1：

输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。
示例 2：

输入：s = "cbbd"
输出："bb"

提示：

1 <= s.length <= 1000
s 仅由数字和英文字母组成

```javascript
//javascript
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function (s) {
  if (s.length < 2) return s

  let start = 0
  let maxLength = 1

  function expandAroundCenter(left, right) {
    while (left >= 0 && right < s.length && s[left] === s[right]) {
      let len = right - left + 1
      if (len > maxLength) {
        maxLength = len
        start = left
      }
      left--
      right++
    }
  }

  for (let i = 0; i < s.length; i++) {
    // 处理i右侧不与自己相同的
    expandAroundCenter(i - 1, i + 1)
    // 处理i右侧与自己相同的条件
    expandAroundCenter(i, i + 1)
  }

  return s.substring(start, start + maxLength)
}

```

### 242. 有效的字母异位词

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

### 56.合并区间

以数组 intervals 表示若干个区间的集合，其中单个区间为 intervals[i] = [starti, endi] 。请你合并所有重叠的区间，并返回 一个不重叠的区间数组，该数组需恰好覆盖输入中的所有区间 。

示例 1：

输入：intervals = [[1,3],[2,6],[8,10],[15,18]]
输出：[[1,6],[8,10],[15,18]]
解释：区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
示例 2：

输入：intervals = [[1,4],[4,5]]
输出：[[1,5]]
解释：区间 [1,4] 和 [4,5] 可被视为重叠区间。

```javascript
// javascript
var merge = function(intervals) {
  // 先按数组每项的第一位进行排序
  intervals.sort((a,b) => a[0] - b[0])

  let res = []
  for(let i=0;i<intervals.length;i++){
    let curr = intervals[i]
    // 当为第1个时或者，当前项的第1位已经大于 res 中的最后项中的第2位时，表示已经不连续，直接将当前 curr 添加到 res中
    if(res.length ===0 || res[res.length-1][1] < curr[0]){
        res.push(curr)
    }else{
        res[res.length -1][1] = Math.max(curr[1], res[res.length -1][1])
    }
  }
  return res
};
```

### 704.二分查找

给定一个 n 个元素有序的（升序）整型数组 nums 和一个目标值 target  ，写一个函数搜索 nums 中的 target，如果目标值存在返回下标，否则返回 -1。

示例 1:

输入: nums = [-1,0,3,5,9,12], target = 9
输出: 4
解释: 9 出现在 nums 中并且下标为 4
示例 2:

输入: nums = [-1,0,3,5,9,12], target = 2
输出: -1
解释: 2 不存在 nums 中因此返回 -1

```javascript
//javascript
var search = function (nums, target) {
  let left = 0
  let right = nums.length - 1
  // let mid = Math.floor(left + (right - left) / 2)
 
    // 注意要进行此处的判断为先
  while (left <= right) {
    // left + (right - left) / 2 是为了处理最大值溢出的问题
    let mid = Math.floor(left + (right - left) / 2)
    if (nums[mid] === target) return mid
    else if (nums[mid] < target) {
      left = mid + 1
    } else {
      right = mid - 1
    }
  } 
    return -1
  }
}

let nums = [-1, 0, 3, 5, 9, 12]
console.log(search(nums, 9))
```

###
