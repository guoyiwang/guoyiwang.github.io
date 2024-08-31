---
title: Day8-String01
date: 2024-08-30 23:09:25
tags:
  - String
categories:
  - Algorithm
---

## 344. Reverse String

### Node:

- Two pointers
- Reverse inplace
  The reverse() method of Array instances reverses an array **in place** and returns the reference to the same array

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```
var reverseString = function(s) {
    let start = 0;
    let end = s.length - 1;
    while(start <= end){
        let temp = s[start];
        s[start] = s[end];
        s[end] = temp;
        start++;
        end--;
    }
    return s;
};
```

## 541. Reverse String II

### Node:

- can't change the string's char by `string1[0] = "c"`, it doesn't work

  - In JavaScript, strings are immutable, which means once a string is created, its characters cannot be changed directly.

    - String: `let str = "hello"; str = str + " world"`; (This creates a new string rather than modifying the original str).
    - Numbers: Numbers are also immutable. Any operation on a number returns a new number rather than modifying the original value.
    - Booleans: true and false are immutable.
    - null and undefined: These are immutable by nature, as they represent the absence of value.
    - Symbols: Introduced in ES6, symbols are unique and immutable. Once created, a symbol's value cannot be changed.
      (All primitive type are immutable, You cannot change a primitive's value. Any operation that appears to change a primitive actually creates a new primitive.)

  - Convert to a array and then change it by `arr[0] = "c"`

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```
var reverseStr = function(s, k) {
    let start = 0;
    let end = start + k-1;
    const arr = s.split("");
    for(let i = 0; i < s.length; i+=2*k){
        const start = i;
        const end = start + k - 1;
        reverse(arr, start, end < arr.length ? end : arr.length);
    }
    return arr.join("");
};

var reverse = function(arr, start, end){
    while(start <= end){
        let temp = arr[start];
        arr[start] = arr[end];
        arr[end] = temp;
        start++;
        end--;
    }
}
```
