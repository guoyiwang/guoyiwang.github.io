---
title: Day6-HashTable 01
date: 2024-08-28 22:16:49
tags:
  - HashTable
categories:
  - Algorithm
---

## 242. Valid Anagram

### Node:

- Could also use array, since there are only 26 letters
  - every letter index is char.charCodeAt() - "a".charCodeAt();

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)
  - map's size is determined by the number of unique characters in "s", which max is 26
  - map's size is constant and not grow up with the size of input "s"

```
var isAnagram = function(s, t) {
    if(s.length !== t.length) return false;
    const map = {};
    for(const char of s){
        if(map[char] === undefined){
            map[char] = 1;
        }else{
            map[char]++;
        }
    }
    for(const char of t){
        // undefined or 0
        if(!map[char]){
            return false;
        }
        map[char]--;
    }
    return true;
};
```

## 349. Intersection of Two Arrays

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n+m)
- Space Complexity: O(n)

```
var intersection = function(nums1, nums2) {
    const nums1Set = new Set(nums1);
    const res = new Set();
    for(const num of nums2){
        if(nums1Set.has(num)){
            res.add(num);
        }
    }
    return Array.from(res);
};
```

## 202. Happy Number

### Node:
- Key: there will be same number(n) if it will be a endless loop
- getSum
    ```
    const getSum = (n)=>{
        let sum = 0;
        while(n>0){
            sum += (n%10) * (n%10);
            n = Math.floor(n/10);
        }
        return sum;
    }
    ```
    - Rather than transfer number to string and split and sum by digit one by one, the getSum use mod and divide is a good way

### Time Complexity && Space Complexity

- Time Complexity: log(n)
    - loop * time complexity of getSum
    - loop is the length of cycle, which should be a small constant number
    - getSum: log(n)
- Space Complexity: log(n)
    - cache: store the unique sum of the squares of digits

- Max number999 => 243 => 29
- You can try 9999, 999999
- getSum: will be called a maximum of O(log n) times. Because log10 n is the number of digits.
- isHappy: will be called a maximum of 9^2 per digit. This is the max we can store in the hash set before we find a cycle or terminate.

Use Recursive
```
var isHappy = function(n) {
    let cache = new Map();
    function count(n){
        if(n === 1){
            return true;
        }
        if(cache.has(n)){
            return false;
        }
        const sum = getSum(n);
        cache.set(n, sum);
        return count(sum);
    return count(n);
};
const getSum = (n)=>{
    let sum = 0;
    while(n>0){
        sum += (n%10) * (n%10);
        n = Math.floor(n/10);
    }
    return sum;
}
```

Use while(true)
```
var isHappy = function(n) {
    let cache = new Map();
    // the count of loop is constant number
    while(true){
        if(n === 1){
            return true;
        }
        if(cache.has(n)){
            return false;
        }
        // O(logn)
        const sum = getSum(n);
        cache.set(n, sum);
        n = sum;
    }
};
// the number of loop here is log10(n). 10 is base
const getSum = (n)=>{
    let sum = 0;
    while(n>0){
        sum += (n%10) * (n%10);
        n = Math.floor(n/10);
    }
    return sum;
}
```
## 1. Two Sum

### Node:
- when save to map, use nums[i]
- when check whether exist in the map, use target-nums[i]

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```
var twoSum = function(nums, target) {
    const map = {};
    let res = [];
    for(let i = 0; i < nums.length; i++){
        const left = target - nums[i];
        if(map[left] === undefined){
            map[nums[i]] = i;
        }else{
            res.push(map[left], i);
        }
    }
    return res;
};
```
