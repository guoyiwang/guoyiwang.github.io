---
title: Day22-BackTracking01
date: 2024-10-11 13:07:40
tags:
  - BackTracking
categories:
  - Algorithm
---

## 77. Combinations

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(k * C(n, k))
    - there are C(n, k) times recusive
    - In every recusive, create a new path cost O(k)
- Space Complexity: O(k * C(n, k))

```js
var combine = function(n, k) {
    const res = [];
    const backTracking = function(index, path){
        if(path.length === k){
            return res.push(path);
        }
        // i=0,1,2,3
        for(let i = index; i <n; i++){
            backTracking(i+1, [...path, i+1])
        }
    }
    backTracking(0, [])
    return res;
};
```

## 216. Combination Sum III

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(k * C(9,k))
- Space Complexity: O(k * C(9, k)) 

```js
var combinationSum3 = function(k, n) {
    const res = [];
    const backTracking = function(index, path, sum){
        if(sum === n && path.length === k){
            return res.push(path);
        }
        if(path.length > k || sum > n){
            return;
        }
        for(let i = index+1; i<= 9 && i+sum <= n; i++){
            backTracking(i, [...path, i], sum+i)
        }
    }
    backTracking(0, [], 0);
    return res;
};
```

## 17. Letter Combinations of a Phone Number

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(4^n * n)
- Space Complexity: O(4^n * n)

```js
var letterCombinations = function(digits) {
    const letterMap = {
        "2": "abc",
        "3": "def",
        "4": "ghi",
        "5": "jkl",
        "6": "mno",
        "7": "pqrs",
        "8": "tuv",
        "9": "wxyz"
    };
    const res = [];
    if(digits.length === 0){
        return res;
    }
    const backTracking = function(index, path){
        if(index === digits.length){
            return res.push(path);
        }
        const letters = letterMap[digits[index]];
        for(let i = 0; i < letters.length; i++){
            const letter = letters[i];
            backTracking(index+1, path+letter);
        }
    }
    backTracking(0, "");
    return res;
};
```
