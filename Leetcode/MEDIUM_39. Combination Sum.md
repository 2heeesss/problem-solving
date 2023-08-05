# 39. Combination Sum

#백트래킹

## 풀이 복기

target의 값보다 지금까지 경로의 합이 작을때는, 재귀를 이어서 더 깊이 들어간다. 나머지 경우에는 재귀를 종료하고, 합과 target이 같을때는 res배열에 지금까지 경로를 복사해서 저장한다.

재귀의 동작방식만 잘 이해하고있다면 dfs 또는 backtracking 을 수월하게 풀수있을듯

### 풀이 1

```js
/**
 * AC
 * n: candidates.length, k: target / candidates[i]
 * 시간복잡도: O(2^k)
 * 공간복잡도: O(2^k)
 */
var combinationSum = function (candidates, target) {
  const res = [];
  const subset = [];

  function sum() {
    return subset.reduce((acc, cur) => acc + cur, 0);
  }

  function backtrack(idx) {
    const subsetSum = sum();
    if (idx >= candidates.length || subsetSum > target) {
      return;
    }
    if (subsetSum === target) {
      res.push([...subset]);
      return;
    }
    subset.push(candidates[idx]);
    backtrack(idx);
    subset.pop();
    backtrack(idx + 1);
  }

  backtrack(0);

  return res;
};
```
