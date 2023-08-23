# 647. Palindromic Substrings

#구현

## 풀이 복기

MEDIUM_5. Longest Palindromic Substring 문제와 유사하다. 길이를 판별하는게 아닌 카운트로 바꾼 문제.
짝수 / 홀수의경우 펠린드롬이 만들어지는 방법이 다른데, 이만 잘 생각하면 된다.

### 풀이 1

```js
/**
 * AC
 * n: s.length
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(1)
 */
var countSubstrings = function (s) {
  function getSubStrCnt(leftIdx, rightIdx) {
    let cnt = 0;
    while (leftIdx >= 0 && rightIdx < s.length)
      if (s[leftIdx] === s[rightIdx]) {
        cnt += 1;
        leftIdx -= 1;
        rightIdx += 1;
      } else {
        break;
      }

    return cnt;
  }

  let res = 0;

  for (let i = 0; i < s.length; i++) {
    res += getSubStrCnt(i, i);
    res += getSubStrCnt(i, i + 1);
  }

  return res;
};
```
