# 347. Top K Frequent Elements

#배열#해쉬

## 풀이 복기

시간복잡도: O(n) + O(mlogm) -> n은 nums의 크기, m은 numMap의 크기. 이는 O(nlogn)보다 작거나 같다.
같은 경우는 모든 배열의 요소가 겹치지 않는 요소 일 경우.

시간복잡도를 더 줄이는 방법은 해쉬맵을 순회하면서 value를 인덱스로 갖는 요소에 key를 저장하는 배열을 만들고, 배열의 가장 뒤에서부터 순회하며 k만큼의 요소를 뽑아내면 된다. 하지만 해당 방법은 공간복잡도가 O(최빈값) 만큼 차지하기 때문에 좋지 않다고 생각한다.

### 풀이 1

```js
var topKFrequent = function (nums, k) {
  const numMap = nums.reduce((map, num) => {
    map.has(num) ? map.set(num, map.get(num) + 1) : map.set(num, 1);
    return map;
  }, new Map());

  return [...numMap.entries()]
    .sort((a, b) => b[1] - a[1])
    .filter((_, idx) => idx < k)
    .map(numEntries => numEntries[0]);
};
```
