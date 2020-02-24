### 713 Subarray product less than K
```javascript
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var numSubarrayProductLessThanK = function(nums, k) {
  if(k <= 1) return 0;
  
  let left = 0;
  let right = 0;
  let product = 1;
  let result = 0;
  
  while(right < nums.length) {
    product *= nums[right];
    //console.log(`@@product ${product}, left ${left}, right ${right} result ${result}`);
    
    while(product >= k) {
      product /= nums[left];
      left++;
    }
    
    result += right - left + 1;
    
    right++;
  }
  return result;
};
```