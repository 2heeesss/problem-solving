# 소수찾기

#수학

## 풀이 복기

소수찾기 알고리즘에서 중요한건 아래 두가지 방법이다.

1. 에라토스테네스의 체 알고리즘
2. i ~ Math.sqrt(i) 까지 탐색하기

둘중 하나라도 사용하지 않는다면 시간초과가 발생하는 문제였다. 첫번째풀이에서 Math.sqrt(i)까지 탐색을 안하고 max까지 탐색하는 바람에 시간초과 발생했다.

### 풀이 1

```js
/**
 * Fail
 * n: n
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(n)
 */
function solution(n) {
  const primaryNums = new Array(n + 1).fill(true);
  primaryNums[0] = false;
  primaryNums[1] = false;

  for (let i = 2; i < primaryNums.length; i++) {
    if (!primaryNums[i]) {
      continue;
    }

    if (isPrimary(i)) {
      primaryNums[i] = true;
      let idx = i * 2;

      while (idx < primaryNums.length) {
        primaryNums[idx] = false;
        idx += i;
      }
    }
  }

  return primaryNums.filter(primaryNum => primaryNum).length;
}

function isPrimary(num) {
  for (let i = 2; i < num; i++) {
    if (num % i === 0) {
      return false;
    }
  }

  return true;
}
```

### 풀이 2

```js
/**
 * Fail
 * n: n
 * 시간복잡도: O(n√n)
 * 공간복잡도: O(n)
 */
function solution(n) {
  const primaryNums = new Array(n + 1).fill(true);
  primaryNums[0] = false;
  primaryNums[1] = false;

  for (let i = 2; i < primaryNums.length; i++) {
    if (!primaryNums[i]) {
      continue;
    }

    if (isPrimary(i)) {
      primaryNums[i] = true;
      let idx = i * 2;

      while (idx < primaryNums.length) {
        primaryNums[idx] = false;
        idx += i;
      }
    }
  }

  return primaryNums.filter(primaryNum => primaryNum).length;
}

function isPrimary(num) {
  for (let i = 2; i <= Math.sqrt(num); i++) {
    if (num % i === 0) {
      return false;
    }
  }

  return true;
}
```
