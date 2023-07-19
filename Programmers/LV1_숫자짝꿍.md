# 숫자 짝꿍

#해쉬맵

## 풀이 복기

배열 생성할때 인덱스를 9까지 만들어서 여러번 틀렸다. 실수도 실력인데

### 풀이 1

```js
/**
 * n: X.length, m: Y.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
function solution(X, Y) {
  const numMap = new Array(10)
    .fill(0)
    .map((_, idx) => idx)
    .reduce((acc, cur) => {
      acc.set(cur.toString(), 0);
      return acc;
    }, new Map());
  const numCnt = new Array(10).fill(0);

  for (const n of X) {
    numMap.set(n, numMap.get(n) + 1);
  }

  for (const n of Y) {
    if (numMap.get(n) > 0) {
      numMap.set(n, numMap.get(n) - 1);
      numCnt[n] += 1;
    }
  }

  const str = numCnt.reduce((acc, cur, idx) => {
    return idx.toString().repeat(cur) + acc;
  }, '');

  return str ? (str[0] === '0' ? '0' : str) : '-1';
}
```
