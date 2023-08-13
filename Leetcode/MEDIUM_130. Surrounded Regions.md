# 130. Surrounded Regions

#그래프#DFS

## 풀이 복기

풀이에서 중요한점은 작은 문제로 나눠서 생각하는것. 까먹지말자. 일반적인 DFS로 모든 요소를 탐색하려고 하지말고, 가능한 적은 셀만 DFS호출하는게 효율적이다.

### 풀이 1

```js
/**
 * AC
 * n: board col, m: board row
 * 시간복잡도: O(n*m)
 * 공간복잡도: O(n*m)
 */
var solve = function (board) {
  const [dy, dx] = [
    [0, 0, 1, -1],
    [1, -1, 0, 0],
  ];
  const [col, row] = [board.length, board[0].length];
  const visitedCharO = new Array(col).fill(0).map(() => new Array(row).fill(false));

  for (let i = 0; i < col; i++) {
    dfs(i, 0);
    dfs(i, row - 1);
  }
  for (let j = 0; j < row; j++) {
    dfs(0, j);
    dfs(col - 1, j);
  }

  for (let i = 0; i < col; i++) {
    for (let j = 0; j < row; j++) {
      if (!visitedCharO[i][j]) {
        board[i][j] = 'X';
      }
    }
  }

  function dfs(y, x) {
    if (visitedCharO[y][x] || board[y][x] === 'X') {
      return;
    }
    visitedCharO[y][x] = true;

    for (let i = 0; i < dy.length; i++) {
      const nextY = y + dy[i];
      const nextX = x + dx[i];
      const isInBound = 0 <= nextY && nextY < col && 0 <= nextX && nextX < row;

      if (isInBound && !visitedCharO[nextY][nextX] && board[nextY][nextX] === 'O') {
        dfs(nextY, nextX);
      }
    }
  }
};
```
