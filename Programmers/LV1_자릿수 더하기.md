# 자릿수 더하기

#문자열

### 풀이 1

```js
function solution(n) {
  return [...n.toString()].reduce((acc, cur) => acc + Number(cur), 0);
}
```
