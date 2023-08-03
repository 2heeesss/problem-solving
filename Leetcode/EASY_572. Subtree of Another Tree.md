# 572. Subtree of Another Tree

#트리

## 풀이 복기

DFS를 사용해서 root, sub의 시작 값이 같다면 재귀함수를 통해서 해당 서브트리들이 같은 값을 가지고있는지 확인하는 방법으로 풀었다.

이번에 풀때 시간복잡도를 계산하지 않고 풀었는데, 실전에서는 먼저 계산하고 풀자

### 풀이 1

```js
/**
 * AC
 * n: root트리 노드 개수, m: subRoot트리 노드 개수
 * 시간복잡도: O(nm)
 * 공간복잡도: O(nm)
 */
var isSubtree = function (root, subRoot) {
  const stack = [root];
  while (stack.length) {
    const node = stack.pop();
    if (!node) {
      continue;
    }
    if (node.val === subRoot.val) {
      const res = rec(node, subRoot);
      if (res) {
        return res;
      }
    }

    stack.push(node.left);
    stack.push(node.right);
  }
  return false;
};

var rec = function (root, subRoot) {
  if (!root && !subRoot) {
    return true;
  }
  if ((root && !subRoot) || (!root && subRoot) || root.val !== subRoot.val) {
    return false;
  }
  return rec(root.left, subRoot.left) && rec(root.right, subRoot.right);
};
```
