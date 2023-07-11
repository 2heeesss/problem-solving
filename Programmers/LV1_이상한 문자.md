# 이상한 문자 만들기

#문자열

### 풀이 1

```js
function solution(s) {
  return s
    .split(' ')
    .map(subStr => [...subStr].map((char, idx) => (idx % 2 === 0 ? char.toUpperCase() : char.toLowerCase(char))).join(''))
    .join(' ');
}
```
