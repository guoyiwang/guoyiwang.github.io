---
title: Day15-BinaryTree03
date: 2024-09-19 23:55:55
tags:
  - BinaryTree
categories:
  - Algorithm
---

## 110. Balanced Binary Tree

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var isBalanced = function(root) {
    return countHeight(root) === -1 ? false : true;
};

var countHeight = function(root) {
    if(!root) return 0;
    const leftHeight = countHeight(root.left);
    if(leftHeight === -1){
        return -1;
    }
    const rightHeight = countHeight(root.right);
    if(rightHeight === -1){
        return -1;
    }
    if(Math.abs(leftHeight - rightHeight) <= 1){
        return 1 + Math.max(leftHeight, rightHeight);
    }else{
        // Not valid
        return -1;
    }
}
```

## 257. Binary Tree Paths

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O()
- Space Complexity: O()

```js
var binaryTreePaths = function(root) {
    if(!root) return [];
    const ans = [];
    getPath(root, "", "", ans);
    return ans;
};

var getPath = function(root, leftPath, rightPath, ans){
    if(!root) return;
    const isLeaf = !root.left && !root.right;
    leftPath += !isLeaf ? `${root.val}->` : `${root.val}`;
    rightPath += !isLeaf ? `${root.val}->`: `${root.val}`;
    if(isLeaf){
        return ans.push(leftPath);
    }
    getPath(root.left, leftPath, rightPath, ans);
    getPath(root.right, leftPath, rightPath, ans);
}
```

```js
var binaryTreePaths = function(root) {
    if(!root) return [];
    const stack = [[root, `${root.val}`]];
    const ans = [];
    while(stack.length > 0){
        const [node, path] = stack.pop();
        if(!node.left && !node.right){
            ans.push(path);
            continue;
        }
        if(node.left){
            stack.push([node.left, `${path}->${node.left.val}`]);
        }
        if(node.right){
            stack.push([node.right, `${path}->${node.right.val}`]);
        }
    }
    return ans;
}
```

## 404. Sum of Left Leaves

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var sumOfLeftLeaves = function(root) {
    let sum = 0;
    var traversal = function(root, isLeft){
        if(!root) return;
        if(root.left){
            traversal(root.left, true);
        }
        if(root.right){
            traversal(root.right, false);
        }
        if(isLeft && !root.left && !root.right){
            sum += root.val;
        }
    }
    traversal(root, false);
    return sum;
};
```

```js
var sumOfLeftLeaves = function(root){
    if(!root) return 0;
    const stack = [[root, false]];
    let sum = 0;
    while(stack.length > 0){
        const [node, isLeft] = stack.pop();
        if(isLeft && !node.left && !node.right){
            sum += node.val;
            continue;
        }
        if(node.left){
            stack.push([node.left, true]);
        }
        if(node.right){
            stack.push([node.right, false]);
        }
    }
    return sum;
}
```

## 222. Count Complete Tree Nodes

### Node:
- Best case: log(n)
- Worse case: log(n) * log(n)
    - Only one node on the left level which is on the most left
    - Every node on the most left side on every level(logn) * need be checked for the leftHeigt, rightHeight(logn)


### Time Complexity && Space Complexity

- Time Complexity: O(log(n) * log(n))
- Space Complexity: O(logn)

```js
var countNodes = function(root) {
    if(!root) return 0;
    let leftNode = root;
    let leftHeight = 0;
    let rightNode = root;
    let rightHeight = 0;
    while(leftNode.left){
        leftHeight += 1;
        leftNode = leftNode.left;
    }
    while(rightNode.right){
        rightHeight += 1;
        rightNode = rightNode.right;
    }
    if(leftHeight === rightHeight){
        return Math.pow(2, leftHeight+1) - 1;
    }else{
        return 1 + countNodes(root.left) + countNodes(root.right);
    }
};
```
