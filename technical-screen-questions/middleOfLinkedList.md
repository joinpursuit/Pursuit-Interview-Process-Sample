# Middle of a Linked List

https://leetcode.com/problems/middle-of-the-linked-list/

## Prompt

Given a singly linked list with head node head, return a middle node of linked list.

## Clarifying Questions & Assumptions

Answers to questions the fellows may ask:

- What if there are an even number of elements? _If there are two middle nodes, return the second middle node._
- What if the head is nil? _The head will never be nil_
- What's the maximum number of nodes? _There will be less than 100 nodes in the list_

## Sample Inputs and Outputs

### Example One:

#### Input

```
1 -> 2 -> 3 -> 4 -> 5 -> nil
```

#### Output

```
3 -> 4 -> 5 -> nil
```

### Example Two:

#### Input

```
1 -> 2 -> 3 -> 4 -> 5 -> 6 -> nil
```

#### Output

```
4 -> 5 -> 6 -> nil
```

## Hints

If a fellow has been stuck for several minutes, it's OK to offer a hint to keep things moving:

- How can we find out when to stop iterating?
- How can we get the size of the Linked List?
- Is there a way we could do it in a single pass?

## Solution Overview

#### Two Passes

1. Get the count of the Linked List
1. Iterate forward until you are at half that number

#### Two Pointers

1. Create a slow pointer and a fast pointer
1. While the fast pointer's next isn't null, move the slow pointer ahead one node, and the fast pointer ahead by two nodes
1. Return the node the slow pointer is pointing at

## Solution Code

### Swift

```swift
func middleNode(_ head: ListNode?) -> ListNode? {
    var count = getCount(head)
    var currentNode = head
    for _ in 0..<(count / 2) {
        currentNode = currentNode?.next
    }
    return currentNode
}
func getCount(_ head: ListNode?) -> Int {
    guard let head = head else { return 0 }
    return 1 + getCount(head.next)
}
```

#### Single-pass solution with two pointers

```swift
func middleNode(_ head: ListNode?) -> ListNode? {
    var slow = head
    var fast = head
    while fast?.next != nil {
        slow = slow?.next
        fast = fast?.next?.next
    }
    return slow
}
```

### JavaScript

```js
const middleNode = (head) => {
    let currentNode = head;
    for (let i=0; i<(Math.floor(getCount(head) /2)); i++) {
        currentNode = currentNode.next;
    }
    return currentNode;
};

const getCount = (head) => {
    if (!head) { return 0 }
    return 1 + getCount(head.next);
}
```

#### Single-pass solution with two pointers

```js
const middleNode = (head) => {
    let slow = head;
    let fast = head;
    while (fast && fast.next) {
        slow = slow.next
        fast = fast.next.next
    }
    return slow
};
```
