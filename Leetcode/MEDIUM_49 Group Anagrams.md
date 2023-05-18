# 49 Group Anagrams

#배열

## 풀이 복기

arr.push(..)를 Map 에 바로 set 하면서 실수한 부분이 있다.
Array.push의 리턴값은 배열의 길이 이므로 set하는 값이 배열이 아니라 숫자 타입이 들어가게 된다. 실수하지말자

push 하지 않고 arr을 선언할때 str까지 함께 추가하는게 더 좋은 방법같다.

### 풀이 1

```js
const groupAnagrams = function (strs) {
  const anagramMap = strs.reduce((anagramMap, str) => {
    const sortedStr = [...str].sort().join('');
    if (anagramMap.has(sortedStr)) {
      const arr = [...anagramMap.get(sortedStr)];
      arr.push(str);
      anagramMap.set(sortedStr, arr);
    } else {
      anagramMap.set(sortedStr, [str]);
    }
    return anagramMap;
  }, new Map());

  return [...anagramMap.values()];
};
```

### 풀이 2

```js
const groupAnagrams = function (strs) {
  const anagramMap = strs.reduce((anagramMap, str) => {
    const sortedStr = [...str].sort().join('');
    if (anagramMap.has(sortedStr)) {
      anagramMap.set(sortedStr, [...anagramMap.get(sortedStr), str]);
    } else {
      anagramMap.set(sortedStr, [str]);
    }
    return anagramMap;
  }, new Map());

  return [...anagramMap.values()];
};
```
