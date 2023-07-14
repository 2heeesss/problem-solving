# 과일 장수

#배열#정렬

### 풀이 1

```js
/**
 * n: scores.length, m:m
 * 시간복잡도: O(nlogn)
 * 공간복잡도: O(n)
 */
function solution(k, m, score) {
  const ans = [];
  score
    .sort((a, b) => b - a)
    .forEach((s, idx) => {
      if (idx !== 0 && (idx + 1) % m === 0) {
        ans.push(s * m);
      }
    });
  return ans.reduce((acc, cur) => acc + cur, 0);
}
```

### 풀이 2

```js
/**
 * n: scores.length, m:m
 * 시간복잡도: O(nlogn)
 * 공간복잡도: O(n)
 */
function solution(k, m, score) {
  return score
    .sort((a, b) => b - a)
    .filter((s, idx) => (idx + 1) % m === 0)
    .reduce((acc, cur) => acc + cur * m, 0);
}
```
