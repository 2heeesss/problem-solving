# 739. Daily Temperatures

#stack

## 풀이 복기

풀이 1 - 시간초과
2중으로 순회하며 가장 기본적인 브루트포스를 사용해서 문제를 풀었다. 하지만 입력 배열의 크기가 `1 <= temperatures.length <= 10^5`이므로 시간초과가 발생해서 통과하지 못했다.

2번 풀이는 stack을사용해 시간복잡도를 O(n)으로 줄여서 통과할수있었다.

문제 입력 크기를 보고 어떤 시간복잡도를 가진 알고리즘을 떠올려야하는지 연습하는 과정이 필요할것같다.

### 풀이 1

```js
/**
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(n)
 */
const dailyTemperatures = function (temperatures) {
  return temperatures.map((temperature, idx, arr) => {
    return arr.slice(idx + 1).findIndex(nextTemperature => nextTemperature > temperature) + 1;
  });
};
```

### 풀이 2

```js
/**
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
const dailyTemperatures = function (temperatures) {
  const res = new Array(temperatures.length).fill(0);
  const indexStack = [];
  temperatures.forEach((temperature, idx) => {
    while (indexStack.length > 0 && temperatures[indexStack[indexStack.length - 1]] < temperature) {
      res[indexStack[indexStack.length - 1]] = idx - indexStack[indexStack.length - 1];
      indexStack.pop();
    }
    indexStack.push(idx);
  });
  return res;
};
```
