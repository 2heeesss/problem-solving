# 994. Rotting Oranges

#그래프#BFS

## 풀이 복기

처음 접근할때 DFS만 생각했다. DFS로 문제를 풀다가 구현이 어려운걸 알고, 방법을 BFS로 변경했다.
JS로 BFS풀이를 할때 shift() 메서드를 사용해야하는데 이는 O(n) 시간복잡도가 걸리기때문에 주의해야함.

### 풀이 1

```js
/**
 * AC
 * n: grid column, m: grid row
 * 시간복잡도: O((n*m)^2) -> 각 셀은 한번씩만 방문하지만, shift() 메서드 때문에 제곱이 된다.
 * 공간복잡도: O(n*m)
 */
var orangesRotting = function (grid) {
  const col = grid.length;
  const row = grid[0].length;
  const dy = [0, 0, 1, -1];
  const dx = [1, -1, 0, 0];
  let minTime = 0;
  const rottenOranges = [];

  for (let i = 0; i < col; i++) {
    for (let j = 0; j < row; j++) {
      if (grid[i][j] === 2) {
        rottenOranges.push([i, j, 0]);
      }
    }
  }
  bfs(rottenOranges);

  const hasFreshOrange = grid.reduce((acc, cur) => acc || cur.some(orange => orange === 1), false);

  return hasFreshOrange ? -1 : minTime;

  function bfs(rottens) {
    const queue = [...rottens];

    while (queue.length) {
      const [currentRottenY, currentRottenX, time] = queue.shift();
      if (time !== 0 && grid[currentRottenY][currentRottenX] === 2) {
        continue;
      }
      minTime = time;
      grid[currentRottenY][currentRottenX] = 2;
      for (let i = 0; i < dy.length; i++) {
        const nextY = currentRottenY + dy[i];
        const nextX = currentRottenX + dx[i];
        const isInBound = 0 <= nextY && nextY < col && 0 <= nextX && nextX < row;
        if (isInBound && grid[nextY][nextX] === 1) {
          queue.push([nextY, nextX, time + 1]);
        }
      }
    }
  }
};
```
