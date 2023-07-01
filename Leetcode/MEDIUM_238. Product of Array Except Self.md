# 238. Product of Array Except Self

#배열

## 풀이 복기

처음에 나눗셈을 사용해서 푸는 방법밖에 떠올리지 못했다.
나눗셈을 쓸때도 주의할점은 0 이다.
0이 2개 이상 있다면, 0으로만 만들어진 배열을 리턴하면 된다.
0이 한개 있다면, 요소가 0인 시점에 나머지 요소를 곱한 값을 넣은 배열을 리턴하면 된다.

하지만 문제 요구사항에 나누기 연산을 사용하지 마라고 나와있어서 다른 방법을 사용해야했다.

두번째 풀이는 앞쪽부터 차례대로 곱한 값을 저장하는 head, 뒷쪽부터 차례대로 곱한 값을 저장하는 tail을 가지고 문제를 풀 수 있었다.

### 풀이 1

```js
const productExceptSelf = function (nums) {
  const head = [...nums];
  const tail = [...nums];

  for (let i = 1; i < nums.length; i++) {
    head[i] = head[i - 1] * head[i];
  }

  for (let i = nums.length - 2; i >= 0; i--) {
    tail[i] = tail[i + 1] * tail[i];
  }

  const res = [];
  for (let i = 0; i < nums.length; i++) {
    const ascNum = i - 1 < 0 ? 1 : head[i - 1];
    const descNum = i + 1 > nums.length - 1 ? 1 : tail[i + 1];
    res.push(ascNum * descNum);
  }

  return res;
};
```
