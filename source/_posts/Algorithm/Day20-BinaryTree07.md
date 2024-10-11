---
title: Day20-BinaryTree07
date: 2024-10-11 13:07:03
tags:
  - BinaryTree
categories:
  - Algorithm
---

## 235. Lowest Common Ancestor of a Binary Search Tree

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(logn)
  - Best/average case (balanced BST): O(log n)
  - Worst case (unbalanced BST): O(n)
  - In a balanced BST, the height h is logarithmic in terms of the number of nodes n, meaning h = O(log n).
  - In the worst case, if the tree is skewed (completely unbalanced), the height of the tree could be O(n) where n is the total number of nodes.
- Space Complexity: O(logn)
  - Best/average case (balanced BST): O(log n)
  - Worst case (unbalanced BST): O(n)

```js
var lowestCommonAncestor = function (root, p, q) {
  if (!root) return null;
  if (root.val > p.val && root.val > q.val) {
    return lowestCommonAncestor(root.left, p, q);
  } else if (root.val < p.val && root.val < q.val) {
    return lowestCommonAncestor(root.right, p, q);
  } else {
    return root;
  }
};
```

## 701. Insert into a Binary Search Tree

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O()
  - Best/average case (balanced BST): O(log n)
  - Worst case (unbalanced BST): O(n)
- Space Complexity: O()
  - Best/average case (balanced BST): O(log n)
  - Worst case (unbalanced BST): O(n)

```js
var insertIntoBST = function (root, val) {
  if (!root) {
    return new TreeNode(val);
  }
  if (root.val > val) {
    root.left = insertIntoBST(root.left, val);
  }
  if (root.val < val) {
    root.right = insertIntoBST(root.right, val);
  }
  return root;
};
```

## 450. Delete Node in a BST

### Node:
- Find the smallest node, add the left subtree of the deleted node to left of the smallest node
- use root.right to replace the root to be deleted

### Time Complexity && Space Complexity

- Time Complexity: O()
  - Best/average case (balanced BST): O(log n)
  - Worst case (unbalanced BST): O(n)
  - Two parts are time-consuming
    - Traversing the Tree to Find the Node: O(log n)
    - Finding the Smallest Node in the Right Subtree (If Necessary): O(log n)

- Space Complexity: O()
  - Best/average case (balanced BST): O(log n)
  - Worst case (unbalanced BST): O(n)

```js
var deleteNode = function(root, key) {
    if(!root) return null
    if(root.val > key){
        root.left = deleteNode(root.left, key);
    }else if(root.val < key){
        root.right = deleteNode(root.right, key);
    }else{
        if(root.right){
            const smallestNode = findSmallestNode2(root.right);
            smallestNode.left = root.left;
            return root.right;
        }else{
            return root.left;
        }
    }
    return root;
};

var findSmallestNode2 = function(root){
    while(root.left){
        root = root.left;
    }
    return root;
}
```
