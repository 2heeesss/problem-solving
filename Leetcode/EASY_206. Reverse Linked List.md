# 206. Reverse Linked List

#연결리스트

## 풀이 복기

연결리스트를 순회하는 방법 두가지를 사용해서 뒤집었다. while, 재귀 두가지 방법이 있다.
재귀를 사용함에 있어서 언제 리턴할건지 중요한데 헷갈리지말자. 헷갈리면 그림으로 그린다음에 풀자

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
 * n: 연결리스트 노드의 개수
 * 시간복잡도: O(n)
 * 공간복잡도: O(n) -> 재귀 공간
 */
var reverseList = function (head) {
  if (head === null) {
    return head;
  }

  function rec(node, prevNode) {
    const nextNode = node.next;
    node.next = prevNode;
    if (!nextNode) {
      return node;
    }
    return rec(nextNode, node);
  }
  return rec(head, null);
};
```

### 풀이 2

```js
/**
 * AC
 * n: 연결리스트 노드의 개수
 * 시간복잡도: O(n)
 * 공간복잡도: O(1)
 */
var reverseList = function (head) {
  if (head === null) {
    return head;
  }

  let currentNode = head;
  let prevNode = null;

  while (currentNode !== null) {
    let nextNode = currentNode.next;
    currentNode.next = prevNode;
    prevNode = currentNode;
    currentNode = nextNode;
  }

  return prevNode;
};
```
