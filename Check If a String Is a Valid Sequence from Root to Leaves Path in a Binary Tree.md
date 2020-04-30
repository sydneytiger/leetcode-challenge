### Check If a String Is a Valid Sequence from Root to Leaves Path in a Binary Tree
```javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @param {number[]} arr
 * @return {boolean}
 */
var isValidSequence = function(root, arr) {
  return helper(root, arr, 0);
};

const helper = (node, arr, index) => {
  if(!node) return false;
  if(index > arr.length - 1) return false;
  
  if(node.val === arr[index]) {
    if(index === arr.length - 1 && !node.left && !node.right) return true;
    
    const left = helper(node.left, arr, index + 1);
    const right = helper(node.right, arr, index + 1);
    return left || right;
  }
  
  return false;
}
```
