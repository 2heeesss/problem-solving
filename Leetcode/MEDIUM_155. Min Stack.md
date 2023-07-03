# 155. Min Stack

#스택

## 풀이 복기

각 메서드는 O(1) 시간복잡도를 가져야한다. push, pop, top 메서드의 경우에는 상관 없지만, getMin의 경우를 잘 처리해야했다.

기존에는 Math.min(...arr) 방식으로 처리하려했지만 해당 방법은 O(n)으로 동작하므로 요구사항에 맞지않다. 그렇기때문에 push, pop 시점에 최소값을 계속 저장하는 배열을 업데이트 하는 방법으로 구현했다.

### 풀이 1

```js
var MinStack = function () {
  this.arr = [];
  this.min = [];
};

/**
 * @param {number} val
 * @return {void}
 */
MinStack.prototype.push = function (val) {
  this.arr.push(val);
  const prevMin = this.min.length === 0 ? val : this.min[this.min.length - 1];
  this.min.push(Math.min(val, prevMin));
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function () {
  this.arr.pop();
  this.min.pop();
};

/**
 * @return {number}
 */
MinStack.prototype.top = function () {
  return this.arr[this.arr.length - 1];
};

/**
 * @return {number}
 */
MinStack.prototype.getMin = function () {
  return this.min[this.arr.length - 1];
};

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(val)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */
```
