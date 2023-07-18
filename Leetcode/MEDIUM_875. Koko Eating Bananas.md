# 875. Koko Eating Bananas

#이진탐색

## 풀이 복기

이진탐색은 정렬된 배열에 적용해야한다. 만약 O(logn) 시간복잡도를 가져야하는데 정렬된 배열이 없다면, 시간 또는 인덱스로 이진탐색을 진행할 수 있다.
이 문제의 경우 1~max 사이의 인덱스로 이진탐색을 진행했다.

습관적으로 Math.floor를 적용한다. 이 문제의 경우 올림 하면 되는거라 Math.ceil로 바로 하면되는건데

### 풀이 1

```js
/**
 * AC
 * n: piles, m: max(piles)
 * 시간복잡도: O(nlog(m))
 * 공간복잡도: O(n)
 */
const getEatHour = function (k, piles) {
  return piles.reduce((hours, pile) => hours + Math.floor(pile / k) + (pile % k === 0 ? 0 : 1), 0);
};

const minEatingSpeed = function (piles, h) {
  let head = 1;
  let tail = Math.max(...piles);
  let minK = Infinity;

  while (head <= tail) {
    const k = Math.floor((head + tail) / 2);
    const eatHour = getEatHour(k, piles);

    if (eatHour <= h) {
      minK = Math.min(k, minK);
      tail = k - 1;
    } else {
      head = k + 1;
    }
  }

  return minK;
};
```

### 풀이 2

```js
/**
 * AC
 * n: piles, m: max(piles)
 * 시간복잡도: O(nlog(m))
 * 공간복잡도: O(n)
 */
const getEatHour = function (k, piles) {
  return piles.reduce((hours, pile) => hours + Math.ceil(pile / k));
};

const minEatingSpeed = function (piles, h) {
  let head = 1;
  let tail = Math.max(...piles);
  let minK = Infinity;

  while (head <= tail) {
    const k = Math.floor((head + tail) / 2);
    const eatHour = getEatHour(k, piles);

    if (eatHour <= h) {
      minK = Math.min(k, minK);
      tail = k - 1;
    } else {
      head = k + 1;
    }
  }

  return minK;
};
```
