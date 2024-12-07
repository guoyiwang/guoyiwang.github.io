---
title: Day30-Greedy04
date: 2024-12-05 16:38:33
tags:
  - Greedy
categories:
  - Algorithm
---

## 452. Minimum Number of Arrows to Burst Balloons

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(nlogn)
- Space Complexity: O(n)

```js
// 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
// sort by first or second
var findMinArrowShots = function (points) {
  points.sort((a, b) => {
    if (a[0] !== b[0]) {
      return a[0] - b[0];
    } else {
      return a[1] - b[1];
    }
  });
  const stack = [points[0]];
  for (let i = 1; i < points.length; i++) {
    const [start, end] = points[i];
    if (start <= stack[stack.length - 1][1]) {
      stack[stack.length - 1][0] = start;
      stack[stack.length - 1][1] = Math.min(end, stack[stack.length - 1][1]);
    } else {
      stack.push(points[i]);
    }
  }
  return stack.length;
};
```

## 435. Non-overlapping Intervals

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(nlogn)
- Space Complexity: O(n)

```js
/**
 * @param {number[][]} intervals
 * @return {number}
 */
var eraseOverlapIntervals = function (intervals) {
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
    if (end <= stack[stack.length - 1][1]) {
      stack.pop();
    }
    stack.push(intervals[i]);
  }

  return intervals.length - stack.length;
};
```

## 763. Partition Labels

### Node:

- Three cases: stack[stack.length-1] vs new intervel
  - First: new intervel cover stack[stack.length-1], pop out stack[stack.length-1], (need to check the lastest stack[stack.length-1] when while loop is over in step2)
  - new intervel overlap stack[stack.length-1], merge stack[stack.length-1] and new intervel
  - new intervel not overlap stack[stack.length-1], push new intervel to stack

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
/**
 * @param {string} s
 * @return {number[]}
 */
var partitionLabels = function (s) {
  const stack = [];
  const indexMap = {};
  for (let i = 0; i < s.length; i++) {
    const char = s[i];
    if (indexMap[char] === undefined) {
      stack.push([i, i]);
      indexMap[s[i]] = i;
    } else {
      const charRange = [indexMap[char], i];
      // pop then charRange cover the stack[stack.length-1]
      while (
        stack.length > 0 &&
        stack[stack.length - 1][1] >= charRange[0] &&
        stack[stack.length - 1][0] >= charRange[0]
      ) {
        stack.pop();
      }
      // extend stack[stack.length-1] when stack[stack.length-1] overlap with charRange
      if (
        stack.length > 0 &&
        stack[stack.length - 1][1] >= charRange[0] &&
        stack[stack.length - 1][0] < charRange[0]
      ) {
        stack[stack.length - 1][0] = Math.min(
          stack[stack.length - 1][0],
          charRange[0]
        );
        stack[stack.length - 1][1] = Math.max(
          stack[stack.length - 1][1],
          charRange[1]
        );
      } else {
        // add charRange when no overlap
        stack.push(charRange);
      }
    }
  }
  return stack.map((item) => item[1] - item[0] + 1);
};
```
