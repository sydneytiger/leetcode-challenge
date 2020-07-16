### 剑指 Offer 03. 数组中重复的数字

#### 找出数组中重复的数字。

#### 在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

`示例: 输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 `

`限制: 2 <= n <= 100000`

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var findRepeatNumber = function(nums) {
  return indexToNum(nums);
};

// time complexity O(nlogn + n) space complexity O(1)
const sortAndSeek = nums => {
  nums.sort((a, b) => a - b);
  let i = 0;
  
  while(i < nums.length - 1) {
    if(nums[i] === nums[i + 1]) return nums[i]
    ++i;
  }
}

// time complexity O(n) space complexity O(n)
const hashSet = nums => {
  const set = new Set();
  for(let num of nums) {
    if(set.has(num)) return num;
    set.add(num);
  }
}

// time complexity O(n) space complexity O(1)
const indexToNum = nums => {
  let i = 0;
    
  while(i < nums.length) {
    if(nums[i] === i) {
      i++;
    } else {
      const temp = nums[i];
      if(temp=== nums[temp]) return temp;
      nums[i] = nums[temp];
      nums[temp] = temp;
    }
    
  }
}
```
