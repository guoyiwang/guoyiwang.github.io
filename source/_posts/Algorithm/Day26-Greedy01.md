---
title: Day26-Greedy01
date: 2024-11-23 07:20:58
tags:
  - Greedy
categories:
  - Algorithm
---

## 455. Assign Cookies

### Node:

    - we can assign the cookie j to the child i, but can't assign the cookie j to two child

### Time Complexity && Space Complexity

- Time Complexity: O(nlogn + mlogn), n is length of g, m is the length of s
  - sort array: O(nlogn + mlogn)
- Space Complexity: O(logn + logn)
  - sort array: O(logn + logn), n is length of g, m is the length of s

```js
var findContentChildren = function (g, s) {
  g.sort((a, b) => a - b);
  s.sort((a, b) => a - b);
  let res = 0;
  let sIndex = s.length - 1;
  for (let i = g.length - 1; i >= 0; i--) {
    if (s[sIndex] >= g[i] && sIndex >= 0) {
      res++;
      sIndex--;
    }
  }
  return res;
};
```

## 376. Wiggle Subsequence

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var wiggleMaxLength = function (nums) {
  if (nums.length <= 1) {
    return nums.length;
  }
  let direction = 0;
  const res = [nums[0]];
  for (let i = 1; i < nums.length; i++) {
    const diff = nums[i] - res[res.length - 1];
    if (diff === 0) {
      continue;
    }
    if (direction === 0) {
      direction = diff > 0 ? 1 : -1;
      res.push(nums[i]);
    } else {
      direction = direction * -1;
      if (diff * direction > 0) {
        res.push(nums[i]);
      } else {
        res.pop();
        res.push(nums[i]);
        direction = direction * -1;
      }
    }
  }
  return res.length;
};
```

## 53. Maximum Subarray

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```js
var maxSubArray = function (nums) {
  let sum = nums[0];
  let res = sum;
  for (let i = 1; i < nums.length; i++) {
    sum = Math.max(nums[i], sum + nums[i]);
    res = Math.max(res, sum);
  }
  return res;
};
```
