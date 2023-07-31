# 문제 제목

#트리

## 풀이 복기

트리 두개를 한번에 재귀하면서 같거나, 같지 않거나, 노드가 있거나, 없거나 분기문으로 조건을 확인하는 방법

### 풀이 1

```js
/**
 * AC
 * n: 노드의 개수
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var isSameTree = function (p, q) {
  return rec(p, q);
};

var rec = function (tree1, tree2) {
  if (!tree1 && !tree2) {
    return true;
  } else if (tree1 && !tree2) {
    return false;
  } else if (!tree1 && tree2) {
    return false;
  } else if (tree1.val !== tree2.val) {
    return false;
  } else {
    return rec(tree1.left, tree2.left) && rec(tree1.right, tree2.right);
  }
};
```
