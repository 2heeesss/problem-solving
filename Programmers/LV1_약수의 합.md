# 약수의 합

#수학

### 풀이 1

```js
function solution(n) {
  const set = new Set();
  for (let i = 1; i <= n; i++) {
    if (n % i === 0) {
      set.add(i);
    }
  }

  return [...set.keys()].reduce((sum, num) => num + sum, 0);
}
```
