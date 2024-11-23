---
title: Day24-BackTracking03
date: 2024-10-15 22:03:18
tags:
  - BackTracking
categories:
  - Algorithm
---

## 93. Restore IP Addresses

### Node:

### Time Complexity && Space Complexity

- Time Complexity: `O(3^n)`
  - In every digital, there are 3 options, str.slice(index, index+1), str.slice(index, index+2), str.slice(index, index+3)
  - There are 12 digital at most
- Space Complexity: `O(m)`, where m is the number of valid IP addresses stored in the result array.
  - Recursion Depth: 4
  - Result Storage:O(m), where m is the number of valid IP addresses.
  - Auxiliary Space: Each recursive call stores a copy of the current path, which can have at most 4 parts (since an IP address has 4 segments)

```js
var restoreIpAddresses = function (s) {
  const res = [];
  const backTracking = function (index, path) {
    if (path.length > 4) {
      return;
    }
    if (index === s.length) {
      if (path.length === 4) {
        return res.push(path.join("."));
      } else {
        return;
      }
    }
    for (let i = index; i < index + 3 && i < s.length; i++) {
      const subStr = s.slice(index, i + 1);
      if (isValid(subStr, s)) {
        backTracking(i + 1, [...path, subStr]);
      }
    }
  };
  backTracking(0, []);
  return res;
};

var isValid = function (str, s) {
  // the max lengh of other three str are 3, total is 9
  if (str.length + 9 < s.length) {
    return false;
  }
  if (str === "") {
    return false;
  }
  if (str[0] === "0" && str.length > 1) {
    return false;
  }
  const value = Number(str);
  if (value < 0 || value > 255) {
    return false;
  } else {
    return true;
  }
};
```

## 78. Subsets

### Node:

### Time Complexity && Space Complexity

- Time Complexity: `O(n * 2^n)`
  - There are `2^n` recusive
    - There are two choices (include or exclude) for each of the `n` elements, the total number of different combinations (subsets) we can create is `2^n`
  - Copy one array in every recusive
  - Compare to backtracking question: generating all k-item subsets (combinations of k elements) from an array nums.length=n
    - `O( C(n,k) * k)`
      - combinations problem, and the number of ways to choose k elements from an array of n elements
      - copy a array is `O(k)`
- Space Complexity: `O( n * 2^n)`
  - Recursion Stack: depends on the recursion depth which is at most `n`: O(n)
  - Space for Storing Results: (usually don't count the result space) O(n \* 2^n)
    - store 2^n subset, every subset length is n
  - Auxiliary Space:
    - a new array is created in every recursive call

```js
var subsets = function (nums) {
  const res = [];
  const backTracking = function (index, path) {
    if (index > nums.length) {
      return;
    }
    res.push(path);
    for (let i = index; i < nums.length; i++) {
      backTracking(i + 1, [...path, nums[i]]);
    }
  };
  backTracking(0, []);
  return res;
};
```

## 90. Subsets II

### Node:

### Time Complexity && Space Complexity

- Time Complexity: `O(n*logn)+O(n*2^n) = O(n*2^n)`
- Space Complexity: `O(n*2^n)`

```js
var subsetsWithDup = function (nums) {
  const res = [];
  nums.sort((a, b) => a - b);
  const visited = new Array(nums.length).fill(false);
  const backTracking = function (index, path) {
    if (index > nums.length) {
      return;
    }
    res.push(path);
    for (let i = index; i < nums.length; i++) {
      if (i > 0 && nums[i] === nums[i - 1] && !visited[i - 1]) {
        continue;
      }
      visited[i] = true;
      backTracking(i + 1, [...path, nums[i]]);
      visited[i] = false;
    }
  };
  backTracking(0, []);
  return res;
};
```
