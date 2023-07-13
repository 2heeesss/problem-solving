# 167. Two Sum II - Input Array Is Sorted

#투포인터

## 풀이 복기

입력 크기의 조건은 다음과 같다.`2 <= numbers.length <= 3 * 10^4` 이를 만족하기 위해서는 O(n^2)보다 작은 알고리즘을 사용해야했다.
첫 풀이는 일단 동작하게 만드는 용으로 통과하지 못할것은 알았지만 일단 풀었다.

두번째 풀이는 O(n) 시간복잡도를 갖기때문에 통과했다.

### 풀이 1

```js
/**
 * 시간초과
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(1)
 */
var twoSum = function (numbers, target) {
  for (let i = 0; i < numbers.length; i++) {
    for (let j = i + 1; j < numbers.length; j++) {
      if (numbers[i] + numbers[j] === target) return [i + 1, j + 1];
    }
  }
};
```

### 풀이 2

```js
/**
 * AC
 * 시간복잡도: O(n)
 * 공간복잡도: O(1)
 */
var twoSum = function (numbers, target) {
  let [head, tail] = [0, numbers.length - 1];

  while (head < tail) {
    if (numbers[head] + numbers[tail] == target) {
      return [head + 1, tail + 1];
    } else if (numbers[head] + numbers[tail] > target) {
      tail -= 1;
    } else {
      head += 1;
    }
  }
};
```
