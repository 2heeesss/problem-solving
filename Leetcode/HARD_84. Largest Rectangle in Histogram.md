# 84. Largest Rectangle in Histogram

#스택

## 풀이 복기

입력의 크기 `1 <= heights.length <= 10^5`를 보고 O(n^2)이상의 알고리즘은 사용하면 안된다는것을 알았다. 하지만 다른 방법이 생각나지 않아서 일단 O(n^2)이 소요되는 풀이방법으로 작성했다.

첫번째 풀이와 두번째 풀이는 거의 동일하고 결과를 리턴하는 방법만 다를 뿐이다. 다만 첫 방법을 사용했을때 메모리 제한을 초과했기때문에 두번째 (추가 배열 공간을 사용하지않는)방법으로 풀었다. 두번째 풀이는 시간초과가 발생했다.

세번째 풀이는 stack을 활용한 O(n) 시간복잡도를 갖는 알고리즘으로 풀었다. 높이가 증가할때는 계산하지 않고, 높이가 감소하는 순간 stack에 쌓여있는 정렬된 높이를 가지고 넓이를 계산하는 방식이다.

### 풀이 1

```js
/**
 * 메모리초과
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(n^2)
 */
var largestRectangleArea = function (heights) {
  const stack = [];
  const heightSet = new Set(heights);
  for (const h of heightSet) {
    let rec = 0;
    for (const height of heights) {
      if (height - h >= 0) {
        rec += h;
      } else {
        stack.push(rec);
        rec = 0;
      }
    }
    stack.push(rec);
  }

  return Math.max(...stack);
};
```

### 풀이 2

```js
/**
 * 시간초과
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(n)
 */
var largestRectangleArea = function (heights) {
  let max = 0;
  const heightSet = new Set(heights);
  for (const h of heightSet) {
    let rec = 0;
    for (const height of heights) {
      if (height - h >= 0) {
        rec += h;
      } else {
        max = Math.max(rec, max);
        rec = 0;
      }
    }
    max = Math.max(rec, max);
  }

  return max;
};
```

### 풀이 3

```js
/**
 * AC
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var largestRectangleArea = function (heights) {
  heights.push(0);
  const stack = [];
  let maxRec = 0;

  const getLastHeight = () => {
    return stack[stack.length - 1].h;
  };

  heights.forEach((height, idx) => {
    let po = idx;
    while (stack.length && getLastHeight() > height) {
      const { h, position } = stack.pop();
      const rec = (idx - position) * h;
      maxRec = Math.max(maxRec, rec);
      po = position;
    }
    stack.push({ h: height, position: po });
  });

  return maxRec;
};
```
