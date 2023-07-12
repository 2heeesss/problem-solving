# 푸트 파이트 대회

#배열#문자열

### 풀이 1

```js
function solution(food) {
  const halfFoodLine = food.reduce((acc, cur, idx) => {
    if (idx === 0) return acc;

    const curStr = idx.toString().repeat(Math.floor(cur / 2));
    acc.push(curStr);

    return acc;
  }, []);

  return `${halfFoodLine.join('')}0${halfFoodLine.reverse().join('')}`;
}
```
