### Leftmost Column with at Least a One
```javascript
/**
 * // This is the BinaryMatrix's API interface.
 * // You should not implement it, or speculate about its implementation
 * function BinaryMatrix() {
 *     @param {integer} x, y
 *     @return {integer}
 *     this.get = function(x, y) {
 *         ...
 *     };
 *
 *     @return {[integer, integer]}
 *     this.dimensions = function() {
 *         ...
 *     };
 * };
 */

/**
 * @param {BinaryMatrix} binaryMatrix
 * @return {number}
 */
var leftMostColumnWithOne = function(binaryMatrix) {
  
  return solution2(binaryMatrix);
};

// start from top right [0, column - 1]
// 0 => move down (x + 1)
// 1 => move left (y - 1)
const solution2 = binaryMatrix => {
  const dimension = binaryMatrix.dimensions();
  const row = dimension[0];
  const column = dimension[1];
  let x = 0;
  let y = column - 1;
  
  while(x < row && y >= 0) {
    const val = binaryMatrix.get(x, y);
    if(val){
      --y;
    } else {
      ++x;
    }
  }
  
  console.log(`x ${x}, y ${y}`);
  return y === column - 1 ? -1 : y + 1;
}


// You made too many calls to BinaryMatrix.get().
const solution1 = binaryMatrix => {
  const dimension = binaryMatrix.dimensions();
  const row = dimension[0];
  const column = dimension[1];
  console.log(`row ${row} column ${column}`)
  let mostLeft = Number.MAX_SAFE_INTEGER;
  
  for(let r = 0; r < row; r++) {
    const mostLeftOnRow = binarySearch(binaryMatrix, r, column);
    
    if(mostLeftOnRow === -1) continue;
    if(mostLeftOnRow === 0) return 0;
    mostLeft = Math.min(mostLeft, binarySearch(binaryMatrix, r, column))
  }
  
  return mostLeft === Number.MAX_SAFE_INTEGER ? -1 : mostLeft;
}

const binarySearch = (binaryMatrix, row, len) => {
  let left = 0;
  let right = len - 1;
  
  while(left + 1 < right) {
    const mid = left + Math.floor((right - left) / 2);
    const val = binaryMatrix.get(row, mid);
    if(val === 1) {
      right = mid;
    } else {
      left = mid;
    }
  }
  
  const leftVal = binaryMatrix.get(row, left);
  const rightVal = binaryMatrix.get(row, right);
  if(leftVal === 0 && rightVal === 1) {
    return right;
  } else if((leftVal === 1 && rightVal === 1)) {
    return 0;
  } else {
    return -1
  }

}





```
