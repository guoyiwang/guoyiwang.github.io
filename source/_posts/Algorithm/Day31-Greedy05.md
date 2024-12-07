---
title: Day31-Greedy05
date: 2024-12-05 16:38:44
tags:
  - Greedy
categories:
  - Algorithm
---

## 56. Merge Intervals

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(nlogn)
- Space Complexity: O(n)

```js
/**
 * @param {number[][]} intervals
 * @return {number[][]}
 */
var merge = function (intervals) {
  intervals.sort((a, b) => {
    if (a[0] !== b[0]) {
      return a[0] - b[0];
    } else {
      return a[1] - b[1];
    }
  });

  const stack = [intervals[0]];
  for (let i = 1; i < intervals.length; i++) {
    const [start, end] = intervals[i];
    if (stack[stack.length - 1][1] >= start) {
      stack[stack.length - 1][0] = Math.min(stack[stack.length - 1][0], start);
      stack[stack.length - 1][1] = Math.max(stack[stack.length - 1][1], end);
    } else {
      stack.push(intervals[i]);
    }
  }
  return stack;
};
```

## 738. Monotone Increasing Digits

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
/**
 * @param {number} n
 * @return {number}
 */
var monotoneIncreasingDigits = function (n) {
  const strArr = String(n)
    .split("")
    .map((char) => Number(char));
  const stack = [strArr[0]];
  for (let i = 1; i < strArr.length; i++) {
    let currChar = strArr[i];
    if (stack[stack.length - 1] <= currChar) {
      stack.push(currChar);
    } else {
      while (stack.length > 0 && stack[stack.length - 1] > currChar) {
        stack[stack.length - 1]--;
        currChar = 9;
        currChar = stack.pop();
      }
      stack.push(currChar);
      break;
    }
  }
  let missingNine = strArr.length - stack.length;
  while (missingNine > 0) {
    stack.push(9);
    missingNine--;
  }

  return Number(stack.join(""));
};

var monotoneIncreasingDigits = function (n) {
  const digitArr = String(n)
    .split("")
    .map((item) => Number(item));
  let nineStartIndex = 0;
  for (let i = digitArr.length - 2; i >= 0; i--) {
    if (digitArr[i] > digitArr[i + 1]) {
      digitArr[i]--;
      nineStartIndex = i + 1;
    }
  }
  if (nineStartIndex > 0) {
    for (let i = nineStartIndex; i < digitArr.length; i++) {
      digitArr[i] = 9;
    }
  }
  return Number(digitArr.join(""));
};
```

## 968. Binary Tree Cameras

### Node:

- For the root node, there are three different cases
  - root is 2, which is covered by children
  - root is 1, which is a camera, and it children would be 0
  - root is 0, which means it need to be a camera, then return count + 1.

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```js
var minCameraCover = function (root) {
  let count = 0;
  const dfs = function (root) {
    if (root.left) {
      dfs(root.left);
    }
    if (root.right) {
      dfs(root.right);
    }
    if (
      (root.left && root.left.val === 0) ||
      (root.right && root.right.val === 0)
    ) {
      count++;
      root.val = 1;
    } else if (
      (root.left && root.left.val === 1) ||
      (root.right && root.right.val === 1)
    ) {
      root.val = 2; //cover
    }
  };
  dfs(root);
  if (root.val === 0) {
    return count + 1;
  }
  return count;
};
```
