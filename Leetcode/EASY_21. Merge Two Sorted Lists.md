# 21. Merge Two Sorted Lists

#연결리스트

## 풀이 복기

첫번째 풀이는 일단 구현부터 하자는 생각으로 나온 코드다. 통과는 하지만 여러 문제가 있는데, 쓸데 없이 많은 분기문, 선언문 들이 있다. 이를 개선하는 방법으로 두번째 풀이로 풀었다.

이때 중요한건 맨처음 new ListNode()를 했을대 만들어지는 초기값을 줘야한다고 생각해서 첫번째 풀이와 같이 길어졌는데, 이때 아무런 값이나 일단 준 다음 next를 해서 두번째 노드부터 리턴하도록 하면 쉽게 구현 가능하다.

만약 원본 연결리스트의 변경을 반영하지 않아야 하는경우는 1번 풀이와같이 각 노드마다 `new ListNode()` 로 인스턴스를 만들어 할당하는게 맞을듯하다.

### 풀이 1

```js
/**
 * AC
 * n: list1 노드의 개수, m: list2 노드의 개수
 * 시간복잡도: O(n + m)
 * 공간복잡도: O(n + m)
 */
var mergeTwoLists = function (list1, list2) {
  if (!list1 && !list2) {
    return list1;
  } else if (!list1) {
    return list2;
  } else if (!list2) {
    return list1;
  }

  let l1Pointer = list1;
  let l2Pointer = list2;
  let linkedList;
  if (l1Pointer.val < l2Pointer.val) {
    linkedList = new ListNode(l1Pointer.val, null);
    l1Pointer = l1Pointer.next;
  } else {
    linkedList = new ListNode(l2Pointer.val, null);
    l2Pointer = l2Pointer.next;
  }
  const ll = linkedList;

  while (l1Pointer || l2Pointer) {
    if (!l1Pointer) {
      linkedList.next = new ListNode(l2Pointer.val, null);
      l2Pointer = l2Pointer.next;
      linkedList = linkedList.next;
      continue;
    } else if (!l2Pointer) {
      linkedList.next = new ListNode(l1Pointer.val, null);
      l1Pointer = l1Pointer.next;
      linkedList = linkedList.next;
      continue;
    }

    if (l1Pointer.val < l2Pointer.val) {
      linkedList.next = new ListNode(l1Pointer.val, null);
      l1Pointer = l1Pointer.next;
    } else {
      linkedList.next = new ListNode(l2Pointer.val, null);
      l2Pointer = l2Pointer.next;
    }
    linkedList = linkedList.next;
  }

  return ll;
};
```

### 풀이 2

```js
/**
 * AC
 * n: list1 노드의 개수, m: list2 노드의 개수
 * 시간복잡도: O(n + m)
 * 공간복잡도: O(1) -> 기존 노드의 공간을 활용하기때문
 */
var mergeTwoLists = function (list1, list2) {
  let linkedList = new ListNode(-1, null);
  const headLL = linkedList;
  let headL1 = list1;

  while (list1 || list2) {
    if (!list1 || !list2) {
      linkedList.next = list1 ? list1 : list2;
      break;
    }

    if (list1.val < list2.val) {
      linkedList.next = list1;
      list1 = list1.next;
    } else {
      linkedList.next = list2;
      list2 = list2.next;
    }
    linkedList = linkedList.next;
  }

  headL1 = new ListNode();

  return headLL.next;
};
```
