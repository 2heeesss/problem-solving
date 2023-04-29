# 배열의 길이에 따라 다른 연산하기

#배열

### 풀이 1

```js
function solution(arr, n) {
  const isEvenLength = arr.length % 2 === 0;
  return arr.map((num, idx) => {
    if (isEvenLength) {
      return idx % 2 === 0 ? num : num + n;
    } else {
      return idx % 2 === 0 ? num + n : num;
    }
  });
}
```
