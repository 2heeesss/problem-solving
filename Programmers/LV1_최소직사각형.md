# 최소직사각형

#완전탐색

### 풀이 1

```js
function solution(sizes) {
  const sortedSizes = sizes.map(size => size.sort((a, b) => a - b));
  const minW = Math.max(...sortedSizes.map(size => size[0]));
  const minH = Math.max(...sortedSizes.map(size => size[1]));

  return minW * minH;
}
```
