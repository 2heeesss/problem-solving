# 기사단원의 무기

#브루트포스

## 풀이 복기

첫번째 방법은 시간초과로 틀렸다. 입력의 조건은 `1 <= number <= 10^5` 이므로 O(n^2)의 알고리즘을 사용하면 안된다.

약수를 찾을때 n까지 전부 순회할 필요는 없다. √n까지만 순회하면 약수를 전부 찾을 수 있다. 이 방법을 사용했을때 O(n√n)시간복잡도를 갖기 때문에 통과할수 있었다.

### 풀이 1

```js
/**
 * Fail
 * n: number
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(n)
 */
function solution(number, limit, power) {
  return new Array(number)
    .fill(0)
    .map((_, idx) => {
      const n = idx + 1;
      let divisor = 0;
      for (let i = 1; i <= n; i++) {
        if (n % i === 0) {
          divisor += 1;
        }
      }
      return divisor;
    })
    .reduce((acc, cur) => (cur > limit ? acc + power : acc + cur), 0);
}
```

### 풀이 2

```js
/**
 * AC
 * n: number
 * 시간복잡도: O(n√n)
 * 공간복잡도: O(n)
 */
function solution(number, limit, power) {
  return new Array(number)
    .fill(0)
    .map((_, idx) => {
      const n = idx + 1;
      let divisor = 0;
      for (let i = 1; i < Math.sqrt(n); i++) {
        if (n % i === 0) {
          divisor += 2;
        }
      }
      const p = n % Math.sqrt(n) === 0 ? 1 : 0;
      return divisor + p;
    })
    .reduce((acc, cur) => (cur > limit ? acc + power : acc + cur), 0);
}
```
