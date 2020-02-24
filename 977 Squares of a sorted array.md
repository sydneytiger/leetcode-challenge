### Squres of a sorted array
```javascript
/**
 * @param {number[]} A
 * @return {number[]}
 */
var sortedSquares = function(A) {
    let right = A.length - 1;
    let left = 0;

    const result = new Array(A.length).fill(0);

    for (let i = result.length - 1; i >= 0; i--) {
      //console.log(`i is ${i}`);
      if(Math.abs(A[left]) > A[right]) {
        // console.log(`left is ${left}`);
        // console.log(`pick number is ${A[left]}`);
        
        result[i]= Math.pow(A[left], 2);
        left ++;
      } else {
        // console.log(`right is ${right}`);
        // console.log(`pick number is ${A[right]}`);
        
        result[i] = Math.pow(A[right], 2);
        right --;
      }
      //console.log(`filled number is is ${result[i]} right: ${right} left: ${left}`);
    }

    return result;
};
``