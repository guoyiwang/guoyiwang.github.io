---
title: Day25-BackTracking04
date: 2024-10-15 22:03:34
tags:
  - BackTracking
categories:
  - Algorithm
---

## 491. Non-decreasing Subsequences

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O()
- Space Complexity: O()

```js
var findSubsequences = function (nums) {
  const res = [];
  const backTracking = (index, path) => {
    if (index > nums.length) {
      return;
    }
    if (path.length >= 2) {
      res.push(path);
    }
    const visited = [];
    for (let i = index; i < nums.length; i++) {
      if (
        // Among the nodes on the same level under the same parent node, duplicate node should be skipped.
        (path.length > 0 && nums[i] < path[path.length - 1]) ||
        visited[nums[i] + 100]
      ) {
        continue;
      }
      visited[nums[i] + 100] = true;
      backTracking(i + 1, [...path, nums[i]]);
      // not need to revert visited[nums[i]+100] = false; since for the nodes on the same level under the same parent node, there always is a new visited array
    }
  };
  backTracking(0, []);
  return res;
};
```

## 46. Permutations

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O()
- Space Complexity: O()

```js
var permute = function (nums) {
  const res = [];
  const visited = new Array(nums.length).fill(0);
  const backTracking = function (path) {
    if (path.length === nums.length) {
      return res.push(path);
    }
    for (let i = 0; i < nums.length; i++) {
      if (!visited[i]) {
        visited[i] = true;
        backTracking([...path, nums[i]]);
        visited[i] = false;
      }
    }
  };
  backTracking([]);
  return res;
};
```

## 47. Permutations II

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O()
- Space Complexity: O()

```js
var permuteUnique = function (nums) {
  nums.sort((a, b) => a - b);
  const res = [];
  const visited = new Array(nums.length).fill(0);
  const backTracking = function (path) {
    if (path.length === nums.length) {
      return res.push(path);
    }
    for (let i = 0; i < nums.length; i++) {
      // For the same tree level nodes, if the previous element (i.e., nums[i-1]) is same as current and didn't be used, which mean there are two duplicate element, we need skip it.
      if (i > 0 && nums[i] === nums[i - 1] && !visited[i - 1]) {
        continue;
      }
      if (!visited[i]) {
        visited[i] = true;
        backTracking([...path, nums[i]]);
        visited[i] = false;
      }
    }
  };
  backTracking([]);
  return res;
};
```

## 332. Reconstruct Itinerary

### Node:

