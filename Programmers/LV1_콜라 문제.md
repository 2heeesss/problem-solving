# 콜라 문제

#재귀

## 풀이 복기

문제를 풀면서 배운점이나 놓친점을 작성합니다.

### 풀이 1

```js
function solution(a, b, n) {
  const getCoke = (martWant, bonusCoke, currentCokeCnt) => {
    if (currentCokeCnt < martWant) return 0;

    const plusCoke = Math.floor(currentCokeCnt / martWant) * bonusCoke;
    const nextCokeCnt = plusCoke + (currentCokeCnt % martWant);

    return getCoke(martWant, bonusCoke, nextCokeCnt) + plusCoke;
  };

  return getCoke(a, b, n);
}
```
