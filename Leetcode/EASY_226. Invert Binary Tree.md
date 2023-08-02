# 226. Invert Binary Tree

#트리

## 풀이 복기

오타때문에 5분가량 지체됨. 프로퍼티 오타는 알려주지 않으니 잘 확인해야함

### 풀이 1

```js
/**
 * AC
 * n: 노드의 개수
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var invertTree = function (root) {
  if (!root) {
    return root;
  }

  rec(root);
  return root;
};

var rec = function (node) {
  if (!node) {
    return;
  }

  [node.left, node.right] = [node.right, node.left];
  rec(node.left);
  rec(node.right);
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
var invertTree = function (root) {
  if (!root) {
    return root;
  }

  [root.left, root.right] = [root.right, root.left];
  invertTree(root.left);
  invertTree(root.right);

  return root;
};
```
