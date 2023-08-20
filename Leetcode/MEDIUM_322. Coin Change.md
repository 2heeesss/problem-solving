# 322. Coin Change

#DP

## 풀이 복기

dp 문제를 풀때 배열을 0으로 습관적 초기화를 한다. min 또는 max에 따라서 필요에 따라 초기값을 다르게 해야하는데 생각하고 초기화를 하자.
dp는 점화식만 잘쓰자

### 풀이 1

```js
/**
 * AC
 * n: amount
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var coinChange = function (coins, amount) {
  if (amount === 0) return 0;
  const dp = new Array(amount + 1).fill(Infinity);

  for (const coin of coins) {
    if (coin <= dp.length) {
      dp[coin] = 1;
    }
  }

  for (let i = 0; i < dp.length; i++) {
    const coinIdxes = [];
    for (const coin of coins) {
      const prevCoinIdx = i - coin;
      if (0 < prevCoinIdx && prevCoinIdx <= dp.length) {
        coinIdxes.push(dp[prevCoinIdx] + 1);
      }
    }

    dp[i] = Math.min(...coinIdxes, dp[i]);
  }

  console.log(dp);
  return dp.at(amount) === Infinity ? -1 : dp.at(amount);
};
```

### 풀이 2

```js

```
