# 695. Max Area of Island

#그래프

### 풀이 1

```js
/**
 * AC
 * n: grid col, m: grid row
 * 시간복잡도: O(n*m)
 * 공간복잡도: O(n*m)
 */
var maxAreaOfIsland = function (grid) {
  const col = grid.length;
  const row = grid[0].length;
  const visited = new Array(col).fill(0).map(() => new Array(row).fill(false));
  const dy = [0, 0, 1, -1];
  const dx = [1, -1, 0, 0];

  function dfs(currentY, currentX) {
    visited[currentY][currentX] = true;
    let visitCnt = 1;

    for (let i = 0; i < dy.length; i++) {
      const nextY = currentY + dy[i];
      const nextX = currentX + dx[i];
      const isInBound = 0 <= nextY && nextY < col && 0 <= nextX && nextX < row;

      if (isInBound && !visited[nextY][nextX] && grid[nextY][nextX] === 1) {
        visitCnt += dfs(nextY, nextX);
      }
    }

    return visitCnt;
  }

  let res = 0;

  for (let i = 0; i < col; i++) {
    for (let j = 0; j < row; j++) {
      if (!visited[i][j] && grid[i][j] === 1) {
        res = Math.max(res, dfs(i, j));
      }
    }
  }

  return res;
};
```
