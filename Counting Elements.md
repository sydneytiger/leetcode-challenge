### Counting Elements (30 days challenge on 7 Apr 2020)
```javascript
/**
 * @param {number[]} arr
 * @return {number}
 */
var countElements = function(arr) {
  return solution2(arr);
};

// time complexity O(2n) space complexity O(n)
const solution1 = arr => {
  const state = {};
  
  for(let i = 0; i < arr.length; i++){
    const num = arr[i];
    if(state[num]) {
      state[num] = state[num] + 1;
    } else {
      state[num] = 1;
    }
  }
  
  let result = 0;
  let keys = Object.keys(state);
  keys.sort((a, b) => a - b);
  
  //console.log(keys);
  for(let i = 1; i < keys.length; i++){
    if(keys[i] - keys[i-1] === 1) result += state[keys[i-1]];
    
    //console.log(`keyi ${keys[i]} keyi-1 ${keys[i - 1]} result ${result}`);
  }
  
  return result;
}

// time complexity O(n), space complexity O(1)
const solution2 = arr => {
  arr.sort((a, b) => a - b);
  let mostLeft = 0;
  let result = 0;
  let prevVal = null;
  
  for(let i = 0; i < arr.length; i++) {
    const val = arr[i];
    if(val != prevVal) {
      if(val - prevVal === 1) {
        result += i - mostLeft;
      }
      mostLeft = i;
      prevVal = val;
    }
  }
    
  return result;
}
```