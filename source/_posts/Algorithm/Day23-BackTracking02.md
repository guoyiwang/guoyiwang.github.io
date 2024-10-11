---
title: Day23-BackTracking02
date: 2024-10-11 13:07:50
tags:
  - BackTracking
categories:
  - Algorithm
---

## 39. Combination Sum

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O()
- Space Complexity: O()

```js
var combinationSum = function (candidates, target) {
  candidates.sort((a, b) => a - b);
  const res = [];
  const backTracking = function (index, path, sum) {
    if (sum === target) {
      return res.push(path);
    }
    if (sum > target) {
      return;
    }
    for (
      let i = index;
      i < candidates.length && sum + candidates[i] <= target;
      i++
    ) {
      backTracking(i, [...path, candidates[i]], sum + candidates[i]);
    }
  };
  backTracking(0, [], 0);
  return res;
};
```

## 40. Combination Sum II

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(2^n \* k)
- Space Complexity: O(2^n \* k)

```js
var combinationSum2 = function (candidates, target) {
  candidates.sort((a, b) => a - b);

  const res = [];
  const visited = new Array(candidates.length).fill(false);
  const backTracking = function (index, path, sum) {
    if (index > candidates.length) {
      return;
    }
    if (sum === target) {
      return res.push(path);
    }
    if (sum > target) {
      return;
    }
    for (
      let i = index;
      i < candidates.length && candidates[i] + sum <= target;
      i++
    ) {
      if (i > 0 && candidates[i] === candidates[i - 1] && !visited[i - 1]) {
        continue;
      }
      visited[i] = true;
      backTracking(i + 1, [...path, candidates[i]], sum + candidates[i]);
      visited[i] = false;
    }
  };
  backTracking(0, [], 0);
  return res;
};
```

## 131. Palindrome Partitioning

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(2^n \* n)
- Space Complexity: O(2^n \* n)

```js
var partition = function (s) {
  const res = [];
  const backTracking = function (index, path) {
    if (index >= s.length) {
      return res.push(path);
    }
    for (let i = index; i < s.length; i++) {
      const subString = s.slice(index, i + 1);
      if (!isValidPalindrome(subString)) {
        continue;
      } else {
        backTracking(i + 1, [...path, subString]);
      }
    }
  };
  backTracking(0, "");
  return res;
};
// a
var isValidPalindrome = function (str) {
  if (str === "") return false;
  let left = 0;
  let right = str.length - 1;
  while (left < right) {
    if (str[left] === str[right]) {
      left++;
      right--;
    } else {
      return false;
    }
  }
  return true;
};
```
