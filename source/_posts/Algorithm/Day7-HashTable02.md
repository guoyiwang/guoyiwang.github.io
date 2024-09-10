---
title: Day7-HashTable 02
date: 2024-08-30 22:20:50
tags:
  - HashTable
categories:
  - Algorithm
---

## 454. 4Sum II

### Node:

- Create an `arrA` which is sum of the Combination of `arr1` and `arr2`, and an `arrB` which is sum of the Combination of `arr3` and `arr4`,
  - This question will be change to find the `element from arrA + element from arrB = 0`;
- Using Map in JavaScript can indeed be faster than using an Object as a hashtable, especially when dealing with large datasets or frequent insertions and lookups

### Time Complexity && Space Complexity

- Time Complexity: O(n^2)
- Space Complexity: O(n^2)
  - The worse case, every sum from the `const sum = num1 + num2;` inside two layer loop are different every time

```
var fourSumCount = function(nums1, nums2, nums3, nums4) {
    const twoSumMap = new Map();;
    let count = 0;
    for(const num1 of nums1){
        for(const num2 of nums2){
            const sum = num1 + num2;
            if(twoSumMap.has(sum)){
                twoSumMap.set(sum, twoSumMap.get(sum)+1)
            }else{
                twoSumMap.set(sum, 1)
            }
        }
    }

    for(const num3 of nums3){
        for(const num4 of nums4){
            const sum = num3 + num4;
            const reminder = 0 - sum;
            if(twoSumMap.has(reminder)){
                count += twoSumMap.get(reminder);
            }
        }
    }
    return count;
};
```

## 383. Ransom Note

### Node:

- `magazine.length` could equal or more than `ransomNote.length`

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)
  - There are only 26 letters
  - The size of map wouldn't increase when the input length incease

```
var canConstruct = function(ransomNote, magazine) {
    const map = {};
    for(const char of magazine){
        if(map[char] === undefined){
            map[char] = 1;
        }else{
            map[char] += 1;
        }
    }
    for(const char of ransomNote){
        if(!map[char]){
            return false;
        }
        map[char] -= 1;
    }
    return true;
};
```

## 15. 3Sum

### Node:

- Use hashtable will be too complex and will get time exceed error for some use cases
- Use three pointers
  - i `for(let i = 0; i < nums.length; i++)`
    - when `nums[i] > 0`, break
    - when `i>0 && nums[i]==nums[i-1]` continue;
  - j: `j=i+1`
    - when`sum < target`, `j++`
    - when `sum === 0`, `j++` and `while(nums[j] === nums[j-1]&&j<k) j++;`
  - k: `k=nums.length-1`
    - when `sum > target`, `k--`
    - when `sum === 0`, `k--` and `while(nums[k] === nums[k+1] && j < k) k--;`

### Time Complexity && Space Complexity

- Time Complexity: O(n^2)
  - the outer loop: O(n)
  - Inside, j and k will iterate the nums one round in total
- Space Complexity: O(1)

```
var threeSum = function(nums) {
    nums.sort((a,b)=>a-b);
    const res = [];
    for(let i = 0; i < nums.length; i++){
        if(nums[i] > 0) break;
        if(i > 0 && nums[i]===nums[i-1]) continue;
        let j = i+1;
        let k = nums.length - 1;
        while(j < k){
            const sum = nums[i] + nums[j] + nums[k];
            if(sum < 0){
                j++;
            }else if(sum > 0){
                k--;
            }else{
                res.push([nums[i], nums[j], nums[k]]);
                j++;
                k--;
                while(nums[j] === nums[j-1]&&j<k) j++;
                while(nums[k] === nums[k+1] && j < k) k--;
            }
        }
    }
    return res;
};
```

## 18. 4Sum

### Node:

- Similar as 3sum, just need one more loop
- target could be negative
- Use four pointers
  - i `for(let i = 0; i < nums.length; i++)`
    - when `i>0 && nums[i]==nums[i-1]` continue;
  - j `for(let j = i+1; i < nums.length; j++)`
    - when `j > i+1 && nums[j] == nums[j-1]` continue
  - k: `k=j+1`
    - when`sum < target`, `k++`
    - when `sum === 0`, `k++` and `while(nums[k] === nums[k-1]&&k<l) k++;`
  - l: `l=nums.length-1`
    - when `sum > target`, `l--`
    - when `sum === 0`, `l--` and `while(nums[l] === nums[l+1] && k < l) l--;`

### Time Complexity && Space Complexity

- Time Complexity: O(n^3)
- Space Complexity: O(1)

```
var fourSum = function(nums, target) {
    nums.sort((a,b) => a-b);
    const res = [];
    for(let i = 0; i < nums.length; i++){
        if(nums[i] > target && target >= 0 ) break;
        if(nums[i] >= 0 && target < 0 ) break;
        if(i>0&&nums[i]==nums[i-1]) continue;
        for(let j = i+1; j < nums.length; j++){
            if(j > i+1 && nums[j] == nums[j-1]) continue;
            let k = j+1;
            let l = nums.length-1;
            while(k<l){
                const sum = nums[i] + nums[j] + nums[k] + nums[l];
                if(sum > target){
                    l--;
                }else if(sum < target){
                    k++;
                }else{
                    res.push([nums[i], nums[j], nums[k], nums[l]]);
                    k++;
                    l--;
                    while(k<l && nums[k] == nums[k-1]) k++;
                    while(k<l && nums[l] == nums[l+1]) l--;
                }
            }
        }
    }
    return res;
};
```
