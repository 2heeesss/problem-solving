# 3. Longest Substring Without Repeating Characters

#슬라이딩윈도우

## 풀이 복기

첫번째 풀이는 for, indexOf 때문에 O(n^2) 시간복잡도를 갖는다. 이때 이미 지나온 문자 중 현재 문자와 동일한것을 찾는데 시간을 줄이려 했다. 그래서 Map()을 사용해서 조회하는데 시간을 줄인 풀이가 두번째 풀이. 공간복잡도는 늘어나는 트레이드오프가 있긴하다

### 풀이 1

```js
/**
 * AC
 * n: s.length
 * 시간복잡도: O(n^2)
 * 공간복잡도: O(1)
 */
var lengthOfLongestSubstring = function (s) {
  let subStr = '';
  let maxSubStrLen = 0;

  for (let i = 0; i < s.length; i++) {
    const repeatCharIdx = subStr.indexOf(s.at(i));
    if (repeatCharIdx === -1) {
      subStr += s.at(i);
    } else {
      maxSubStrLen = Math.max(maxSubStrLen, subStr.length);
      subStr = subStr.slice(repeatCharIdx + 1);
      subStr += s.at(i);
    }
  }

  return Math.max(maxSubStrLen, subStr.length);
};
```

### 풀이 2

```js
/**
 * AC
 * n: s.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(n)
 */
var lengthOfLongestSubstring = function (s) {
  const charMap = new Map();
  let maxSubStrLen = 0;
  let startPoint = 0;

  for (let i = 0; i < s.length; i++) {
    if (charMap.has(s.at(i))) {
      startPoint = Math.max(charMap.get(s.at(i)) + 1, startPoint);
    }
    charMap.set(s.at(i), i);
    maxSubStrLen = Math.max(maxSubStrLen, i - startPoint + 1);
  }

  return maxSubStrLen;
};
```
