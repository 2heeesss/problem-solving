# 567. Permutation in String

#슬라이딩윈도우

## 풀이 복기

첫번째 접근방법은 틀린 접근법이다. s1, s2가 각각 `abc`, `babc` 인 경우에 동작하지 않기때문.
두번째, 세번째 접근방법은 부르트포스 방식으로 모든 경우를 각각 확인하는 방법이다. 두 방법은 시간복잡도는 동일하나, slice메서드를 사용해서 문자열을 자르거나, 인덱스를 사용해서 문자열을 자르는 방법에 있어서 시간의 차이가 있다.

네번째 방법은 슬라이딩 윈도우를 사용해서 시간복잡도를 최적화 한 방법이다. 이런 문제가 나왔을때 Map으로만 해결하려는 습관이 있는데, 비교가 필요한 순간 배열이 더 편한 방법이라 생각됨. join()으로 쉽게 확인 가능하기때문.

### 풀이 1

```js
/**
 * Fail
 * n: s1.length, m: s2.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(1)
 */
var checkInclusion = function (s1, s2) {
  let cnt = s1.length;
  let charMap = new Map();
  for (const char of s1) {
    charMap.set(char, charMap.get(char) || 1);
  }
  const fixCharMap = Object.freeze(charMap);

  for (const char of s2) {
    if (charMap.has(char) && charMap.get(char) > 0) {
      charMap.set(char, charMap.get(char) - 1);
      cnt -= 1;
    } else {
      charMap = Object.freeze(fixCharMap);
      cnt = s1.length;
    }

    if (cnt === 0) {
      return true;
    }
  }

  return false;
};
```

### 풀이 2

```js
/**
 * 시간초과
 * n: s1.length, m: s2.length
 * 시간복잡도: O(nm)
 * 공간복잡도: O(n)
 */
var checkInclusion = function (s1, s2) {
  let cnt = s1.length;
  let charMap = new Map();

  const clearCharMap = () => {
    charMap.clear();
    for (const char of s1) {
      charMap.set(char, charMap.get(char) + 1 || 1);
    }
  };
  clearCharMap();

  for (let i = 0; i < s2.length - s1.length + 1; i++) {
    const subStr = s2.slice(i, i + s1.length);
    clearCharMap();
    cnt = s1.length;
    for (const char of subStr) {
      if (charMap.has(char) && charMap.get(char) > 0) {
        charMap.set(char, charMap.get(char) - 1);
        cnt -= 1;
      } else {
        break;
      }

      if (cnt === 0) {
        return true;
      }
    }
  }

  return false;
};
```

### 풀이 3

```js
/**
 * AC
 * n: s1.length, m: s2.length
 * 시간복잡도: O(nm)
 * 공간복잡도: O(n)
 */
var checkInclusion = function (s1, s2) {
  let cnt = s1.length;
  let charMap = new Map();

  const clearCharMap = () => {
    charMap.clear();
    for (const char of s1) {
      charMap.set(char, charMap.get(char) + 1 || 1);
    }
  };
  clearCharMap();

  for (let i = 0; i < s2.length - s1.length + 1; i++) {
    clearCharMap();
    cnt = s1.length;
    for (let j = i; j < i + s1.length; j++) {
      const char = s2[j];
      if (charMap.has(char) && charMap.get(char) > 0) {
        charMap.set(char, charMap.get(char) - 1);
        cnt -= 1;
      } else {
        break;
      }

      if (cnt === 0) {
        return true;
      }
    }
  }

  return false;
};
```

### 풀이 4

```js
/**
 * AC
 * n: s1.length, m: s2.length
 * 시간복잡도: O(n)
 * 공간복잡도: O(1)
 */
var checkInclusion = function (s1, s2) {
  const s1Count = new Array(26).fill(0);
  const s2Count = new Array(26).fill(0);

  for (let i = 0; i < s1.length; i++) {
    s1Count[s1.charCodeAt(i) - 'a'.charCodeAt(0)]++;
  }

  for (let i = 0; i < s2.length; i++) {
    s2Count[s2.charCodeAt(i) - 'a'.charCodeAt(0)]++;

    if (i >= s1.length) {
      s2Count[s2.charCodeAt(i - s1.length) - 'a'.charCodeAt(0)]--;
    }
    console.log(s2Count.join());

    if (s1Count.join() === s2Count.join()) {
      return true;
    }
  }

  return false;
};
```
