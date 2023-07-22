# 981. Time Based Key-Value Store

#이진탐색#해쉬맵

## 풀이 복기

처음 접근은 timestamp 를 기반으로 Map을 만드는것으로 시작했다. 이 방법으로는 시간초과를 맞출수가 없어서 실패했다.

첫번째풀이, 두번째 풀이는 key 를 기반으로 Map을 만들었다. value, timestamp를 배열에 저장하는식으로 동작한다.
이 방법은 이진탐색이 가능하므로 입력값의 범위에 잘 작동할것이라 생각했다.

하지만 첫번째 풀이에서 스프레드연산자를 습관적으로 사용한것때문에 시간초과가 발생했다. push를 사용하자

### 풀이 1

```js
/**
 * Fail
 * n: set, get 호출 횟수, m: 특정 키에 대한 입력 값의 개수, k: set 호출횟수
 * 시간복잡도: O(nm)
 * 공간복잡도: O(k)
 */
var TimeMap = function () {
  this.keyMap = new Map();
};

TimeMap.prototype.set = function (key, value, timestamp) {
  if (this.keyMap.has(key)) {
    const innerArr = this.keyMap.get(key);
    this.keyMap.set(key, [...innerArr, { value, timestamp }]);
  } else {
    const innerArr = [{ value, timestamp }];
    this.keyMap.set(key, innerArr);
  }
};

TimeMap.prototype.get = function (key, timestamp) {
  const arr = this.keyMap.get(key);
  let head = 0;
  let tail = arr.length - 1;
  let stk = '';
  while (head <= tail) {
    const mid = Math.floor((head + tail) / 2);
    const midVal = arr.at(mid);
    if (midVal.timestamp <= timestamp) {
      head = mid + 1;
      stk = midVal.value;
    } else {
      tail = mid - 1;
    }
  }

  return stk === 0 ? '' : stk;
};
```

### 풀이 2

```js
/**
 * AC
 * n: set, get 호출 횟수, m: 특정 키에 대한 입력 값의 개수, k: set 호출횟수
 * 시간복잡도: O(n * logm)
 * 공간복잡도: O(k)
 */
var TimeMap = function () {
  this.keyMap = new Map();
};

TimeMap.prototype.set = function (key, value, timestamp) {
  if (this.keyMap.has(key)) {
    const innerArr = this.keyMap.get(key);
    innerArr.push({ value, timestamp });
  } else {
    const innerArr = [{ value, timestamp }];
    this.keyMap.set(key, innerArr);
  }
};

TimeMap.prototype.get = function (key, timestamp) {
  if (!this.keyMap.has(key)) return '';

  const arr = this.keyMap.get(key);
  let head = 0;
  let tail = arr.length - 1;
  let stk = '';

  while (head <= tail) {
    const mid = Math.floor((head + tail) / 2);
    const midVal = arr.at(mid);
    if (midVal.timestamp < timestamp) {
      head = mid + 1;
      stk = midVal.value;
    } else if (midVal.timestamp > timestamp) {
      tail = mid - 1;
    } else {
      return midVal.value;
    }
  }

  return stk === 0 ? '' : stk;
};
```
