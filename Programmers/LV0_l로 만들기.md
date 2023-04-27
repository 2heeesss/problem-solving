# l로 만들기

#문자열

## 풀이 복기

l의 아스키코드인 108보다 작을때 l문자로 변경시켜주는 방법으로 작성했다. 두번째 풀이는 정규식으로 더 간단하게 문자열 안에서 해결함

### 풀이 1

```js
function solution(myString) {
  const lAscciCode = 108;
  return [...myString].map(char => (char.charCodeAt() < 108 ? 'l' : char)).join('');
}
```

### 풀이 2

```js
function solution(myString) {
  return myString.replace(/[a-k]/g, 'l');
}
```
