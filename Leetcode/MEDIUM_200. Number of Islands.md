# 200. Number of Islands

#그래프

### 풀이 1

```js
/**
 * AC
 * n: grid col, m: grid row
 * 시간복잡도: O(n*m)
 * 공간복잡도: O(n*m)
 */
var numIslands = function (grid) {
  const col = grid.length;
  const row = grid[0].length;
  const dy = [0, 0, 1, -1];
  const dx = [1, -1, 0, 0];
  const visited = new Array(col).fill(0).map(() => new Array(row).fill(false));

  function dfs(currentY, currentX) {
    visited[currentY][currentX] = true;

    for (let i = 0; i < dy.length; i++) {
      const nextY = currentY + dy[i];
      const nextX = currentX + dx[i];
      const isInBound = 0 <= nextY && nextY < col && 0 <= nextX && nextX < row;

      if (isInBound && grid[nextY][nextX] === '1' && !visited[nextY][nextX]) {
        dfs(nextY, nextX);
      }
    }
  }

  let cnt = 0;
  for (let i = 0; i < col; i++) {
    for (let j = 0; j < row; j++) {
      if (grid[i][j] === '1' && !visited[i][j]) {
        dfs(i, j);
        cnt += 1;
      }
    }
  }

  return cnt;
};
```
