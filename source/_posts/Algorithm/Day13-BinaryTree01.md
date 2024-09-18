---
title: Day13-BinaryTree01
date: 2024-09-17 07:42:02
tags:
---

## 144. Binary Tree Preorder Traversal

### Node:

- Preorder: mid, left, right
- Iterate: push the right node, then push the left node

### Time Complexity && Space Complexity

- Recursive

  - Time Complexity: O(n)
  - Space Complexity: O(n)

  ```js
  var preorderTraversal = function (root) {
    const ans = [];
    function traversal(root) {
      if (!root) return;
      ans.push(root.val);
      traversal(root.left);
      traversal(root.right);
    }
    traversal(root);
    return ans;
  };
  ```

- Iterate

  - Time Complexity: O(n)
  - Space Complexity: O(n)

  ```js
  var preorderTraversal = function (root) {
    if (!root) return [];
    const stack = [root];
    const ans = [];
    while (stack.length > 0) {
      const node = stack.pop();
      ans.push(node.val);
      if (node.right) {
        stack.push(node.right);
      }
      if (node.left) {
        stack.push(node.left);
      }
    }
    return ans;
  };
  ```

## 145. Binary Tree Postorder Traversal

### Node:

- Postorder: left, right, mid
  - Do preorder first, mid, right, left, means push the [left, right], then pop [right, left]
  - then reverse the ans

### Time Complexity && Space Complexity

- Recursive

  - Time Complexity: O(n)
  - Space Complexity: O(n)

  ```js
  var postorderTraversal = function (root) {
    const ans = [];
    function traversal(root) {
      if (!root) return;
      if (root.left) {
        traversal(root.left);
      }
      if (root.right) {
        traversal(root.right);
      }
      ans.push(root.val);
    }
    traversal(root);
    return ans;
  };
  ```

- Iterate

  - Time Complexity: O(n)
  - Space Complexity: O(n)

  ```js
  var postorderTraversal = function (root) {
    if (!root) return [];
    const stack = [root];
    const ans = [];
    while (stack.length > 0) {
      const node = stack.pop();
      ans.push(node.val);
      if (node.left) {
        stack.push(node.left);
      }
      if (node.right) {
        stack.push(node.right);
      }
    }
    return ans.reverse();
  };
  ```

## 94. Binary Tree Inorder Traversal

### Node:

- left, mid, right
- Iterate
  - Push the root, root.left, root.left.left until the leaf
  - when reach the leaf, pop the node from stack
  - check the popNode.right

### Time Complexity && Space Complexity

- Recursive

  - Time Complexity: O(n)
  - Space Complexity: O(n)

  ```js
  var inorderTraversal = function (root) {
    const ans = [];
    function traversal(root) {
      if (!root) return;
      if (root.left) {
        traversal(root.left);
      }
      ans.push(root.val);
      if (root.right) {
        traversal(root.right);
      }
    }
    traversal(root);
    return ans;
  };
  ```

- Iterate

  - Time Complexity: O(n)
  - Space Complexity: O(n)

  ```js
  var inorderTraversal = function (root) {
    if (!root) return [];
    const stack = [];
    const ans = [];
    let curr = root;
    while (stack.length > 0 || curr) {
      if (curr) {
        stack.push(curr);
        curr = curr.left;
      } else {
        curr = stack.pop();
        ans.push(curr.val);
        curr = curr.right;
      }
    }
    return ans;
  };
  ```

## Binary Tree Depth:

### Node:

- Use queue, and use length for loop

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

#### 102. Binary Tree Level Order Traversal

```js
var levelOrder = function (root) {
  if (!root) return [];
  const queue = [root];
  const ans = [];
  while (queue.length > 0) {
    const length = queue.length;
    const levelAns = [];
    for (let i = 0; i < length; i++) {
      const node = queue.shift();
      levelAns.push(node.val);
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
    }
    ans.push(levelAns);
  }
  return ans;
};
```

#### 107. Binary Tree Level Order Traversal II

