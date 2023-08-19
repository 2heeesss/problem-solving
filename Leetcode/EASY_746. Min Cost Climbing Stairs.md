# 746. Min Cost Climbing Stairs

#DP

### 풀이 1

```js
/**
 * AC
 * n: cost.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var minCostClimbingStairs = function (cost) {
  const dp = new Array(cost.length).fill(-1);
  dp[0] = cost[0];
  dp[1] = cost[1];

  for (let i = 2; i < dp.length; i++) {
    dp[i] = Math.min(dp[i - 1], dp[i - 2]) + cost[i];
  }

  return Math.min(dp.at(-1), dp.at(-2));
};
```
