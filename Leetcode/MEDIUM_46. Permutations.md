# 46. Permutations

#백트래킹

## 풀이 복기

1번풀이 dfs로 풀때 종료 조건을 리턴하며 배열로 한번 더 감싸야하는지, 아니면 그냥 리턴할지 헷갈렸다. 헷갈릴때는 실제로 그려보면서 아니면 디버깅툴을 사용하면서 이해하자.

### 풀이 1

```js
/**
 * AC
 * n: nums.length
 * 시간복잡도: O(n!)
 * 공간복잡도: O(n!)
 */
var permute = function (nums) {
  return dfs(nums);
};

var dfs = function (arr) {
  if (arr.length <= 1) {
    return arr;
  }
  const path = [];
  for (let i = 0; i < arr.length; i++) {
    const fixNum = arr[i];
    const restArr = [...arr.slice(0, i), ...arr.slice(i + 1, arr.length)];
    for (const num of dfs(restArr)) {
      path.push([fixNum, num]);
    }
  }
  return path;
};
```

### 풀이 2

```js
/**
 * AC
 * n: nums.length
 * 시간복잡도: O(n!)
 * 공간복잡도: O(n!)
 */
var permute = function (nums) {
  const res = [];
  const path = [];
  const visited = new Array(nums.length).fill(false);

  function backtrack(idx) {
    if (path.length === nums.length) {
      res.push([...path]);
      return;
    }
    for (let i = 0; i < nums.length; i++) {
      if (visited[i]) {
        continue;
      }
      visited[i] = true;
      path.push(nums[i]);
      backtrack(i);

      visited[i] = false;
      path.pop();
    }
  }

  backtrack(0);
  return res;
};
```
