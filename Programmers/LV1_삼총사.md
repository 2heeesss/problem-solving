# 삼총사

#배열

## 풀이 복기

입력값의 범위를 먼저 확인하자. number의 최대 길이는 13이므로 시간복잡도 O(n^3)은 n의 크기가 500 이하일때 1초안에 연산을 끝낼 수 있으므로 3중 for문이 시간안에 풀어질 수 있을것이라는 생각을 먼저 하게되었음.

### 풀이 1

```js
function solution(number) {
  let cnt = 0;

  for (let i = 0; i < number.length; i++) {
    for (let j = i + 1; j < number.length; j++) {
      for (let k = j + 1; k < number.length; k++) {
        if (number[i] + number[j] + number[k] === 0) {
          cnt += 1;
        }
      }
    }
  }

  return cnt;
}
```

### 풀이 2

```js

```
