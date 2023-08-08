# 79. Word Search

#DFS

## 풀이 복기

DFS를 사용해서 보드를 순회하며 글자를 찾으면 된다. 기본적인 해결방법에서는 실수하지 않는데, 리턴문 그리고 방문처리 다시 돌리기에서 실수하는 경우가 생긴다. 방문처리한거 다시 돌리는건 항상 생각하자.

### 풀이 1

```js
/**
 * AC
 * n: board.length, m: board[i].length
 * 시간복잡도: O((n*m)^2)
 * 공간복잡도: O(n*m) -> DFS 최대깊이는 word.length인데 이는 상수이므로 빼기
 */
var exist = function (board, word) {
  const dy = [0, 0, 1, -1];
  const dx = [1, -1, 0, 0];

  function dfs(currentY, currentX, wordIdx, visited) {
    if (wordIdx === word.length - 1) {
      return true;
    }

    let flag = false;
    visited[currentY][currentX] = true;

    for (let i = 0; i < dy.length; i++) {
      const nextY = currentY + dy[i];
      const nextX = currentX + dx[i];
      const isInBound = 0 <= nextY && nextY < board.length && 0 <= nextX && nextX < board[0].length;
      if (isInBound && !visited[nextY][nextX] && board[nextY][nextX] === word[wordIdx + 1]) {
        flag = flag || dfs(nextY, nextX, wordIdx + 1, visited);
      }
    }
    visited[currentY][currentX] = false;

    return flag;
  }

  for (let i = 0; i < board.length; i++) {
    for (let j = 0; j < board[0].length; j++) {
      if (board[i][j] === word[0]) {
        const visited = new Array(board.length).fill(0).map(() => new Array(board[0].length).fill(false));
        const hasWord = dfs(i, j, 0, visited);
        if (hasWord) {
          return true;
        }
      }
    }
  }

  return false;
};
```
