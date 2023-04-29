# 크기가 작은 부분 문자열

#문자열

## 풀이 복기

문자열을 자르는 문제였는데 slice메서드가 생각나지 않아서 for문으로 해결하려고 했었다. 자주 사용되는 메서드는 꼭 기억해야함.

### 풀이 1

```js
function solution(t, p) {
  return [...t].filter((_, idx) => {
    const sliceString = t.slice(idx, idx + p.length);
    if (sliceString.length < p.length) {
      return false;
    }
    return Number(sliceString) <= Number(p);
  }).length;
}
```
