# 가장 가까운 같은 글자

#문자열#배열

### 풀이 1

```js
function solution(s) {
  const charMap = new Map();
  return [...s].map((char, idx) => {
    let prevPosition = charMap.has(char) ? idx - charMap.get(char) : -1;
    charMap.set(char, idx);
    return prevPosition;
  });
}
```
