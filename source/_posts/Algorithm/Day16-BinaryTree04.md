---
title: Day16-BinaryTree04
date: 2024-10-03 17:33:17
tags:
  - BinaryTree
categories:
  - Algorithm
---

## 106. Construct Binary Tree from Inorder and Postorder Traversal

### Node:

- Get root from the postorder which is always the last one
  - Left root index in postOrder: `rootIndexinPost - (inorderRight - inorderMid) - 1`// rootIndex - rightChildsCount - 1
  - Right root index in postOrder: `rootIndexinPost - 1`
- Use root in inoroder to know the left childs and right childs

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var buildTree = function (inorder, postorder) {
  const inorderMap = {};
  for (let i = 0; i < inorder.length; i++) {
    inorderMap[inorder[i]] = i;
  }
  const recusive = function (inorderLeft, inorderRight, rootIndexinPost) {
    const rootVal = postorder[rootIndexinPost];
    const root = new TreeNode(rootVal);
    const inorderMid = inorderMap[rootVal];
    if (inorderMid > inorderLeft) {
      root.left = recusive(
        inorderLeft,
        inorderMid - 1,
        rootIndexinPost - (inorderRight - inorderMid) - 1
      );
    }
    if (inorderMid < inorderRight) {
      root.right = recusive(inorderMid + 1, inorderRight, rootIndexinPost - 1);
    }
    return root;
  };

  return recusive(0, inorder.length - 1, postorder.length - 1);
};
```

## 513. Find Bottom Left Tree Value

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

#### Recusive

```js
var findBottomLeftValue = function (root) {
  if (!root) return null;
  const leftNodeMap = new Map();
  let maxHeight = Number.MIN_SAFE_INTEGER;
  var traversl = function (root, height) {
    if (!root) return;
    if (!root.left && !root.right) {
      if (!leftNodeMap.has(height)) {
        maxHeight = Math.max(maxHeight, height);
        leftNodeMap.set(height, root.val);
      }
      return;
    }
    if (root.left) {
      traversl(root.left, height + 1);
    }
    if (root.right) {
      traversl(root.right, height + 1);
    }
  };
  traversl(root, 0);
  return leftNodeMap.get(maxHeight);
};
```

#### BFS queue

```js
var findBottomLeftValue = function (root) {
  if (!root) return;
  let ans = 0;
  const queue = [root];
  while (queue.length > 0) {
    const length = queue.length;
    const levelValue = [];
    for (let i = 0; i < length; i++) {
      const node = queue.shift();
      levelValue.push(node.val);
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
    }
    ans = levelValue[0];
  }
  return ans;
};
```

## 112. Path Sum

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

#### Recusive

```js
var hasPathSum = function (root, targetSum) {
  if (!root) return false;
  var traversal = function (root, sum) {
    sum += root.val;
    if (!root.left && !root.right) {
      if (sum === targetSum) {
        return true;
      } else {
        return false;
      }
    }
    let isLeftValid = false;
    let isRightValid = false;
    if (root.left) {
      isLeftValid = traversal(root.left, sum);
      if (isLeftValid) {
        return true;
      }
    }
    if (root.right) {
      isRightValid = traversal(root.right, sum);
      if (isRightValid) {
        return true;
      }
    }
    return isLeftValid || isRightValid;
  };
  return traversal(root, 0);
};
```

#### DFS(stack)

```js
var hasPathSum = function (root, targetSum) {
  if (!root) return false;
  const stack = [[root, root.val]];
  while (stack.length > 0) {
    const [node, sum] = stack.pop();
    if (!node.left && !node.right && sum === targetSum) {
      return true;
    }
    if (node.left) {
      stack.push([node.left, sum + node.left.val]);
    }
    if (node.right) {
      stack.push([node.right, sum + node.right.val]);
    }
  }
  return false;
};
```
