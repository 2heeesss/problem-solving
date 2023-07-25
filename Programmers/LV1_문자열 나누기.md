# 문자열 나누기

#문자열

## 풀이 복기

1번 풀이는 for에 while을 섞어서 풀었는데 i가 for에서만 값이 변경되는게 아니라 while에서도 변경되어서 가독성 측면에서 좋지 않다고 생각함.
while문이 없이도 풀수있어서 두번째 풀이로 변경

### 풀이 1

```js
/**
 * AC
 * n: s.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(1)
 */
function solution(s) {
  let cnt = 0;

  for (let i = 0; i < s.length; i++) {
    cnt += 1;
    const fixChar = s[i];
    let fixCharCnt = 1;
    while (fixCharCnt > 0) {
      i += 1;
      const nextChar = s[i];
      if (nextChar === fixChar) {
        fixCharCnt += 1;
      } else {
        fixCharCnt -= 1;
      }
    }
  }

  return cnt;
}
```

### 풀이 2

```js
/**
 * AC
 * n: s.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(1)
 */
function solution(s) {
  let res = 0;
  let currentChar = '';
  let charCnt = 0;

  for (const char of s) {
    if (charCnt === 0) {
      currentChar = char;
      charCnt += 1;
      res += 1;
    } else {
      if (char === currentChar) {
        charCnt += 1;
      } else {
        charCnt -= 1;
      }
    }
  }

  return res;
}
```
