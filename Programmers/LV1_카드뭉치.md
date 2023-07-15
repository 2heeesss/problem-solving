# 카드 뭉치

#구현#배열

## 풀이 복기

shift()를 사용하면 코드가 좀더 간결해지지만 O(n)이 걸리는 shift()를 루프동안 계속 사용하고싶지는 않았다.

### 풀이 1

```js
/**
 * AC
 * n: goal.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(1)
 */
function solution(cards1, cards2, goal) {
  let card1Pointer = 0;
  let card2Pointer = 0;

  for (let i = 0; i < goal.length; i++) {
    if (card1Pointer < cards1.length && cards1[card1Pointer] === goal[i]) {
      card1Pointer += 1;
    } else if (card2Pointer < cards2.length && cards2[card2Pointer] === goal[i]) {
      card2Pointer += 1;
    } else {
      return 'No';
    }
  }
  return 'Yes';
}
```
