### 856 socre of parentheses

```javascript
/**
 * @param {string} S
 * @return {number}
 */

 /*
  time complexity O(n)
  space complexity O(n/2)
 */
var scoreOfParentheses = function(S) {
  const stack = [];
  let score = 0;

  for (let s of S) {
    if (s === '(') {
      stack.push(score);
      score = 0;
      console.log(`push: stack ${stack}`);
    } else {
      console.log(`before pop: stack ${stack}`);
      score = stack.pop() + Math.max(score*2, 1);
      console.log(`after pop: stack ${stack}, score ${score}`);
    }
  }
  
  return score;
};

/* sample code:
"((()()))"
stdout:
push: stack 0
push: stack 0,0
push: stack 0,0,0
before pop: stack 0,0,0
after pop: stack 0,0, score 1
push: stack 0,0,1
before pop: stack 0,0,1
after pop: stack 0,0, score 2
before pop: stack 0,0
after pop: stack 0, score 4
before pop: stack 0
after pop: stack , score 8
*/
```