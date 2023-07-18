# 덧칠하기

#부르트포스

## 풀이 복기

풀이 1에서 중첩된 분기문은 사실 필요 없었다. 어짜피 똑같이 계산되므로 없애자.
전형적인 부르트포스 문제인듯. 1부터 시작하는것만 인지하면 실수하지 않을듯하다

### 풀이 1

```js
/**
 * k: section.length
 * 시간복잡도: O(k)
 * 공간복잡도: O(1)
 */
function solution(n, m, section) {
  let max = 0;
  let res = 0;
  const limit = n + 1 - m;

  for (let i = 0; i < section.length; i++) {
    if (section.at(i) > max) {
      if (section.at(i) > limit) {
        res += 1;
        break;
      }
      res += 1;
      max = section.at(i) + m - 1;
    }
  }

  return res;
}
```

### 풀이 2

```js
/**
 * k: section.length
 * 시간복잡도: O(k)
 * 공간복잡도: O(1)
 */
function solution(n, m, section) {
  let max = 0;
  let res = 0;
  const limit = n + 1 - m;

  for (let i = 0; i < section.length; i++) {
    if (section.at(i) > max) {
      res += 1;
      max = section.at(i) + m - 1;
    }
  }

  return res;
}
```
