# 70. Climbing Stairs

#DP

## 풀이 복기

DP는 점화식 잘 세우고, 이미 계산된 값은 저장된 배열에서 가져다쓰면 된다.

### 풀이 1

```js
/**
 * AC
 * n: n
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var climbStairs = function (n) {
  const dp = new Array(n + 1).fill(0);
  dp[1] = 1;
  dp[2] = 2;

  for (let i = 3; i < dp.length; i++) {
    dp[i] = dp[i - 1] + dp[i - 2];
  }

  return dp.at(n);
};
```

### 풀이 2

```js
/**
 * AC
 * n: n
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var climbStairs = function (n) {
  // dp[i] = dp[i-1] + dp[i-2]
  const dp = new Array(n + 1).fill(0);
  dp[1] = 1;
  dp[2] = 2;

  function rec(i) {
    if (dp[i] !== 0) {
      return dp[i];
    }
    dp[i] = rec(i - 1) + rec(i - 2);

    return dp[i];
  }

  return rec(n);
};
```
