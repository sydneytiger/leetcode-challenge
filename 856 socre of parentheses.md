### 856 socre of parentheses

```javascript
/**
 * @param {string} S
 * @return {number}
 */
var scoreOfParentheses = function(S) {
  const stack = [];
  let score = 0;

  for (let s of S) {
    if (s === '(') {
      stack.push(score);
      score = 0;
    } else {
      score = stack.pop() + Math.max(score*2, 1)
    }
  }
  
  return score;
};

```