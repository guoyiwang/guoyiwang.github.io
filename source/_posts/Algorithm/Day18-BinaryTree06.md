---
title: Day18-BinaryTree06
date: 2024-10-11 13:06:46
tags:
  - BinaryTree
categories:
  - Algorithm
---

## 530. Minimum Absolute Difference in BST

### Node:
- Find the max and min of every node
- Calculate the absolue diff for every node by the min and max `res = Math.min(res, rootVal - min, max - rootVal);`

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var getMinimumDifference = function (root) {
  let res = Number.MAX_SAFE_INTEGER;
  var recusive = function (root, min, max) {
    if (!root) return;
    const rootVal = root.val;
    res = Math.min(res, rootVal - min, max - rootVal);
    if (root.left) {
      recusive(root.left, min, Math.min(max, root.val));
    }
    if (root.right) {
      recusive(root.right, Math.max(min, root.val), max);
    }
  };
  recusive(root, Number.MIN_SAFE_INTEGER, Number.MAX_SAFE_INTEGER);
  return res;
};
```

## 501. Find Mode in Binary Search Tree

### Node:
- Since there is a BST and the left subtree less than or equal to the root, the right subtree greater than or equal to the node's key.
- We need use left, mid, right inorder to check the duplicate the node
- Use maxCount and preNode to count to reduce the Space Complexity to 1(Assume that the implicit stack space incurred due to recursion does not count)

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var findMode = function(root) {
    const res = [];
    let maxCount = 0;
    let count = 0;
    let preNode = null;

    var recusive = function(root){
        if(!root) return;
        recusive(root.left);
        // start from the most left leaf node
        if(preNode && preNode.val === root.val){
            count++;
        }else{
            count = 1;
        }
        preNode = root;
        if(count >  maxCount){
            maxCount = count;
            res.length = 0;
        }
        if(count === maxCount){
            res.push(root.val);
        }
        recusive(root.right);
    }
    recusive(root);
    return res;
};
```

## 236. Lowest Common Ancestor of a Binary Tree

### Node:
- Postorder: left, right, mid
- Need know the left or right first
    - If left or right not include p or q, root will be null
    - If left or right, one is p or q, return this one
    - If left is p, right is q, return the root

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var lowestCommonAncestor = function(root, p, q) {
    if(!root) return null;
    if(root === p || root === q){
        return root;
    }
    const leftNode = lowestCommonAncestor(root.left, p, q);
    const rightNode = lowestCommonAncestor(root.right, p, q);
    if(leftNode && rightNode){
        return root;
    }else{
        return leftNode || rightNode;
    }
};
```
