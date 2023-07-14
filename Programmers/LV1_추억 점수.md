# 추억 점수

#배열

## 풀이 복기

or 를 사용하면 3항연산자 사용하지 않아도 되었을텐데

### 풀이 1

```js
/**
 * 시간복잡도: O(n*m)
 * 공간복잡도: O(n)
 */
function solution(names, yearning, photo) {
  const yearningMap = names.reduce((map, name, idx) => map.set(name, yearning[idx]), new Map());

  return photo.map(photoMans => photoMans.reduce((acc, cur) => (yearningMap.has(cur) ? acc + yearningMap.get(cur) : acc), 0));
}
```

### 풀이 2

```js

```
