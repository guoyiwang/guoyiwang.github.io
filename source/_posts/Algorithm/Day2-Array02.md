---
title: Day2-Array02
date: 2024-08-23 09:35:17
tags:
  - Array
  - Sliding Window
categories:
  - Algorithm
---

## 209. Minimum Size Subarray Sum

### Note: 
- sliding window: a fixed or variable-size window is moved through a data structure, to solve problems efficiently based on continous subsets of elements. It's used to find subarrays or substrings to a given set of conditions
    - start index: how to move it?
    - increase the start index when meet the condition
    - end index: how to move it?
    - use for loop to keep increase the end index
    - from start to end, what are inside the scope?

### Time Complexity && Space Complexity

- Time Complexity: O(n)
  - when moving the window, every element is added to sum for one time, is deleted from the sum for one time
- Space Complexity: O(1)

```
/**
 * @param {number} target
 * @param {number[]} nums
 * @return {number}
 */
var minSubArrayLen = function(target, nums) {
    let ans = Number.MAX_SAFE_INTEGER;

    let i = 0;
    let j = 0;
    let sum = 0;
    while( j < nums.length){
        sum += nums[j];
        while(sum >= target && i < nums.length){
            ans = Math.min(ans, j - i + 1);
            sum -= nums[i];
            i++;
        }
        j++;
    }
    return ans == Number.MAX_SAFE_INTEGER ? 0 : ans;
};
```

## 59. Spiral Matrix II

### Note: 
- every for loop only include the left, exclude the right, which could keep the consistent

### Time Complexity && Space Complexity

- Time Complexity: O(n^2)
  - when moving the window, every element is added to sum for one time, is deleted from the sum for one time
- Space Complexity: O(1)

```
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
    const res = new Array(n).fill().map(()=>new Array(n).fill(0));
    let value = 1;
    let row = 0;
    let col = 0;
    let offSet = 1;
    let start = 0;
    let loop = Math.floor(n/2);
    // all need be [left, right)
    // keep safe will make the code easy
    while(loop > 0){
        let row = start, col = start;
        for(; col < n - offSet; col++){
            res[row][col] = value;
            value++;
        }
        for(; row < n - offSet; row++){
            res[row][col] = value;
            value++;
        }
        for(; col> start; col--){
            res[row][col] = value;
            value++;
        }
        for(; row >start; row--){
            res[row][col] = value;
            value++;
        }
        start++;
        offSet++;
        loop--;
    }
    let mid = Math.floor(n/2);
    if(n%2 == 1){
        res[mid][mid] = n*n;
    }
    return res;
};
```
