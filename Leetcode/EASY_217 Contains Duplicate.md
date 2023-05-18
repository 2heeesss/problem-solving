# Contains Duplicate

#배열

### 풀이 1

```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function (nums) {
  return nums.length !== new Set(nums).size;
};
```
