---
title: Day17-BinaryTree05
date: 2024-10-05 22:02:06
tags:
  - BinaryTree
categories:
  - Algorithm
---

## 654. Maximum Binary Tree

### Node:

### Time Complexity && Space Complexity

- Time Complexity:
  - Worst case: O(n\*n)
  - Average case: O(nlogn)
    - In the average case, the maximum element tends to be closer to the middle of the current subarray.
    - the binary tree formed will have a height of approximately `log n`
    - At each level of recursion(`log n`), we need to find the maximum element in a subarray. For an array of size n, finding the maximum element takes `O(n)` time.
- Space Complexity: O(n)

```js
var constructMaximumBinaryTree = function (nums) {
  var recusive = function (nums, left, right) {
    if (left > right) {
      return null;
    }
    const [rootValue, rootIndex] = findMaxValueAndIndex(nums, left, right);
    const root = new TreeNode(rootValue);
    if (left < rootIndex) {
      root.left = recusive(nums, left, rootIndex - 1);
    }
    if (rootIndex < right) {
      root.right = recusive(nums, rootIndex + 1, right);
    }
    return root;
  };
  return recusive(nums, 0, nums.length - 1);
};

var findMaxValueAndIndex = function (nums, left, right) {
  let max = nums[left];
  let maxIndex = left;
  for (let i = left + 1; i <= right; i++) {
    const currentValue = nums[i];
    if (currentValue > max) {
      max = currentValue;
      maxIndex = i;
    }
  }
  return [max, maxIndex];
};
```

## 617. Merge Two Binary Trees

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```
var mergeTrees = function(root1, root2) {
    if(!root1 && !root2){
        return null;
    }else if(!root1 && root2){
        return root2;
    }else if(root1 && !root2){
        return root1;
    }else{
        const newRoot = new TreeNode(root1.val + root2.val);
        newRoot.left = mergeTrees(root1.left, root2.left);
        newRoot.right = mergeTrees(root1.right, root2.right);
        return newRoot;
    }
};
```

## 700. Search in a Binary Search Tree

### Node:

### Time Complexity && Space Complexity

- Time Complexity:
  - Best: O(log n)
  - Worst: O(n)
- Space Complexity: O(n)

```
var searchBST = function(root, val) {
    if(!root) return null;
    if(root.val === val){
        return root;
    }else if(root.val > val){
        return searchBST(root.left, val);
    }else{
        return searchBST(root.right, val);
    }
};
```

## 98. Validate Binary Search Tree

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)
  - Recursive Call Stack
    - Best: O(logn), the height of the tree is O(log n), and therefore the recursion depth is also O(log n)
    - Worst: O(n), the height of the tree is O(n), leading to a recursion depth of O(n)
  - Additional Memory: 0

```
var isValidBST = function(root) {
    if(!root){
        return false;
    }
    var isValid = function(root, minValue, maxValue){
        if(!root){
            return true;
        }
        if(root.val <= minValue || root.val >= maxValue){
            return false;
        }
        return isValid(root.left, minValue, Math.min(root.val, maxValue)) && isValid(root.right, Math.max(minValue, root.val), maxValue);
    }

    return isValid(root.left, Number.MIN_SAFE_INTEGER, root.val) && isValid(root.right, root.val, Number.MAX_SAFE_INTEGER);
};
```
