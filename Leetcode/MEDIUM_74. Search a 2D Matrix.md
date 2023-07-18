# 74. Search a 2D Matrix

#이진탐색

## 풀이 복기

첫번째 풀이에서 flat을 사용했기때문에 `O(m*n)` 시간복잡도를 갖는다. 문제 조건인 `O(log(m*n))` 를 통과해야하므로 첫번째는 틀렸다.
두번째는 입력받은 배열을 그대로 사용해서 풀었다. 이때 나누기를 잘못하는 바람에 AC가 늦어짐. 계산 똑바로하자

### 풀이 1

```js
/**
 * m: matrix.length, n: matrix[0].length;
 * 시간복잡도: O(m*n)
 * 공간복잡도: O(m*n)
 */
var searchMatrix = function (matrix, target) {
  const nums = matrix.flat();
  let head = 0;
  let tail = nums.length - 1;

  while (head <= tail) {
    const mid = Math.floor((head + tail) / 2);
    const currentNum = nums.at(mid);

    if (currentNum === target) {
      return true;
    } else if (currentNum < target) {
      head = mid + 1;
    } else {
      tail = mid - 1;
    }
  }

  return false;
};
```

### 풀이 2

```js
/**
 * AC
 * m: matrix.length, n: matrix[0].length;
 * 시간복잡도: O(log(m*n))
 * 공간복잡도: O(1)
 */
var searchMatrix = function (matrix, target) {
  const m = matrix.length;
  const n = matrix[0].length;
  let head = 0;
  let tail = m * n - 1;

  while (head <= tail) {
    const mid = Math.floor((head + tail) / 2);
    const midNum = matrix[Math.floor(mid / n)][mid % n];

    if (midNum === target) {
      return true;
    } else if (midNum < target) {
      head = mid + 1;
    } else {
      tail = mid - 1;
    }
  }

  return false;
};
```
