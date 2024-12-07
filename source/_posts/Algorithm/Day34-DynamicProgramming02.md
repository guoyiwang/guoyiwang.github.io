---
title: Day34-DynamicProgramming02
date: 2024-12-05 16:39:31
tags:
  - DynamicProgramming
categories:
  - Algorithm
---

## 62. Unique Paths

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(m*n)
- Space Complexity: O(m*n)

```js
var uniquePaths = function(m, n) {
    const map = new Array(m).fill().map((row) => new Array(n).fill(1));
    for(let i = 1; i < m; i++){
        for(let j = 1; j < n; j++){
            map[i][j] = map[i-1][j] + map[i][j-1];
        }
    }
    return map[m-1][n-1];
};
```

## 63. Unique Paths II

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(m*n)
- Space Complexity: O(m*n)

```js
/**
 * @param {number[][]} obstacleGrid
 * @return {number}
 */
var uniquePathsWithObstacles = function(obstacleGrid) {
    const rows = obstacleGrid.length;
    const cols = obstacleGrid[0].length;
    const pathCount = new Array(rows).fill().map((_)=> new Array(cols).fill(0));
    for(let j = 0; j < cols; j++){
        if(obstacleGrid[0][j] === 1){
            break;
        }else{
            pathCount[0][j] = 1;
        }
    }
    for(let i = 0; i < rows; i++){
        if(obstacleGrid[i][0] === 1){
            break;
        }else{
            pathCount[i][0] = 1;
        }
    }
    for(let i = 1; i < rows; i++){
        for(let j = 1; j < cols; j++){
            if(obstacleGrid[i][j] === 1){
                pathCount[i][j] = 0;
            }else{
                pathCount[i][j] = pathCount[i-1][j] + pathCount[i][j-1];
            }
        }
    }
    return pathCount[rows-1][cols-1];
};
```

## 343. Integer Break
### Node:
- Example of 10
    - 5*5
    - 4*6
    - 3*7
    - 2*8
    - 1*9
- The max product of 9
    - 5*4
    - 6*3
    - 7*2
    - 8*1

### Time Complexity && Space Complexity

- Time Complexity: O(n^2)
- Space Complexity: O(n)

```js
var integerBreak = function(n) {
    const arr = new Array(n+1).fill(0);
    arr[1] = 1;
    arr[2] = 1;
    for(let i = 3; i <= n; i++){
        const mid = Math.ceil(i/2);
        for(let integer = mid; integer < i; integer++){
            const product = Math.max(arr[integer], integer) * Math.max(arr[i-integer], i-integer);
            arr[i] = Math.max(product, arr[i]);
        }
    }
    return arr[n];
};
```

## 96. Unique Binary Search Trees

### Node:
- dp[4] = dp[3] * dp[0] + dp[2] * dp[1] + dp[1] * dp[2] + dp[0] * dp[3]
- except the root node, there are four way of the childs:
    - left: 3 nodes, right: 0 node
    - left: 2 nodes, right: 1 node
    - left: 1 nodes, right: 2 node
    - left: 0 nodes, right: 3 node
- dp[3] = dp[2] * dp[0] + dp[1] * dp[1] + dp[0] * dp[2]
- except the root node, there are three way of the childs:
    - left: 2 nodes, right: 0 node
    - left: 1 nodes, right: 1 node
    - left: 0 nodes, right: 2 node

### Time Complexity && Space Complexity

- Time Complexity: O(n^2)
- Space Complexity: O(n)

```js
var numTrees = function(n) {
    const arr = new Array(n+1).fill(0);
    arr[0] = 1;
    for(let i = 1; i <= n; i++){
        for(let j = 0; j < i; j++){// j is the count of the nodes on the left side of root node
            arr[i] += arr[j]*arr[i-j-1];
        }
    }
    return arr[n];
};
```