```js
var levelOrderBottom = function (root) {
  if (!root) return [];
  const queue = [root];
  const ans = [];
  while (queue.length > 0) {
    const length = queue.length;
    const levelAns = [];
    for (let i = 0; i < length; i++) {
      const node = queue.shift();
      levelAns.push(node.val);
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
    }
    ans.push(levelAns);
  }
  return ans.reverse();
};
```

#### 199. Binary Tree Right Side View

```js
var rightSideView = function (root) {
  if (!root) return [];
  const queue = [root];
  const ans = [];
  while (queue.length > 0) {
    let length = queue.length;
    while (length > 0) {
      const node = queue.shift();
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
      length--;
      if (length === 0) {
        ans.push(node.val);
      }
    }
  }
  return ans;
};
```

#### 637. Average of Levels in Binary Tree

```js
var averageOfLevels = function (root) {
  if (!root) return [];
  const queue = [root];
  const ans = [];
  while (queue.length > 0) {
    const length = queue.length;
    let sum = 0;
    for (let i = 0; i < length; i++) {
      const node = queue.shift();
      sum += node.val;
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
    }
    ans.push(sum / length);
  }
  return ans;
};
```

#### 429. N-ary Tree Level Order Traversal

```js
var levelOrder = function (root) {
  if (!root) return [];
  const queue = [root];
  const ans = [];
  while (queue.length > 0) {
    const length = queue.length;
    const levelAns = [];
    for (let i = 0; i < length; i++) {
      const node = queue.shift();
      levelAns.push(node.val);
      for (const child of node.children) {
        child && queue.push(child);
      }
    }
    ans.push(levelAns);
  }
  return ans;
};
```

#### 515. Find Largest Value in Each Tree Row

```js
var largestValues = function (root) {
  if (!root) return [];
  const queue = [root];
  const ans = [];
  while (queue.length > 0) {
    const length = queue.length;
    let maxValue = Number.MIN_SAFE_INTEGER;
    for (let i = 0; i < length; i++) {
      const node = queue.shift();
      maxValue = Math.max(maxValue, node.val);
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
    }
    ans.push(maxValue);
  }
  return ans;
};
```

#### 116. Populating Next Right Pointers in Each Node

```js
var connect = function (root) {
  if (!root) return null;
  const queue = [root];
  while (queue.length > 0) {
    let length = queue.length;
    while (length > 0) {
      const node = queue.shift();
      length--;
      if (length === 0) {
        node.next = null;
      } else {
        node.next = queue[0];
      }
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
    }
  }
  return root;
};
```

#### 117. Populating Next Right Pointers in Each Node II

```js
var connect = function (root) {
  if (!root) return null;
  const queue = [root];
  while (queue.length > 0) {
    let length = queue.length;
    while (length > 0) {
      const node = queue.shift();
      length--;
      if (length === 0) {
        node.next = null;
      } else {
        node.next = queue[0];
      }
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
    }
  }
  return root;
};
```

#### 104. Maximum Depth of Binary Tree

```js
var maxDepth = function (root) {
  if (!root) return 0;
  const queue = [root];
  let maxDepth = 0;
  while (queue.length > 0) {
    const length = queue.length;
    for (let i = 0; i < length; i++) {
      const node = queue.shift();
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
    }
    maxDepth++;
  }
  return maxDepth;
};
```

#### 111. Minimum Depth of Binary Tree

```js
var minDepth = function (root) {
  if (!root) return 0;
  const queue = [root];
  let depth = 0;
  let minDepth = Number.MAX_SAFE_INTEGER;
  while (queue.length > 0) {
    const length = queue.length;
    depth++;
    for (let i = 0; i < length; i++) {
      const node = queue.shift();
      if (!node.left && !node.right) {
        minDepth = Math.min(minDepth, depth);
      }
      if (node.left) {
        queue.push(node.left);
      }
      if (node.right) {
        queue.push(node.right);
      }
    }
  }
  return minDepth;
};
```
