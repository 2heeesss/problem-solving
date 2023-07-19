# 153. Find Minimum in Rotated Sorted Array

#이진탐색

## 풀이 복기

문제 조건은 시간복잡도 O(logN)이다. 이는 이진탐색을 사용했을때 가능한 시간복잡도.

다만 일반적인 정렬된 배열에서 사용하는것이 아니라, `정렬된 배열 + K번 움직임 배열`이다. 때문에 head를 옮길지 tail을 옮길지 결정하는 조건이 중요하다.

아래는 `정렬된 배열 + K번움직임 배열` 에서 나올 수 있는 경우들을 작성한것이다. `mid value < tail value` 일때 `tail = mid - 1`을 해주면 조건에 만족하는것을 확인할 수 있다.

첫번째 풀이에서는 이런 규칙을 발견하지 못해서 fail이 발생함.

```
 1 2 3 4 5 -> headV < midV < tailV -> tail = mid - 1
 5 1 2 3 4 -> headV > midV < tailV -> tail = mid - 1
 4 5 1 2 3 -> headV > midV < tailV -> tail = mid - 1

 3 4 5 1 2 -> headV < midV > tailV -> head = mid + 1
 2 3 4 5 1 -> headV < midV > tailV -> head = mid + 1

 1 100 -> headV <= midV < tailV -> tail = mid - 1
 100 1 -> headV <= midV > tailV -> head = mid + 1
```

### 풀이 1

```js
/**
 * Fail
 * n: nums.length
 * 시간복잡도: O(logn)
 * 공간복잡도: O(1)
 */
var findMin = function (nums) {
  if (nums.length === 1) {
    return nums.at(0);
  }
  let head = 0;
  let tail = nums.length - 1;

  while (head <= tail) {
    const mid = Math.floor((head + tail) / 2);
    const midNum = nums.at(mid);

    if (nums.at(mid - 1) > midNum) {
      return midNum;
    } else if (nums.at(head) < nums.at(tail)) {
      tail = mid - 1;
    } else {
      head = mid + 1;
    }
  }
};
```

### 풀이 2

```js
/**
 * AC
 * n: nums.length
 * 시간복잡도: O(logn)
 * 공간복잡도: O(1)
 */
var findMin = function (nums) {
  if (nums.length === 1) {
    return nums.at(0);
  }
  let head = 0;
  let tail = nums.length - 1;

  while (head <= tail) {
    const mid = Math.floor((head + tail) / 2);
    const midNum = nums.at(mid);
    if (nums.at(mid - 1) > midNum) {
      return midNum;
    } else if (nums.at(mid) > nums.at(tail)) {
      head = mid + 1;
    } else {
      tail = mid - 1;
    }
  }
};
```
