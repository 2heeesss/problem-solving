# 104. Maximum Depth of Binary Tree

#트리

### 풀이 1

```js
/**
 * AC
 * n: 노드의 개수
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var maxDepth = function (root) {
  if (!root) {
    return root;
  }

  const depth = rec(root, 0);

  return depth;
};

var rec = function (node, depth) {
  if (!node) {
    return depth;
  }

  const leftCnt = rec(node.left, depth + 1);
  const rightCnt = rec(node.right, depth + 1);
  return Math.max(leftCnt, rightCnt);
};
```

### 풀이 2

```js
/**
 * AC
 * n: 노드의 개수
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var maxDepth = function (root, depth = 0) {
  if (!root) {
    return depth;
  }

  const leftCnt = maxDepth(root.left, depth + 1);
  const rightCnt = maxDepth(root.right, depth + 1);
  return Math.max(leftCnt, rightCnt);
};
```
