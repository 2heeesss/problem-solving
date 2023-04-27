# 서울에서 김서방 찾기

#배열#문자열

### 풀이 1

```js
function solution(seoul) {
  const kimIndex = seoul.findIndex(name => name === 'Kim');
  return `김서방은 ${kimIndex}에 있다`;
}
```
