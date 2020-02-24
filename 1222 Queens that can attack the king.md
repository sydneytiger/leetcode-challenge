### 1222 Queens that can attack the king
```javascript
/**
 * @param {number[][]} queens
 * @param {number[]} king
 * @return {number[][]}
 */

var queensAttacktheKing = function(queens, king) {
  const result = [];
  const moveDirection = [-1, 0, 1];
  
  moveDirection.forEach(dx => {
    moveDirection.forEach(dy => {
      if (dx === 0 && dy === 0) return;

      let x = king[0] + dx;
      let y = king[1] + dy;

      while (x >= 0 && y >= 0 && x < 8 && y < 8) {
        if(hasQueen(queens, [x, y])) {
          result.push([x, y]);
          return;
        }
        
        x += dx;
        y += dy;
      }
    })
  })
  
  return result;
}

const hasQueen = function(queens, position) {

  for (let i = 0; i < queens.length; i++) {
    const coordinate = queens[i];
    if(coordinate[0] === position[0] && coordinate[1] === position[1]){
      return true;
    }
  }

  return false;
}
```