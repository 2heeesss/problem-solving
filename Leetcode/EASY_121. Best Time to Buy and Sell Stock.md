# 121. Best Time to Buy and Sell Stock

#슬라이딩윈도우#투포인터

## 풀이 복기

한번에 최적의 풀이방법이 생각 안날때는 일단 브루트포스로 해결하고 생각하자.

### 풀이 1

```js
/**
 * 시간초과
 * n: prices.length
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(1)
 */
var maxProfit = function (prices) {
  let maxProfit = 0;

  for (let i = 0; i < prices.length; i++) {
    for (let j = i + 1; j < prices.length; j++) {
      if (prices.at(i) < prices.at(j)) {
        maxProfit = Math.max(maxProfit, prices.at(j) - prices.at(i));
      }
    }
  }

  return maxProfit;
};
```

### 풀이 2

```js
/**
 * AC
 * n: prices.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(1)
 */
var maxProfit = function (prices) {
  let minPrice = Infinity;
  let maxProfit = 0;

  for (let i = 0; i < prices.length; i++) {
    if (prices.at(i) < minPrice) {
      minPrice = prices.at(i);
    } else {
      maxProfit = Math.max(maxProfit, prices.at(i) - minPrice);
    }
  }

  return maxProfit;
};
```