- Why backtracking not work? (couldn't pass for test case)
  ```js
  visitedMap {
    JFK: [ [ 'ATL', false ], [ 'SFO', false ] ],
    SFO: [ [ 'JFK', false ] ],
    ATL: [
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ],
      [ 'AAA', false ], [ 'AAA', false ]
    ],
    AAA: [
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ],
      [ 'BBB', false ], [ 'BBB', false ]
    ],
    BBB: [
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ],
      [ 'ATL', false ], [ 'ATL', false ]
    ]
  }
  ```
  - The infinite loop in backtracking algorithm is due to repeated exploration of **cyclic paths** without a mechanism to prevent revisiting the same set of nodes
  - "ATL" -> "AAA" -> "BBB" -> "ATL".
  - Once the cycle repeats and all destinations from "ATL" are exhausted, the algorithm starts to backtrack.
  - During backtracking, each ticket used in the cycle ("ATL" -> "AAA", "AAA" -> "BBB", etc.) is unmarked.
  - After unmarking the tickets, the algorithm tries to find other routes.
  - Since the tickets used in the cycle have been unmarked, it ends up choosing the same cycle again: "ATL" -> "AAA" -> "BBB" -> "ATL".
  - This creates a loop where the algorithm keeps exploring the same set of nodes repeatedly without ever finding a way to use the remaining tickets in the graph.
- Why backtracking slow than DFS(Hierholzer's Algorithm)

  - DFS (Hierholzer's Algorithm): designed to construct Eulerian paths or circuits in a graph. Visits every edge exactly once without backtracking because it "knows" all the edges are needed for a valid path. It is optimized to use each ticket exactly once, thereby preventing revisiting or redundant explorations.

  - Backtracking: more general-purpose problem-solving strategy. It is designed to explore all possible paths and revert changes if a path does not lead to a solution. It’s great for scenarios where we don’t know the structure of the solution space or when there could be multiple solutions, but it’s not optimized for graphs that inherently form a single complete path, such as Eulerian paths.

### Time Complexity && Space Complexity

- Time Complexity: O()
- Space Complexity: O()

// DFS (Hierholzer's Algorithm)

```js
var findItinerary = function (tickets) {
  const map = {};
  const res = [];
  for (const [depart, arrive] of tickets) {
    if (!map[depart]) {
      map[depart] = [arrive];
    } else {
      map[depart].push(arrive);
    }
  }
  for (const [_, value] of Object.entries(map)) {
    value.sort().reverse();
  }
  const dfs = (currentStop) => {
    const nextStops = map[currentStop];
    while (nextStops && nextStops.length > 0) {
      // smallest lexical order
      const nextStop = nextStops.pop();
      dfs(nextStop);
    }
    // start save when reach the end of itinerary
    res.push(currentStop);
  };
  dfs("JFK");
  return res.reverse();
};
```

// Backtracking, not pass one test case

```js
var findItinerary = function (tickets) {
  const visitedMap = {};
  const requiredPathLength = tickets.length + 1;
  for (const [depart, arrive] of tickets) {
    if (visitedMap[depart]) {
      visitedMap[depart].push([arrive, false]);
    } else {
      visitedMap[depart] = [[arrive, false]];
    }
  }
  for (const [key, value] of Object.entries(visitedMap)) {
    value.sort((a, b) => a[0].localeCompare(b[0]));
  }
  const ans = [];
  const backTracking = (path) => {
    if (path.length === requiredPathLength) {
      ans.push(path);
      return true;
    }
    const nextStops = visitedMap[path[path.length - 1]];
    if (!nextStops) {
      return false;
    }
    for (const nextStop of nextStops) {
      if (!nextStop[1]) {
        nextStop[1] = true;
        if (backTracking([...path, nextStop[0]])) {
          return true;
        }
        nextStop[1] = false;
      }
    }
  };
  backTracking(["JFK"]);
  return ans[0];
};
```

## 51. N-Queens

### Node:
- Check every cell of the cheese which above the current node

### Time Complexity && Space Complexity

- Time Complexity: O(n×n!)
  - Number of recursive calls： n×(n−1)×(n−2)×…×1=n! worst case
  - isValid: O(n)
- Space Complexity: O(T(n)×n^2).  T(n) number of valid cheese
  - cheese board: O(n^2)
  - recursion stack space is O(n)
  - result space: O(T(n)×n^2).

```js
var solveNQueens = function(n) {
    const cheese = new Array(n).fill(0).map(()=>new Array(n).fill("."));
    const res = [];
    const dfs = (currentRow) => {
        if(currentRow === n){
            return res.push(cheese.map((arr)=>arr.join("")));
        }
        for(let i = 0; i < cheese[currentRow].length; i++){
            if(isValid(currentRow, i, cheese, n)){
                cheese[currentRow][i] = "Q";
                dfs(currentRow+1);
                cheese[currentRow][i] = ".";
            }
        }
    }
    dfs(0);
    return res;
};
// [row, col]
// [row+1, col-1] [row-1, col+1]
// [row+1, col -1]
var isValid = (row, col, board, n) => {
    // check there is Q in the column
    for(let i = 0; i < n; i++){
        if(board[i][col] === "Q"){
            return false;
        }
    }
    // In 135 degree, the node on the top has Q or not
    for(let i = row -1, j = col-1; i>=0 && j>= 0; i--, j--){
        if(board[i][j] === "Q"){
            return false;
        }
    }
    for(let i = row - 1, j = col+1; i >= 0 && j < n; i--, j++){
        if(board[i][j] === "Q"){
            return false;
        }
    }
    return true;
}
```

## 37

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O() (n*n*9)^n *n
  - recusive: O(9^m) m is the empty cell
  - isValid: O(1) 9+9+9
- Space Complexity: O(m)
  - recusive depty: O(m) m is the empty cell
```js
var solveSudoku = function(board) {
    function isValid(row, col, val, board) {
        let len = board.length
        // no duplicate in same row
        for(let i = 0; i < len; i++) {
            if(board[row][i] === val) {
                return false
            }
        }
        // no duplicate in same column
        for(let i = 0; i < len; i++) {
            if(board[i][col] === val) {
                return false
            }
        }
        let startRow = Math.floor(row / 3) * 3
        let startCol = Math.floor(col / 3) * 3

        for(let i = startRow; i < startRow + 3; i++) {
            for(let j = startCol; j < startCol + 3; j++) {
                if(board[i][j] === val) {
                    return false
                }
            }
        }

        return true
    }
    const backTracking = () => {
        const colLength = board[0].length;
        const rowLength = board.length;
        for(let i = 0; i < rowLength; i++){
            for(let j = 0; j < colLength; j++){
                if(board[i][j] === "."){
                    for(let value = 1; value <= 9; value++){
                        if(isValid(i, j, `${value}`, board)){
                            board[i][j] = `${value}`;
                            if(backTracking()){
                                return true;
                            }
                            board[i][j] = ".";
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }
    backTracking();
    return board;
};
```
