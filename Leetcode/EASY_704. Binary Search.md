# 704. Binary Search

#이진탐색

## 풀이 복기

가장 기본적인 이진탐색 문제.
이진탐색의 선행조건은 정렬이되어있는 배열이다 기억하자.
정렬에 소요되는 시간복잡도는 O(nlogn) 이므로 정렬을 하고 이진탐색을 할건지도 생각해야한다.

### 풀이 1

```js
/**
 * n: nums.length
 * 시간복잡도: O(logn)
 * 공간복잡도: O(1)
 */
var search = function (nums, target) {
  let head = 0;
  let tail = nums.length - 1;

  while (head <= tail) {
    const mid = Math.floor((head + tail) / 2);
    const currentNum = nums.at(mid);

    if (currentNum === target) {
      return mid;
    } else if (currentNum < target) {
      head = mid + 1;
    } else {
      tail = mid - 1;
    }
  }

  return -1;
};
```

### 풀이 2

```js
/**
 * n: nums.length
 * 시간복잡도: O(logn)
 * 공간복잡도: O(1)
 */
const binarySearch = (nums, target, head, tail) => {
  if (head > tail) {
    return -1;
  }
  const mid = Math.floor((head + tail) / 2);
  const currentNum = nums.at(mid);

  if (currentNum === target) {
    return mid;
  } else if (currentNum < target) {
    return binarySearch(nums, target, mid + 1, tail);
  } else {
    return binarySearch(nums, target, head, mid - 1);
  }
};

var search = function (nums, target) {
  return binarySearch(nums, target, 0, nums.length - 1);
};
```
