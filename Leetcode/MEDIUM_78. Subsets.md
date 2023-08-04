# 78. Subsets

#백트래킹

## 풀이 복기

풀이 1은 기본적인 dfs 방식으로 풀었고, 풀이 2는 백트래킹 방식으로 풀었다. dfs가 익숙하지만 백트래킹은 아직 익숙하지 않다. 연습이 필요함.

### 풀이 1

```js
/**
 * AC
 * n: nums.length
 * 시간복잡도: O(2^n)
 * 공간복잡도: O(2^n)
 */
var subsets = function (nums) {
  const set = new Set();

  var dfs = function (nums) {
    if (nums.length < 2) {
      return [nums];
    }

    const subSets = [nums];
    for (let i = 0; i < nums.length; i++) {
      const subNums = [...nums.slice(0, i), ...nums.slice(i + 1, nums.length)];
      if (!set.has(subNums.join())) {
        subSets.push(subNums);
        set.add(subNums.join());
        subSets.push(...dfs(subNums));
      }
    }

    return subSets;
  };

  const subSets = dfs(nums);
  subSets.push([]);
  const set2 = new Set();
  return subSets.filter(subSetNums => {
    const str = subSetNums.join();
    if (!set2.has(str)) {
      set2.add(str);
      return true;
    }
    return false;
  });
};
```

### 풀이 2

```js
/**
 * AC
 * n: nums.length
 * 시간복잡도: O(2^n)
 * 공간복잡도: O(2^n)
 */
var subsets = function (nums) {
  const res = [];
  const subset = [];

  function backtrack(idx) {
    if (nums.length <= idx) {
      res.push([...subset]);
      return;
    }
    subset.push(nums[idx]);
    backtrack(idx + 1);
    subset.pop();
    backtrack(idx + 1);
  }

  backtrack(0);
  return res;
};
```
