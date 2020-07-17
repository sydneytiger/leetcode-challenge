### 剑指 Offer 05. 替换空格
#### 请实现一个函数，把字符串 s 中的每个空格替换成"%20"。
`示例: 输入：s = "We are happy."
输出："We%20are%20happy."`

`限制: 0 <= s 的长度 <= 10000`

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var replaceSpace = function(s) {
  return solution(s);
};

const simpleSolution = s => {
  return s.replace(/ /g, '%20');
}

// time complexity O(2n) space complexity O(n)
const solution = s => {
  const wsCount = s.split('').reduce((acc, curr) => {
    if(curr === ' ') acc++;
    return acc;
  }, 0)
  
  if(!wsCount) return s;
  
  let oldPointer = s.length - 1;
  let newPointer = oldPointer + wsCount * 2;
  const arr = new Array(s.length + wsCount * 2);
  
  while(oldPointer >= 0) {
    if(s[oldPointer] !== ' ') {
      arr[newPointer--] = s[oldPointer];
    } else {
      arr[newPointer--] = '0';
      arr[newPointer--] = '2';
      arr[newPointer--] = '%';
    }
    --oldPointer;
  }
  
  // console.log(arr);
  return arr.join('');
}
```
