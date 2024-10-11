---
title: Day21-BinaryTree08
date: 2024-10-11 13:07:19
tags:
  - BinaryTree
categories:
  - Algorithm
---

## 669. Trim a Binary Search Tree

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O()
    - Best case (balanced tree): O(log n).
    - Worst case (unbalanced tree): O(n).

```js
var trimBST = function(root, low, high) {
    if(!root){
        return null;
    }
    // if root.val < low, the left subtree of root will also less than low
    if(root.val < low){
        return trimBST(root.right, low, high);
    }
    // if root.val > high, the right subtree of root will also more than high
    if(root.val > high){
        return trimBST(root.left, low, high);
    }
    root.left = trimBST(root.left, low, high);
    root.right = trimBST(root.right, low, high);
    return root;
};
```

```js
var trimBST = function(root, low, high) {
    if(!root){
        return null;
    }
    if(root.val >= low && root.val <= high){
        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);
        return root;
    }else{
        if(!root.right && !root.left){
            return null;
        }else if(root.right && !root.left){
            return trimBST(root.right, low, high);
        }else if(!root.right && root.left){
            return trimBST(root.left, low, high);
        }else{
            const smallestNode = getSmallestNode(root.right);
            smallestNode.left = root.left;
            return trimBST(root.right, low, high);
        }
    }
};
```

## 108. Convert Sorted Array to Binary Search Tree

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(logn)
    - Call Stack Space: The recursion depth is proportional to the height of the tree. In the best-case scenario, the tree is balanced, and its height is O(log n). Therefore, the recursive calls will consume O(log n) space in the call stack.
    - Tree Node Space: Each element in the input array results in a TreeNode, so the total space used by the tree itself is O(n) for the n nodes.

```js
var sortedArrayToBST = function(nums) {
    var recusive = function(nums, left, right){
        if(left > right){
            return null;
        }
        const mid = Math.floor((left+right)/2);
        const root = new TreeNode(nums[mid]);
        root.left = recusive(nums, left, mid-1);
        root.right = recusive(nums, mid+1, right);
        return root;
    }
    return recusive(nums, 0, nums.length - 1);
};
```

## 538. Convert BST to Greater Tree

### Node:
- right, mid, left

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var convertBST = function(root) {
    let sum = 0;
    const recusive = function(root){
        if(!root){
            return null
        }
        let right = null;
        if(root.right){
            right = recusive(root.right);
        }
        sum += root.val;
        const newRoot = new TreeNode(sum, null, right);
        if(root.left){
            newRoot.left = recusive(root.left);
        }
        return newRoot;
    }
    return recusive(root);
};
```
