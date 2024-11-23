---
title: Day28-Greedy02
date: 2024-11-23 07:21:06
tags:
  - Greedy
categories:
  - Algorithm
---

## 122. Best Time to Buy and Sell Stock II

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var maxProfit = function(prices) {
    const profits = [];
    for(let i = 1; i < prices.length; i++){
        profits.push(prices[i] - prices[i-1]);
    }
    let sum = 0;
    for(const profit of profits){
        if(profit > 0){
            sum += profit;
        }
    }
    return sum;
};
```

## 55. Jump Game

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```js
// Greedy
var canJump = function(nums){
    if(nums.length == 1) return true;
    let maxIndex = nums[0];
    for(let i = 1; i < nums.length; i++){
        if(maxIndex >= i){
            maxIndex = Math.max(maxIndex, nums[i] + i);
        }
    }
    return maxIndex > nums.length;
}
```

## 45. Jump Game II

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```js
var jump = function(nums) {
    if(nums.length == 1) return 0;
    let cover = 0;
    let count = 0;
    for(let i = 0; i < nums.length; i++){
        cover = Math.max(cover, nums[i] + i);
        count++;
        if(cover >= nums.length - 1){
            return count;
        }
    }
    return -1;
};
```

##

### Node: 1005. Maximize Sum Of Array After K Negations

### Time Complexity && Space Complexity

- Time Complexity: O()
- Space Complexity: O()

```js
var largestSumAfterKNegations = function(nums, k) {
    nums.sort((a,b) => a-b);
    for(let i = 0; i < nums.length; i++){
        if(nums[i] < 0 && k > 0){
            nums[i] = -nums[i];
            k--;
        }
    }
    // nums 没有负数，k没用完 k > 负数
    // nums 有负数， k用完 k < 负数
    nums.sort((a,b) => a-b);
    if( k > 0){
        if(k%2 === 1){
            nums[0] = -nums[0];
        }
    }
    return nums.reduce((pre, curr) => pre+curr, 0)
};
```