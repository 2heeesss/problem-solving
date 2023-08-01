# 141. Linked List Cycle

#연결리스트

## 풀이 복기

slow - fast 알고리즘을 사용하면 연결리스트의 전체 길이를 알지못하더라도 비교가 가능하다.

### 풀이 1

```js
/**
 * @param {ListNode} head
 * @return {boolean}
 */
var hasCycle = function (head) {
  while (head) {
    if (head.visited) {
      return true;
    }
    head.visited = true;
    head = head.next;
  }

  return false;
};
```

### 풀이 2

```js
/**
 * @param {ListNode} head
 * @return {boolean}
 */
var hasCycle = function (head) {
  let slow = head;
  let fast = head;

  while (fast && fast.next) {
    slow = slow.next;
    fast = fast.next.next;
    if (slow === fast) {
      return true;
    }
  }

  return false;
};
```
