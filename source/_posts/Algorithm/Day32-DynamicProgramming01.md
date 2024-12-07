---
title: Day32-DynamicProgramming01
date: 2024-12-05 16:39:13
tags:
  - DynamicProgramming
categories:
  - Algorithm
---

## 509. Fibonacci Number

### Node:

```
fib(4)
 ├── fib(3)
 │    ├── fib(2)
 │    │    ├── fib(1) -> 1
 │    │    └── fib(0) -> 0
 │    └── fib(1) -> 1
 └── fib(2)
      ├── fib(1) -> 1
      └── fib(0) -> 0

```

### Time Complexity && Space Complexity

- Time Complexity: O(2^n)
- Space Complexity: O(n)

```js
var fib = function (n) {
  if (n == 0) {
    return 0;
  }
  if (n == 1) {
    return 1;
  }
  return fib(n - 1) + fib(n - 2);
};
```

## 70. Climbing Stairs

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var climbStairs = function (n) {
  const countArr = new Array(n + 1).fill(0);
  countArr[1] = 1;
  countArr[2] = 2;
  for (let i = 3; i <= n; i++) {
    countArr[i] = countArr[i - 1] + countArr[i - 2];
  }
  return countArr[n];
};
```

## 746. Min Cost Climbing Stairs

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var minCostClimbingStairs = function (cost) {
  const costArry = new Array(cost.length + 1).fill(0);
  for (let i = 2; i < costArry.length; i++) {
    costArry[i] = Math.min(
      costArry[i - 2] + cost[i - 2],
      costArry[i - 1] + cost[i - 1]
    );
  }
  return costArry[costArry.length - 1];
};
```
