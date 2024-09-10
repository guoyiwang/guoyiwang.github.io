---
title: AlgorithmSummary.md
date: 2024-09-10 12:24:44
tags:
  - Summary
categories:
  - Algorithm
---

## String(Immutable in JS)
### Common solutions
- Combine two string, check the combined include the orignal one
- Reverse the whole sentence and reverse the every word, with start and end pointer
- Remove target element, with fast and slow pointers, fast skip the target, slow point to the target, and then `arr[slowIndex] = arr[fastIndex]`, remove the target element
- KMP

## Space Complexity
- A string variable, like `const a = "sdfwefewfewfwefew"`, the space complexity depends on the size of the string stored in memory.
- arr in a for loop
    - Space Complexity should be the O(arr.length): JavaScript's garbage collector automatically frees memory for any object (or string) that is no longer referenced
- variable in the recusive
    - Space Complexity should be the O(recusive.depth*variable.length): JavaScript's garbage collector automatically frees memory for any object (or string) that is no longer referenced, but the variable is still be referenced in the recusive