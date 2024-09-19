---
title: Day14-BinaryTree02
date: 2024-09-18 22:20:47
ttags:
  - BinaryTree
categories:
  - Algorithm
---

## 226. Invert Binary Tree

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var invertTree = function (root) {
  if (!root) return null;
  let temp = root.right;
  root.right = root.left;
  root.left = temp;
  root.left && invertTree(root.left);
  root.right && invertTree(root.right);
  return root;
};
```

## 101. Symmetric Tree

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var isSymmetric = function (root) {
  if (!root) return false;
  return isValSame(root.left, root.right);
};

var isValSame = function (left, right) {
  if (left && right) {
    if (left.val !== right.val) {
      return false;
    } else {
      return (
        isValSame(left.left, right.right) && isValSame(left.right, right.left)
      );
    }
  } else if ((!left && right) || (left && !right)) {
    return false;
  } else {
    return true;
  }
};
```

```js
var isSymmetric = function (root) {
  if (!root) return false;
  const queue = [root.left, root.right];
  while (queue.length > 0) {
    const leftNode = queue.shift();
    const rightNode = queue.shift();
    if (!leftNode && !rightNode) {
      continue;
    }
    if (!leftNode || !rightNode || leftNode.val !== rightNode.val) {
      return false;
    }
    queue.push(leftNode.left);
    queue.push(rightNode.right);
    queue.push(leftNode.right);
    queue.push(rightNode.left);
  }
  return true;
};
```
