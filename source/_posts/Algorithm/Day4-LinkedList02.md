---
title: 24. Swap Nodes in Pairs && 19. Remove Nth Node From End of List && 160. Intersection of Two Linked Lists && 142. Linked List Cycle II
date: 2024-08-25 17:27:42
tags:
  - Linked List
categories:
  - Algorithm
---

## 24. Swap Nodes in Pairs

### Node:

- Understand Space Complexity(O(1))
  - `second` variable is assigned the reference to a exist node in the current linkedlist
  - When you declare a variable inside a loop (e.g., `const second = ...;`), memory is allocated for that variable **only for the duration of that iteration**.
  - Once the iteration completes and the variable goes out of scope, the memory can be reclaimed, especially in languages with garbage collection like JavaScript.
  - This means that at any given time, there is only one instance of the second variable occupying memory, regardless of how many iterations the loop runs.
  - If the algorithm were **recursive**, each recursive call would add a new layer to the call stack, resulting in O(n) space complexity

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```
var swapPairs = function(head) {
    if(!head || !head.next) return head;
    let dummyHead = new ListNode(null, head);
    let res = dummyHead;
    while(dummyHead && dummyHead.next){
        const second = dummyHead.next.next;
        if(!second){
            break;
        }
        dummyHead.next.next = second.next;
        second.next = dummyHead.next;
        dummyHead.next = second;
        dummyHead = dummyHead.next.next;
    }
    return res.next;
};
```

## 19. Remove Nth Node From End of List

### Node:

- fast and slow poitner
  - be case for the edge case, like `head = [1], n = 1` or `head = [1,2], n = 1`

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```
var removeNthFromEnd = function(head, n) {
    let slow = head;
    let fast = head;
    while(n>0 && fast){
        fast = fast.next;
        n--;
    }
    if(!fast){
        return slow.next;
    }
    while(fast){
        if(!fast.next){
            slow.next = slow.next.next;
            break;
        }
        slow = slow.next;
        fast = fast.next;
    }
    return head;
};
```

## 160. Intersection of Two Linked Lists

### Node:

- same value doesn't mean same not

### Time Complexity && Space Complexity

- Time Complexity: O(n+m)
- Space Complexity: O(1)

```
var getIntersectionNode = function(headA, headB) {
    let lengthA = 0;
    let lengthB = 0;
    let rootA = headA;
    let rootB = headB;
    while(rootA){
        lengthA++;
        rootA = rootA.next;
    }
    while(rootB){
        lengthB++;
        rootB = rootB.next;
    }
    if(lengthA > lengthB){
        [lengthA, lengthB] = [lengthB, lengthA];
        [headA, headB] = [headB, headA];
    }
    let diff = lengthB - lengthA;
    while(diff > 0){
        headB = headB.next;
        diff--;
    }
    while(headA && headB){
        if(headA === headB){
            return headA;
        }
        headA = headA.next;
        headB = headB.next;
    }
    return null;
};
```

## 142. Linked List Cycle II

### Note:

- fast and slow pointer - fast: head.next.next; - slow: head.next - fastLength: x+y+z+y - slowLength: x+y - `2*slowLength = fastLength` => `2(x+y) = x+y+z+y` => `x = y`
  ![find Intersection In Cycle](/images/findIntersectionInCycle.png)

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```
var detectCycle = function(head) {
    if(!head || !head.next){
        return null;
    }
    let slow = head.next;
    let fast = head.next.next;
    while(fast && fast.next && slow && fast !== slow){
        slow = slow.next;
        fast = fast.next.next;
    }
    while(head && slow){
        if(head === slow){
            return head;
        }
        head = head.next;
        slow = slow.next;
    }
    return null;
};
```
