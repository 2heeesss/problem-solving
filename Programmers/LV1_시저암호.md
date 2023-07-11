# 시저암호

#문자열

### 풀이 1

```js
function isUpperCase(char) {
  return char === char.toUpperCase();
}

function solution(s, n) {
  const [a_UTF_IDX, z_UTF_IDX] = ['a'.charCodeAt(0), 'z'.charCodeAt(0)];
  const [A_UTF_IDX, Z_UTF_IDX] = ['A'.charCodeAt(0), 'Z'.charCodeAt(0)];

  return [...s]
    .map(char => {
      if (char === ' ') return ' ';

      const nextUtfIdx = n + char.charCodeAt(0);
      const lowerCase = nextUtfIdx <= z_UTF_IDX ? nextUtfIdx : (nextUtfIdx % z_UTF_IDX) + a_UTF_IDX - 1;
      const upperCase = nextUtfIdx <= Z_UTF_IDX ? nextUtfIdx : (nextUtfIdx % Z_UTF_IDX) + A_UTF_IDX - 1;

      return isUpperCase(char) ? String.fromCharCode(upperCase) : String.fromCharCode(lowerCase);
    })
    .join('');
}
```
