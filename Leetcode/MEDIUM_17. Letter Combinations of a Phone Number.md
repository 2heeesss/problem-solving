# 17. Letter Combinations of a Phone Number

#백트래킹

## 풀이 복기

백트래킹은 머리속에 트리구조를 그려가며 생각하면 풀기쉽다.

### 풀이 1

```js
/**
 * AC
 * n: digits.length
 * 시간복잡도: O(4^n)
 * 공간복잡도: O(4^n)
 */
var letterCombinations = function (digits) {
  if (!digits.length) {
    return [];
  }
  const res = [];
  const path = [];
  const digitsMap = getDigitsMap();

  function backtrack(digitIdx) {
    if (digitIdx >= digits.length) {
      res.push([...path].join(''));
      return;
    }
    const strs = digitsMap.get(digits[digitIdx]);
    strs.forEach(str => {
      path.push(str);
      backtrack(digitIdx + 1);
      path.pop();
    });
  }

  backtrack(0);
  return res;
};

function getDigitsMap() {
  const map = new Map();

  map.set('2', ['a', 'b', 'c']);
  map.set('3', ['d', 'e', 'f']);
  map.set('4', ['g', 'h', 'i']);
  map.set('5', ['j', 'k', 'l']);
  map.set('6', ['m', 'n', 'o']);
  map.set('7', ['p', 'q', 'r', 's']);
  map.set('8', ['t', 'u', 'v']);
  map.set('9', ['w', 'x', 'y', 'z']);

  return map;
}
```
