# 125. Valid Palindrome

#정규식#완전탐색#투포인터

## 풀이 복기

풀이1과 2는 비슷한 방식으로 동작한다. 팰린드롬 문자열인지 확인하는 방법에서 반을 자르냐 전체를 확인하느냐 차이다.

1. 숫자, 영어 소문자로만 이루어진 문자열로 변경
2. 팰린드롬 문자열인지 확인 (반 잘라서 같은지 확인 or 전체를 뒤집은것 같은지 확인)

풀이 3번은 팰린드롬 문자열을 확인할때 투포인터로 head, tail에서 같은지 확인하면서 가운데 인덱스까지 도착하게 된다.

3개 풀이의 시간복잡도는 O(n)으로 동일하다. 하지만 투포인터 방법이 문자열 전체를 확인하지 않을 수 있으므로 조금 더 빠르게 동작한다.

### 풀이 1

```js
/**
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var isPalindrome = function (s) {
  const alphaNumericStr = [...s]
    .map(c => c.toLowerCase())
    .join('')
    .replace(/[^a-z0-9]/g, '');

  const halfLen = Math.floor(alphaNumericStr.length / 2);
  const halfIdx = alphaNumericStr.length % 2 === 0 ? halfLen : halfLen + 1;
  const startStr = alphaNumericStr.slice(0, halfLen);
  const endStr = [...alphaNumericStr].slice(halfIdx).reverse().join('');

  return startStr === endStr;
};
```

### 풀이 2

```js
/**
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var isPalindrome = function (s) {
  const alphaNumericStr = [...s].reduce((str, char) => str + char.toLowerCase().replace(/[^a-z0-9]/, ''), '');
  return alphaNumericStr === [...alphaNumericStr].reverse().join('');
};
```

### 풀이 3

```js
/**
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var isPalindrome = function (s) {
  const alphaNumericStr = [...s].reduce((str, char) => str + char.toLowerCase().replace(/[^a-z0-9]/, ''), '');

  let head = 0;
  let tail = alphaNumericStr.length - 1;

  while (head <= tail) {
    if (alphaNumericStr[head] !== alphaNumericStr[tail]) return false;
    head += 1;
    tail -= 1;
  }
  return true;
};
```
