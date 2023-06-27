# 문제 제목

#배열#set

## 풀이 복기

문제의 요구사항을 정확하게 파악하지 못했다. 맨 처음 풀이에서 O(n^2)으로 동작(while, Math.min) 하기때문에 O(n)시간복잡도 조건을 맞추지 못했다. 그렇기때문에 timeout에 걸려서 통과하지 못했다.

또한, Map을 사용할 필요가 없음에도 불구하고 관성적으로 사용했다.

두번째 풀이는 Set을 사용한 O(n)으로 고쳐서 작성했고 while부분을 함수로뺀다면 첫번째보다 가독성 측면에도 더 좋다고 판단된다.

### 풀이 1

```js
const longestConsecutive = function (nums) {
  let min = Math.min(...nums);
  let res = 0;
  let cnt = 0;

  const numMap = nums.reduce((map, num) => {
    map.set(num, true);
    return map;
  }, new Map());

  while (numMap.size > 0) {
    numMap.delete(min);
    cnt = cnt + 1;
    if (numMap.has(min + 1)) {
      min = min + 1;
    } else {
      res = Math.max(cnt, res);
      cnt = 0;
      min = Math.min(...numMap.keys());
    }
  }

  return res;
};
```

### 풀이 2

```js
const longestConsecutive = function (nums) {
  const numSet = new Set(nums);
  let res = 0;

  for (const num of nums) {
    let cnt = 1;
    if (numSet.has(num)) {
      let prev = num - 1;
      let next = num + 1;
      while (numSet.has(prev)) {
        numSet.delete(prev);
        prev = prev - 1;
        cnt = cnt + 1;
      }
      while (numSet.has(next)) {
        numSet.delete(next);
        next = next + 1;
        cnt = cnt + 1;
      }

      res = Math.max(cnt, res);
    }
  }

  return res;
};
```
