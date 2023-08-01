# 102. Binary Tree Level Order Traversal

#트리

## 풀이 복기

문제를 풀면서 배운점이나 놓친점을 작성합니다.

### 풀이 1

```js
/**
 * AC
 * n: root 트리 노드 개수
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var levelOrder = function (root) {
  if (!root) {
    return [];
  }
  const nodes = rec(root, 0);
  const maxDepth = Math.max(...nodes.map(node => node.depth));
  const res = new Array(maxDepth + 1).fill(0).map(() => []);

  nodes.forEach(node => {
    const { depth, val } = node;
    res[depth].push(val);
  });

  return res;
};

var rec = function (tree, depth) {
  if (!tree) {
    return [];
  }
  return [{ depth, val: tree.val }, ...rec(tree.left, depth + 1), ...rec(tree.right, depth + 1)];
};
```

### 풀이 2

```js
/**
 * AC
 * n: root 트리 노드 개수
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var levelOrder = function (root) {
  if (!root) {
    return [];
  }

  let res = [];
  rec(root, 0);
  return res;

  function rec(node, depth) {
    if (!node) {
      return;
    }
    if (!res[depth]) {
      res[depth] = [];
    }

    res[depth].push(node.val);

    rec(node.left, depth + 1);
    rec(node.right, depth + 1);
  }
};
```
