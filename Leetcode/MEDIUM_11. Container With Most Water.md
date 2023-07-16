# 11. Container With Most Water

#투포인터

## 풀이 복기

height의 범위가 `2 <= n <= 10^5`이므로 O(n^2) 방법인 브루트포스는 사용하지 못한다.
O(n) 시간복잡도를 갖는 투포인터를 사용해서 문제를 풀었다.

정렬된 배열에서만 투포인터를 사용하는것은 아니다. 이런 넓이를 구할때도 투포인터 가능

### 풀이 1

```js
/**
 * n: height.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(1)
 */
var maxArea = function (height) {
  let head = 0;
  let tail = height.length - 1;
  let max = 0;

  while (head < tail) {
    const minH = Math.min(height.at(head), height.at(tail));
    max = Math.max(minH * (tail - head), max);

    if (height.at(head) <= height.at(tail)) {
      head += 1;
    } else if (height.at(head) > height.at(tail)) {
      tail -= 1;
    }
  }

  return max;
};
```
