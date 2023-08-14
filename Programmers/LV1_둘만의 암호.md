# 둘만의 암호

#수학#구현

## 풀이 복기

수학문제를 풀때는 글로 한번써보고 풀자 아니면 실수가 나올수밖에

### 풀이 1

```js
function solution(s, skip, index) {
  const aUtf16 = 'a'.charCodeAt(0);
  const zUtf16 = 'z'.charCodeAt(0);
  const aTozRange = zUtf16 - aUtf16;
  const skipCharSet = getSkipUtf16Set(skip);

  const utf16Chars = [...s].map(char => {
    let charUtf16 = char.charCodeAt(0);
    let cnt = 0;
    while (cnt < index) {
      charUtf16 = charUtf16 + 1 > zUtf16 ? ((zUtf16 - charUtf16) % aTozRange) + aUtf16 : charUtf16 + 1;
      if (!skipCharSet.has(charUtf16)) {
        cnt += 1;
      }
    }
    return String.fromCharCode(charUtf16);
  });

  return utf16Chars.join('');
}

function getSkipUtf16Set(str) {
  return [...str].reduce((set, cur) => {
    set.add(cur.charCodeAt(0));
    return set;
  }, new Set());
}
```
