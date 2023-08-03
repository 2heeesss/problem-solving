# 199. Binary Tree Right Side View

#트리

## 풀이 복기

1번 풀이는 잘못된 접근법으로 틀렸다. 트리의 오른쪽부분만 확인하면 되는 간단한 문제로 착각함.

2번 풀이는 모든 노드를 DFS로 순회하며 각 depth 를 2차원 배열로 저장하여 계산하는 방법으로 풀었다.

3번 풀이는 BFS를 사용해서 모든 노드에 접근하고, 가장 오른쪽에 있는 노드만 배열에 저장하는 방법으로 풀었다.

JS로 탐색 문제를 풀때 shift()때문에 BFS는 잘 사용하지 않았는데, 그래도 연습이 필요한 부분인것같다.

### 풀이 1

```js
/**
 * Fail
 */
var rightSideView = function (root) {
  if (!root) {
    return [];
  }
  if (root.right) {
    return [root.val, ...rightSideView(root.right)];
  } else {
    return [root.val, ...rightSideView(root.left)];
  }
};
```

### 풀이 2

```js
/**
 * AC
 * n: 트리 노드 개수
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var rightSideView = function (root) {
  const arr = [];
  function rec(node, depth) {
    if (!node) {
      return;
    }
    if (!arr[depth]) {
      arr[depth] = [];
    }
    arr[depth].push(node.val);

    rec(node.left, depth + 1);
    rec(node.right, depth + 1);
  }

  rec(root, 0);

  return arr.map(treeDepthVals => treeDepthVals.at(-1)).flat();
};
```

### 풀이 3

```js
/**
 * 시간복잡도: O(n^2) -> shift() 때문에
 * 공간복잡도: O(n)
 */
var rightSideView = function (root) {
  const arr = [];
  if (root === null) return arr;

  const queue = [root];

  while (queue.length) {
    const size = queue.length;
    for (let i = 0; i < size; i++) {
      let n = queue.shift();
      if (i === size - 1) arr.push(n.val);
      if (n.left) queue.push(n.left);
      if (n.right) queue.push(n.right);
    }
  }

  return arr;
};
```
