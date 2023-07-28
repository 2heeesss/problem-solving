# 19. Remove Nth Node From End of List

#문제카테고리1#문제카테고리2

## 풀이 복기

첫번째 풀이는 다음과 같다.

1. 연결리스트의 전체 길이를 구한다.
2. 끝에서 n번째 위치로 이동한다.
3. 해당 노드를 건너뛴다.

이 풀이는 O(n)이다. 하지만 전체 연결리스트를 두번 순회하게 된다. 이 방법을 해결하기 위해 slow-fast 투포인터 알고리즘을 사용하면 한번만 순회해서 끝에서 n 번째 위치를 찾을 수 있다.

두번째 풀이

1. fast 포인터를 n만큼 오른쪽으로 이동한다.
2. slow, fast 포인터를 fast의 next가 null 값 나올때까지 오른쪽으로 이동한다
3. slow 포인터의 현재 위치는 끝에서 n번째 위치가 되므로, 해당 노드를 건너뛴다.

### 풀이 1

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * AC
 * m: head 연결리스트 길이
 * 시간복잡도: O(m)
 * 공간복잡도: O(1)
 */
var removeNthFromEnd = function (head, n) {
  let l1 = head;
  let l2 = head;
  let len = 0;
  while (l1) {
    len += 1;
    l1 = l1.next;
  }

  const targetIdx = len - n;
  if (targetIdx === 0) {
    return l2.next;
  }

  let currentIdx = 0;
  while (currentIdx < targetIdx - 1) {
    currentIdx += 1;
    head = head.next;
  }

  console.log(JSON.stringify(head));
  if (!head.next) {
    head.next = null;
  } else {
    head.next = head.next.next;
  }

  return l2;
};
```

### 풀이 2

```js
/**
 * AC
 * m: head 연결리스트 길이
 * 시간복잡도: O(m)
 * 공간복잡도: O(1)
 */
var removeNthFromEnd = function (head, n) {
  const list = new ListNode(-1, null);
  let fast = list;
  let slow = list;
  list.next = head;

  while (n > 0) {
    fast = fast.next;
    n -= 1;
  }

  while (fast.next) {
    fast = fast.next;
    slow = slow.next;
  }

  slow.next = slow.next.next;
  return list.next;
};
```
