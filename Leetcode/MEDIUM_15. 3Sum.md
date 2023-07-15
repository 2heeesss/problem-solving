# 15. 3Sum

#투포인터

## 풀이 복기

입력값의 범위가 `3 <= nums.length <= 3000` 이므로 O(n^3)의 시간복잡도를 갖는 알고리즘은 사용하면 안된다.

따라서 O(n^2)이하의 시간복잡도를 갖도록 구현해야한다. 첫번째 풀이는 구현이 잘못되었다. 해당 풀이는 숫자가 1의자리수만 가질때만 통과한다(-를 붙이는 과정에서)
이 문제를 고치기위해 풀이2 로 고쳤는데, 위에서 발생한 에러는 잡았지만 시간초과가 발생했다. O(n^2) 알고리즘이라 시간초과가 안날것을 예상했었다.

최적화를 진행해야했다. 풀이 3에서는 각 forEach 문 마다 head 포인터의 위치를 0 에서 idx + 1로 변경시켰다. 이 부분이 가장 큰 역할을 했을것으로 판단된다. 또한, set을 사용하지 않기 위해 중복되는것을 반복문 안에서 처리했다.

### 풀이 1

```js
/**
 * Fail
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(n)
 */
var threeSum = function (nums) {
  nums.sort((a, b) => a - b);
  const set = new Set();

  nums.forEach((num, idx) => {
    let head = 0;
    let tail = nums.length - 1;
    while (head < tail) {
      if (tail === idx) {
        tail -= 1;
        continue;
      }
      if (head === idx) {
        head += 1;
        continue;
      }

      if (nums.at(head) + nums.at(tail) === -num) {
        const sortedSubSet = [nums.at(head), num, nums.at(tail)].sort((a, b) => a - b);
        set.add(sortedSubSet.join(''));
        tail -= 1;
      } else if (nums.at(head) + nums.at(tail) < -num) {
        head += 1;
      } else {
        tail -= 1;
      }
    }
  });

  return [...set.keys()].map(key => {
    let b = 1;
    const ch = [];
    [...key].forEach(char => {
      if (char === '-') {
        b = -1;
      } else {
        ch.push(char * b);
        b = 1;
      }
    });

    return ch;
  });
};
```

### 풀이 2

```js
/**
 * 시간초과
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(n)
 */
var threeSum = function (nums) {
  nums.sort((a, b) => a - b);
  const set = new Set();

  nums.forEach((num, idx) => {
    let head = 0;
    let tail = nums.length - 1;
    while (head < tail) {
      if (tail === idx) {
        tail -= 1;
        continue;
      }
      if (head === idx) {
        head += 1;
        continue;
      }

      if (nums.at(head) + nums.at(tail) === -num) {
        const sortedSubSet = [nums.at(head), num, nums.at(tail)].sort((a, b) => a - b);
        set.add(sortedSubSet.join(','));
        tail -= 1;
      } else if (nums.at(head) + nums.at(tail) < -num) {
        head += 1;
      } else {
        tail -= 1;
      }
    }
  });

  return [...set.keys()].map(key => {
    return key.split(',').map(n => Number(n));
  });
};
```

### 풀이 3

```js
/**
 * AC
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(n)
 */
var threeSum = function (nums) {
  nums.sort((a, b) => a - b);
  const res = [];

  nums.forEach((num, idx) => {
    if (idx > 0 && nums[idx] === nums[idx - 1]) {
      return;
    }
    let head = idx + 1;
    let tail = nums.length - 1;
    while (head < tail) {
      let sum = nums.at(idx) + nums.at(head) + nums.at(tail);

      if (sum === 0) {
        res.push([nums.at(idx), nums.at(head), nums.at(tail)]);

        while (nums.at(head) === nums.at(head + 1)) head += 1;
        while (nums.at(tail) === nums.at(tail - 1)) tail -= 1;
        head += 1;
        tail -= 1;
      } else if (sum < 0) {
        head += 1;
      } else {
        tail -= 1;
      }
    }
  });

  return res;
};
```
