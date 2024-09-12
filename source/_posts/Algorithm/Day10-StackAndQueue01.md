---
title: Day10-StackAndQueue01
date: 2024-09-12 10:28:27
tags:
  - Stack&Queue
categories:
  - Algorithm
---

## 232. Implement Queue using Stacks

### Node:

- ## Use two queue to implement stack

### Time Complexity && Space Complexity

- Time Complexity:
  - Option1
    - push: O(n)
    - pop: O(1)
    - peek: O(1)
    - empty: O(1)
  - Option2
    - push: O(1)
    - pop: worst case O(n), best case: O(1)
    - peek: worst case O(n), best case: O(1)
    - empty: O(1)
- Space Complexity: O(n)

```js
var MyQueue = function () {
  this.stackA = [];
  this.stackB = [];
};

/** Option1
 * @param {number} x
 * @return {void}
 */
MyQueue.prototype.push = function (x) {
  while (this.stackB.length > 0) {
    this.stackA.push(this.stackB.pop());
  }
  this.stackB.push(x);
  while (this.stackA.length > 0) {
    this.stackB.push(this.stackA.pop());
  }
};

/** Option2
 * @return {number}
 */
MyQueue.prototype.pop = function () {
  return this.stackB.pop();
};

/**
 * @return {number}
 */
MyQueue.prototype.peek = function () {
  return this.stackB[this.stackB.length - 1];
};

/**
 * @return {boolean}
 */
MyQueue.prototype.empty = function () {
  return this.stackB.length === 0;
};
```

```js
var MyQueue = function () {
  this.stackIn = [];
  this.stackOut = [];
};

/**
 * @param {number} x
 * @return {void}
 */
MyQueue.prototype.push = function (x) {
  this.stackIn.push(x);
};

/**
 * @return {number}
 */
MyQueue.prototype.pop = function () {
  const size = this.stackOut.length;
  if (size > 0) return this.stackOut.pop();

  while (this.stackIn.length > 0) {
    this.stackOut.push(this.stackIn.pop());
  }
  return this.stackOut.pop();
};

/**
 * @return {number}
 */
MyQueue.prototype.peek = function () {
  const x = this.pop();
  this.stackOut.push(x);
  return x;
};

/**
 * @return {boolean}
 */
MyQueue.prototype.empty = function () {
  return this.stackIn.length === 0 && this.stackOut.length === 0;
};
```

## 225. Implement Stack using Queues

### Node:

- Use shift and push to mimic queue

### Time Complexity && Space Complexity

- Time Complexity:
  - push: O(n)
  - pop: O(n)
  - peek: O(1)
  - empty: O(1)
- Space Complexity: O(n)

```js
var MyStack = function () {
  this.queue1 = [];
  this.queue2 = [];
};

/**
 * @param {number} x
 * @return {void}
 */
MyStack.prototype.push = function (x) {
  for (let i = 0; i < this.queue2.length; i++) {
    this.queue1.push(this.queue2[i]);
  }
  this.queue2.length = 0;
  this.queue2.push(x);
  for (let i = 0; i < this.queue1.length; i++) {
    this.queue2.push(this.queue1[i]);
  }
  this.queue1.length = 0;
};

/**
 * @return {number}
 */
MyStack.prototype.pop = function () {
  return this.queue2.shift();
};

/**
 * @return {number}
 */
MyStack.prototype.top = function () {
  return this.queue2[0];
};

/**
 * @return {boolean}
 */
MyStack.prototype.empty = function () {
  return this.queue2.length === 0;
};
```

## 20. Valid Parentheses

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var isValid = function (s) {
  const stack = [];
  for (let i = 0; i < s.length; i++) {
    const char = s[i];
    if (
      stack.length > 0 &&
      ((char === ")" && stack[stack.length - 1] === "(") ||
        (char === "]" && stack[stack.length - 1] === "[") ||
        (char === "}" && stack[stack.length - 1] === "{"))
    ) {
      stack.pop();
    } else {
      stack.push(char);
    }
  }
  return stack.length === 0;
};
```

## 1047. Remove All Adjacent Duplicates In String

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var removeDuplicates = function (s) {
  const stack = [];
  for (let i = 0; i < s.length; i++) {
    const char = s[i];
    if (stack.length > 0 && char === stack[stack.length - 1]) {
      stack.pop();
    } else {
      stack.push(char);
    }
  }
  return stack.join("");
};
```
