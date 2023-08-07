# 90. Subsets II

#백트래킹

### 풀이 1

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsetsWithDup = function (nums) {
  const res = [];
  const path = [];
  const set = new Set();

  function backtrack(idx) {
    if (idx >= nums.length) {
      const copyPath = [...path];
      copyPath.sort((a, b) => b - a);
      if (set.has(copyPath.join())) {
        return;
      }
      set.add(copyPath.join());
      res.push(copyPath);
      return;
    }

    path.push(nums[idx]);
    backtrack(idx + 1);
    path.pop();
    backtrack(idx + 1);
  }

  backtrack(0);
  return res;
};
```

### 풀이 2

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsetsWithDup = function (nums) {
  const res = [];
  const path = [];
  const set = new Set();
  nums.sort((a, b) => b - a);

  function backtrack(idx) {
    if (idx >= nums.length) {
      const copyPath = [...path];
      if (set.has(copyPath.join())) {
        return;
      }
      set.add(copyPath.join());
      res.push(copyPath);
      return;
    }

    path.push(nums[idx]);
    backtrack(idx + 1);
    path.pop();
    backtrack(idx + 1);
  }

  backtrack(0);
  return res;
};
```

### 풀이 3

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsetsWithDup = function (nums) {
  const res = [];
  const path = [];
  nums.sort((a, b) => b - a);

  function backtrack(idx, prevIncluded) {
    if (idx >= nums.length) {
      const copyPath = [...path];
      res.push(copyPath);
      return;
    }
    if (idx > 0 && nums[idx] === nums[idx - 1] && !prevIncluded) {
      backtrack(idx + 1, false);
      return;
    }

    path.push(nums[idx]);
    backtrack(idx + 1, true);
    path.pop();
    backtrack(idx + 1, false);
  }

  backtrack(0);
  return res;
};
```
