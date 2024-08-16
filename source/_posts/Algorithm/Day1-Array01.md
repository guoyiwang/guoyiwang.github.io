---
title: 704. Binary Search and 27. Remove Element
date: 2024-08-15 17:16:41
tags:
  - Array
categories:
  - Algorithm
---

## Concept

- Time Complexity: The Time Complexity of an algorithm/code is not equal to the actual time required to execute a particular code, but **the number of times a statement executes**
- Space Complexity: The **total amount of memory space** used by an algorithm/program, including the space of input values for execution

## 704. Binary Search

### Iterate

#### left include, right include, [left, right]

```JavaScript
var search = function(nums, target) {
    let left = 0;
    let right = nums.length - 1;
    // target will be in [left, right]
    while(left <= right){
        let mid = Math.floor((left+right)/2);
        let num = nums[mid];
        if(num == target){
            return mid;
        }else if(num < target){
            left = mid + 1;
        }else{
            right = mid - 1;
        }
    }
    return -1;
};
```

#### left include, right exclude, [left, right)

```
var search = function(nums, target) {
    let left = 0;
    let right = nums.length;
    // target will be in [left, right)
    while(left < right){
        let mid = Math.floor((left+right)/2);
        let num = nums[mid];
        if(num == target){
            return mid;
        }else if(num < target){
            left = mid + 1;
        }else{
            right = mid;
        }
    }
    return -1;
};
```

- Time Complexity: O(logn)
  - If there are n element, the scope of every loop will be n, n/2, n/4, ...n/2^k, k is the count of loop
  - Finally, n/2^k >= 1, then n = 2^k, k = log2n, k is how many time the code be run
- Space Complexity: O(1)
  - Since only create left/right one time

### Recursive

- Three steps in Recsive
  - define function parameter and return
  - end condition
  - logical for every recusive

```JS
var search = function(nums, target) {
    return recusive(nums, target, 0, nums.length - 1)
}

function recusive(nums, target, left, right){
    if(target < nums[left] || target > nums[right] || left > right){
        return -1;
    }
    const mid = Math.floor((left + right)/2);
    if(nums[mid] === target){
        return mid;
    }else if(nums[mid] < target){
        return recusive(nums, target, mid+1, right)
    }else{
        return recusive(nums, target, left, mid-1)
    }
}
```

- Time Complexity: O(logn)
  - depth of recusive is logn
- Space Complexity: O(logn)
  - depth of recusive(logn) \* space need for every recusive

## 27. Remove Element

### slow pointer and fast pointer

```
// fast pointer will find the non-target first
// slow will still be target
// swap
var removeElement = function(nums, val) {
    let slow = 0;
    for(let fast = 0; fast < nums.length; fast++){
        // when fast pointer to the item not target, slow still pointer to the target
        if(nums[fast] !== val){
            nums[slow] = nums[fast];
            slow++;
        }
    }
    return slow;
}
```

- Time Complexity: O(1)
- Space Complexity: O(1)