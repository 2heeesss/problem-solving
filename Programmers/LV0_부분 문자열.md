# 부분 문자열

#문자열

## 풀이 복기

includes 메서드가 생각이 안나서 배열을 직접순회하면서 찾아냈다. 이런건 금방떠올려야하는데

### 풀이 1

```js
function solution(str1, str2) {
  for (let i = 0; i < str2.length - str1.length + 1; i++) {
    let str = '';
    for (let j = 0; j < str1.length; j++) {
      str += str2[i + j];
    }
    if (str === str1) {
      return 1;
    }
  }
  return 0;
}
```

### 풀이 2

```js
function solution(str1, str2) {
  return str2.includes(str1) ? 1 : 0;
}
```
