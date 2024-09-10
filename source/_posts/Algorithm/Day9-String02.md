---
title: Day9-String02
date: 2024-09-08 22:05:34
tags:
  - String
  - KMP
categories:
  - Algorithm
---

## 151. Reverse Words in a String

### Node:

- I used split and reverse at first, actually the time complexity of split and reverse is O(n), space complexity is O(n)
- Inorder to improve the space complexity to O(1)
  - remove the extra space, there are space in the beign, middle and end
    - use slice(time complexity is O(n))
    - Or use fast and slow pointer, like in **27. Remove Element** in {% post_link Day1-Array01 %}
  - reverse the whole sentence
  - reverse every word inside

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```
var reverseWords = function(s){
    const strArr = Array.from(s);
    // remove the extra space, O(n)
    removeSpace(strArr);
    // reverse the whole sentenc, O(n)
    reverse(strArr, 0, strArr.length-1);

    let startIndex = 0;
    // loop is O(n), reverse every word is constant, total is still O(n)
    for(let i = 0; i <= strArr.length; i++){
        if(strArr[i] === " " || i === strArr.length){
            reverse(strArr, startIndex, i-1);
            startIndex = i+1;
        }
    }
    return strArr.join("");
}

var removeSpace = function(strArr){
    let slowIndex = 0, fastIndex = 0;
    // remove the space at begin and in the middle
    while(fastIndex < strArr.length){
        if(strArr[fastIndex] === " " && (fastIndex === 0 || strArr[fastIndex-1] === " ")){
            fastIndex++;
        }else{
            strArr[slowIndex] = strArr[fastIndex];
            slowIndex++;
            fastIndex++;
        }
    }
    // remove the space at end
    if(strArr[slowIndex-1] === " "){
        strArr.length = slowIndex - 1;
    }else{
        strArr.length = slowIndex;
    }
}

var reverse = function(strArr, start, end){
    while(start <  end){
        [strArr[start], strArr[end]] = [strArr[end], strArr[start]];
        start++;
        end--;
    }
}
```

## 28. Find the Index of the First Occurrence in a String

### Node:

- Find the substring in a string, which should use KMP, O(n)
  - Todo: add detailed explaination of KMP
- Bruce force is O(n^2)
  - slice is O(m)
  - **comparison(===) is O(m)**
    - I always forget to count the comparison in count the time complexity

### Time Complexity && Space Complexity

- Time Complexity: O(n+m)
- Space Complexity: O(m)

#### Brute force

```
// length of haystack is n
// length of needle is m
// Time Complexity: O(n^2)
// Space Complexity: O(m)
var strStr = function(haystack, needle) {
    if(needle.length > haystack.length){
        return -1;
    }
    //loop: O(n - m + 1), slice in every loop is O(m), comparison(===) is O(m)
    for(let i = 0; i < haystack.length - needle.length + 1; i++){
        const str = haystack.slice(i, needle.length + i);
        if(str === needle){
            return i;
        }
    }
    return -1;
};
```

#### KMP

```
// length of haystack is n
// length of needle is m
var strStr = function(haystack, needle){
    // O(m)
    function getNext(needle){
        const next = [];
        let j = 0;
        next.push(j);
        for(let i = 1; i < needle.length; i++){
            while( j > 0 && needle[i] !== needle[j]){
                j = next[j-1];
            }
            if(needle[i] === needle[j]){
                j++;
            }
            next.push(j);
        }
        return next;
    }
    // get the arr for the longest same prefix and suffix for arr[0] to arr[i]
    const next = getNext(needle);
    let j = 0;
    // O(n)
    for(let i = 0; i < haystack.length; i++){
        while( j > 0 && haystack[i] !== needle[j]){
            j = next[j-1];
        }
        if(haystack[i] === needle[j]){
            j++;
        }
        if(j === needle.length){
            return i+1 - needle.length;
        }
    }
    return -1;
}
```

## 459. Repeated Substring Pattern

### Node:

- Use KMP
  - s is "abcabcabc"
  - the longest same prefix and suffix is "abcabc", the s.length - "abcabc" = 3; s.length%3 = 0
- Use combine two s to s+s, and s+s.includes(s)
  - if s is "abcabc", abc is the substring
  - when s+s will be "abcabcabcabc"
  - if s+s(remove the first and last letter - "bc**abcabc**ab") include "abcabc", when we can prove it repeated substring pattern

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```combine two s to s+s, and s+s.includes(s)
// Time Complexity: O(n)
// Space Complexity: O(n)
var repeatedSubstringPattern = function(s) {
    // O(n)
    const doubleS = (s+s).slice(1, s.length*2 - 1);
    // O(n)
    if(doubleS.includes(s)){
        return true;
    }else{
        return false;
    }
};
```

```
var repeatedSubstringPattern = function(s) {
    const next = [];
    let j = 0;
    next.push(j);
    for(let i = 1; i < s.length; i++){
        while(j > 0 && s[j] !== s[i]){
            j = next[j-1];
        }
        if(s[j] === s[i]){
            j++;
        }
        next.push(j);
    }
    const longestSamePrefixSuffix = next[next.length-1];
    if(longestSamePrefixSuffix == 0){
        return false;
    }else{
        if(s.length % (s.length - longestSamePrefixSuffix) === 0){
            return true;
        }else{
            return false;
        }
    }
};
```
