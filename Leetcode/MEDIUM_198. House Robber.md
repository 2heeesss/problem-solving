# 198. House Robber

#DP

### 풀이 1

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var rob = function (nums) {
  const dp = new Array(nums.length).fill(null);

  for (let i = 0; i < dp.length; i++) {
    if (i < 2) {
      dp[i] = nums[i];
    } else if (i === 2) {
      dp[i] = nums[i] + nums[i - 2];
    } else {
      dp[i] = Math.max(dp[i - 2], dp[i - 3]) + nums[i];
    }
  }

  return Math.max(dp.at(-1), dp.at(-2) || 0);
};
```
