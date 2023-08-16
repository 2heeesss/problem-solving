# 5. Longest Palindromic Substring

#구현

## 풀이 복기

1번 풀이에서는 회문의 길이가 홀수인 경우만 판단했기 때문에 제대로 정답이 나오지 않음. 2번 풀이에서는 홀수, 짝수 경우 둘다 커버한다.

### 풀이 1

```js
/**
 * Fail
 */
var longestPalindrome = function (s) {
  let res = '';

  for (let i = 0; i < s.length; i++) {
    let leftPointer = i - 1;
    let rightPointer = i + 1;
    let leftStr = s[leftPointer];
    let rightStr = s[rightPointer];
    let cnt = 0;

    while (leftPointer >= 0 && rightPointer < s.length) {
      cnt += 1;
      leftPointer -= 1;
      rightPointer += 1;
      if (s[leftPointer] + leftStr === rightStr + s[rightPointer]) {
        leftStr = s[leftPointer] + leftStr;
        rightStr = rightStr + s[rightPointer];
      } else {
        break;
      }
    }

    res = cnt > res.length ? `${leftStr}${s[i]}${rightStr}` : res;
  }

  return res;
};
```

### 풀이 2

```js
/**
 * AC
 * n: s.length
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(1)
 */
var longestPalindrome = function (s) {
  function findP(i, j) {
    while (i >= 0 && j < s.length && s[i] === s[j]) {
      i -= 1;
      j += 1;
    }
    return s.slice(i + 1, j);
  }

  let res = '';

  for (let i = 0; i < s.length; i++) {
    const subStr1 = findP(i, i);
    const subStr2 = findP(i, i + 1);
    const sub = subStr1.length > subStr2.length ? subStr1 : subStr2;
    res = res.length > sub.length ? res : sub;
  }

  return res;
};
```
