---
title: Day3-Linked List 01
date: 2024-08-23 10:19:34
tags:
  - Linked List
categories:
  - Algorithm
---

## 203. Remove Linked List Elements

### Node:

    - Create a dummy header
    - Need another while inside the while, which is for the case like [7,7,7,7]

### Time Complexity && Space Complexity

- Time Complexity: O(n)
  - Every element is maniplated once
- Space Complexity: O(1)

```
var removeElements = function(head, val) {
    let dummyHead = new ListNode(null, head);
    const result = dummyHead;
    while(dummyHead){
        while(dummyHead.next && dummyHead.next.val === val){
            dummyHead.next = dummyHead.next.next;
        }
        dummyHead = dummyHead.next;
    }
    return result.next;
};
```

## 707. Design Linked List

### Node

- Need a dummyHead and a size variable
- need consider index is 0 for get/addAtIndex/deleteAtIndex
- If create a end to track the tail, need to update the end in
  - `void addAtHead(int val)`: when add first element, update end
  - `void addAtTail(int val)`: update end
  - `void deleteAtIndex(int index)`: delete the last one, update the end

### Time Complexity && Space Complexity

- Time Complexity:
  - `int get(int index)`: O(index)
  - `void addAtHead(int val)`: O(1)
  - `void addAtTail(int val)`: O(n)
  - `void addAtIndex(int index, int val)`: O(index)
  - `void deleteAtIndex(int index)`: O(index)
- Space Complexity: O(n)

```

function ListNode(val, next){
    this.val = (val === undefined ? 0 : val);
    this.next = (next === undefined ? null : next);
}

var MyLinkedList = function() {
    this.dummyHead = new ListNode();
    this.length = 0;
};

/**
 * @param {number} index
 * @return {number}
 */
MyLinkedList.prototype.get = function(index) {
    if(index >= this.length || index < 0){
        return -1;
    }
    let root = this.dummyHead;
    while(root && index >= 0){
        root = root.next;
        if(index == 0){
            return root.val;
        }
        index--;
    }
    return -1;
};

/**
 * @param {number} val
 * @return {void}
 */
MyLinkedList.prototype.addAtHead = function(val) {
    const next = this.dummyHead.next;
    const newHead = new ListNode(val, next);
    this.dummyHead.next = newHead;
    this.length++;
};

/**
 * @param {number} val
 * @return {void}
 */
MyLinkedList.prototype.addAtTail = function(val) {
    const newEnd = new ListNode(val);
    let root = this.dummyHead;
    while(root){
        if(!root.next){
            root.next= newEnd;
            break;
        }
        root = root.next;
    }
    this.length++;
};

/**
 * @param {number} index
 * @param {number} val
 * @return {void}
 */
MyLinkedList.prototype.addAtIndex = function(index, val) {
    if(index > this.length){
        return;
    }else if(index == this.length){
        this.addAtTail(val);
    }else if(index == 0){
        this.addAtHead(val);
    }else{
        let root = this.dummyHead;
        while(root && index > 0){
            root = root.next;
            index--;
            if(index === 0){
                const newNode = new ListNode(val, root.next);
                root.next = newNode;
            }
        }
        this.length++;
    }
};

/**
 * @param {number} index
 * @return {void}
 */
MyLinkedList.prototype.deleteAtIndex = function(index) {
    if(index >= this.length) return;
    let root = this.dummyHead;
    while(root && index >= 0){
        if(index === 0){
            const needDelete = root.next;
            const next = needDelete && needDelete.next ? needDelete.next : null;
            root.next = next;
        }
        root = root.next;
        index--;
    }
    this.length--;

};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * var obj = new MyLinkedList()
 * var param_1 = obj.get(index)
 * obj.addAtHead(val)
 * obj.addAtTail(val)
 * obj.addAtIndex(index,val)
 * obj.deleteAtIndex(index)
 */
```

## 206. Reverse Linked List

### Node:

- create a new Node for every node
- Or use two pointer to change on the input

#### Create new node for every one

- Time Complexity && Space Complexity
  - Time Complexity: O(n)
  - Space Complexity: O(n): since need to create new ListNode in every loop

```
var reverseList = function(head) {
    let dummyHead = new ListNode();
    while(head){
        const next = dummyHead.next;
        dummyHead.next = new ListNode(head.val, next);
        head = head.next;
    }
    return dummyHead.next;
};
```

#### Use two pointer to change on it, no need to create new ListNode every time

- Time Complexity && Space Complexity
  - Time Complexity: O(n)
  - Space Complexity: O(1): only declare temp, prev, curr once

```
var reverseList = function(head) {
    if(!head || !head.next) return head;
    let temp = null
    let prev = null
    let curr = head;
    while(curr){
        temp = curr.next;
        curr.next = prev;
        prev = curr;
        curr = temp;
    }
    return prev;
};
```
