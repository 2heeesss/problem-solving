# 417. Pacific Atlantic Water Flow

#그래프#DFS

## 풀이 복기

1번 풀이는 아예 잘못된 접근법으로 틀렸다. 각 셀마다 DFS로 대서양과 태평양에 도달할 수 있는지 확인한다. 만약 도달 가능하다면 원본배열의 경로 좌표를 true로, 도달하지 않는다면 false로 바꿔준다.

만약 모든 좌표에 대해서 true, false 처리를 안하고 순회할 시 200\*200 배열까지 입력 가능하므로 시간초과 날것이라고 예상

이 방법은 하나의 함수에서 너무 많은 일을 처리하게되므로 코드가 복잡해진다. 그래서 나중에 디버깅하기도 어렵게 됨..

2번 풀이는 모든 셀에 대해서 dfs를 호출하지 않는다. 테두리에 있는 즉, 태평양 || 대서양의 시작점인 셀만 DFS 호출한다. 태평양은 태평양방문배열, 대서양은 대서양방문배열에 각각 방문처리를 한다. 전부 DFS를 호출한 이후에는 방문처리가 동일하게 완료된 좌표만 정답배열에 저장한다.

2번 풀이에서 중요한점은 작은 문제로 나눠서 생각하는것, 그리고 입력의 범위를 보고 적절한 해결책을 찾는것.

### 풀이 1

```js
/**
 * Fail
 */
var pacificAtlantic = function (heights) {
  const col = heights.length;
  const row = heights[0].length;
  const dy = [0, 0, 1, -1];
  const dx = [1, -1, 0, 0];

  for (let i = 0; i < col; i++) {
    for (let j = 0; j < row; j++) {
      const vi = new Array(col).fill(0).map(() => new Array(row).fill(false));
      dfs(i, j, { pacific: false, atlantic: false }, vi);
    }
  }

  function dfs(currentY, currentX, state, visited) {
    visited[currentY][currentX] = true;
    if (currentY === 0 || currentX === 0) {
      state.pacific = true;
    }
    if (currentY === col - 1 || currentX === row - 1) {
      state.atlantic = true;
    }
    if (state.pacific && state.atlantic) {
      heights[currentY][currentX] = true;
      return true;
    }

    if (heights[currentY][currentX] === true) {
      return true;
    } else if (heights[currentY][currentX] === false) {
      return false;
    }

    let flag = false;
    for (let i = 0; i < dy.length; i++) {
      const nextY = currentY + dy[i];
      const nextX = currentX + dx[i];
      const isInBound = 0 <= nextY && nextY < col && 0 <= nextX && nextX < row;

      if (isInBound && !visited[nextY][nextX] && heights[currentY][currentX] >= heights[nextY][nextX]) {
        if (heights[nextY][nextX] !== true && heights[nextY][nextX] !== false) {
          flag = flag || dfs(nextY, nextX, state, visited);
        }
      }
    }

    heights[currentY][currentX] = flag;

    return flag;
  }
};
```

### 풀이 2

```js
/**
 * AC
 * n: height col, m: height row
 * 시간복잡도: O((n+m) * (n*m))
 * 공간복잡도: O(n*m)
 */
var pacificAtlantic = function (heights) {
  const col = heights.length;
  const row = heights[0].length;
  const pacific = new Array(col).fill(0).map(() => new Array(row).fill(false));
  const atlantic = new Array(col).fill(0).map(() => new Array(row).fill(false));
  const dy = [0, 0, 1, -1];
  const dx = [1, -1, 0, 0];
  for (let i = 0; i < row; i++) {
    // 1. pacific이 갈 수 있는 좌표 찾기
    if (!pacific[0][i]) {
      dfs(0, i, pacific);
    }
    // 2. atlantic이 갈 수 있는 좌표 찾기
    if (!atlantic[col - 1][i]) {
      dfs(col - 1, i, atlantic);
    }
  }

  for (let j = 0; j < col; j++) {
    if (!pacific[j][0]) {
      dfs(j, 0, pacific);
    }
    if (!atlantic[j][row - 1]) {
      dfs(j, row - 1, atlantic);
    }
  }

  const res = [];
  for (let i = 0; i < col; i++) {
    for (let j = 0; j < row; j++) {
      if (pacific[i][j] && atlantic[i][j]) {
        res.push([i, j]);
      }
    }
  }

  return res;

  function dfs(y, x, oceanVisited) {
    oceanVisited[y][x] = true;

    for (let i = 0; i < dy.length; i++) {
      const nextY = y + dy[i];
      const nextX = x + dx[i];
      const isInBound = 0 <= nextY && nextY < col && 0 <= nextX && nextX < row;
      if (isInBound && !oceanVisited[nextY][nextX] && heights[y][x] <= heights[nextY][nextX]) {
        dfs(nextY, nextX, oceanVisited);
      }
    }
  }
};
```
