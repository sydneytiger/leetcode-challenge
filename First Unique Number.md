### First Unique Number
```javascript
// ES 6
/**
 * @param {number[]} nums
 */
class FirstUnique {
  constructor(nums) {
    this.head = new Node();
    this.tail = new Node();
    this.head.next = this.tail;
    this.tail.prev = this.head;

    this.map = nums.reduce((acc, num) => {
      const count = acc.get(num) ? acc.get(num) + 1 : 1;
      acc.set(num, count);
      return acc;
    }, new Map());

    // console.log(this.map);

    for(let i = 0; i < nums.length; i++){
      if(this.map.get(nums[i]) === 1) {
        const node = new Node(nums[i]);
        this.addNoteToTail(node);
      } 
    }

    // console.log(this.head);
  }
  
  showFirstUnique() {
    const val = this.head.next.val;
    // console.log(val);
    return val ? val : -1;
  }
  
  add(value) {
    const exist = this.map.has(value);
  
    if(exist){
      this.map.set(value, this.map.get(value) + 1);
      const foundNode = this.findNode(value);
      if(foundNode) {
        this.removeNode(foundNode);
      }
    } else {
      this.map.set(value, 1);
      this.addNoteToTail(new Node(value));
    }
  }
  
  addNoteToTail(node) {
    const lastNode = this.tail.prev;
    node.prev = lastNode;
    node.next = this.tail;
    lastNode.next = node;
    this.tail.prev = node;
  }
  
  findNode(val) {
    let current = this.head;
    while(current) {
      if(current.val === val) return current;
      current = current.next;
    }

    return null;
  }
  
  removeNode(node) {
    if(!node) return;

    const prevNode = node.prev;
    const nextNode = node.next;
    prevNode.next = nextNode;
    nextNode.prev = prevNode;
  }
}

class Node{
  constructor(val){
    this.val = val;
    this.next = null;
    this.prev = null;
  }
}

/** 
 * Your FirstUnique object will be instantiated and called as such:
 * var obj = new FirstUnique(nums)
 * var param_1 = obj.showFirstUnique()
 * obj.add(value)
 */
```

```javascript
// ES 5
/**
 * @param {number[]} nums
 */
var FirstUnique = function(nums) {
  this.head = new Node();
  this.tail = new Node();
  this.head.next = this.tail;
  this.tail.prev = this.head;
  
  this.map = nums.reduce((acc, num) => {
    const count = acc.get(num) ? acc.get(num) + 1 : 1;
    acc.set(num, count);
    return acc;
  }, new Map());
  
  // console.log(this.map);
  
  for(let i = 0; i < nums.length; i++){
    if(this.map.get(nums[i]) === 1) {
      const node = new Node(nums[i]);
      this.addNoteToTail(node);
    } 
  }
  
  // console.log(this.head);
};

function Node(val){
  this.val = val;
  this.next = null;
  this.prev = null;
};

/**
 * @return {number}
 */
FirstUnique.prototype.showFirstUnique = function() {
  const val = this.head.next.val;
  // console.log(val);
  return val ? val : -1;
};

/** 
 * @param {number} value
 * @return {void}
 */
FirstUnique.prototype.add = function(value) {
  const exist = this.map.has(value);
  
  if(exist){
    this.map.set(value, this.map.get(value) + 1);
    const foundNode = this.findNode(value);
    if(foundNode) {
      this.removeNode(foundNode);
    }
  } else {
    this.map.set(value, 1);
    this.addNoteToTail(new Node(value));
  }
};

FirstUnique.prototype.addNoteToTail = function(node) {
  const lastNode = this.tail.prev;
  node.prev = lastNode;
  node.next = this.tail;
  lastNode.next = node;
  this.tail.prev = node;
};

FirstUnique.prototype.removeNode = function(node) {
  if(!node) return;
  
  const prevNode = node.prev;
  const nextNode = node.next;
  prevNode.next = nextNode;
  nextNode.prev = prevNode;
};

FirstUnique.prototype.findNode = function(val) {
  let current = this.head;
  while(current) {
    if(current.val === val) return current;
    current = current.next;
  }
  
  return null;
};

/** 
 * Your FirstUnique object will be instantiated and called as such:
 * var obj = new FirstUnique(nums)
 * var param_1 = obj.showFirstUnique()
 * obj.add(value)
 */
```