# 문자열 바꿔서 찾기

#string

## 풀이 복기

첫번째 풀이에서 바로 A -> B, B -> A 이렇게 바로 replace를 하게되면 두번째 replace에서 전부 다 같은 문자로 바뀌게 된다. 그래서 소문자로 바꿔준다음 대문자로 변경시켜주는 과정을 거쳤다. 또한, myString이 아닌 pat을 replace 한 이유는 pat 문자열의 최대 길이가 10으로 myString 문자열의 최대길이보다 짧기 때문.

두번재 풀이에서는 두번의 replaceAll보다 map으로 한번에 처리하는게 도 좋은 방법으로 생각되어 변경.

### 풀이 1

```js
function solution(myString, pat) {
  const replacePat = pat.replaceAll('A', 'b').replaceAll('B', 'a').toUpperCase();
  return myString.includes(replacePat) ? 1 : 0;
}
```

### 풀이 2

```js
function solution(myString, pat) {
  const replacePat = [...pat].map(word => (word === 'A' ? 'B' : 'A')).join('');
  return myString.includes(replacePat) ? 1 : 0;
}
```
