---
title: Day11-StackAndQueue02
date: 2024-09-16 22:25:31
tags:
  - Stack&Queue
  - Monotonic-Stack
  - Priority-Queue
categories:
  - Algorithm
---

## 150. Evaluate Reverse Polish Notation

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var evalRPN = function (tokens) {
  const stack = [];
  for (const char of tokens) {
    if (char !== "+" && char !== "-" && char !== "*" && char !== "/") {
      stack.push(Number(char));
    } else {
      const second = stack.pop();
      const first = stack.pop();
      if (char === "+") {
        stack.push(first + second);
      } else if (char === "-") {
        stack.push(first - second);
      } else if (char === "*") {
        stack.push(first * second);
      } else {
        stack.push(Math.trunc(first / second));
      }
    }
  }
  return stack[0];
};
```

## 239. Sliding Window Maximum

### Node:

- Could use priority queue or monotonic stack(decrease)
  - monotonic stack: only keep the unique value which decrease, not save the equal value
- Key is the know when to remove the previous value out of k scope

### Time Complexity && Space Complexity

- Monotonic Stack(decrease)
  - Time Complexity: O(n^2)
    - stack.shift() is n in worse case
  - Space Complexity: O(n)

```js
var maxSlidingWindow = function (nums, k) {
  if (k === 1) return nums;
  const stack = [];
  const res = [];
  for (let i = 0; i < nums.length; i++) {
    while (stack.length >= k) {
      stack.shift();
    }
    while (stack.length > 0 && nums[i] >= stack[stack.length - 1][0]) {
      stack.pop();
    }
    stack.push([nums[i], i]);
    if (i >= k - 1) {
      while (i - k >= stack[0][1]) {
        stack.shift();
      }
      res.push(stack[0][0]);
    }
  }
  return res;
};
```

- Priority Queue
  - Time Complexity: O(nlogk)
  - Space Complexity: O(n)

```js
var maxSlidingWindow = function (nums, k) {
  const maxHeap = new PriorityQueue({ compare: (e1, e2) => e2[1] - e1[1] });
  const removedMap = new Map();
  const res = [];

  for (let i = 0; i < k; i++) {
    maxHeap.enqueue([i, nums[i]]);
  }
  res.push(maxHeap.front()[1]);
  for (let i = k; i < nums.length; i++) {
    maxHeap.enqueue([i, nums[i]]);
    removedMap.set(i - k, nums[i - k]);
    while (removedMap.has(maxHeap.front()[0])) {
      maxHeap.dequeue();
    }
    res.push(maxHeap.front()[1]);
  }
  return res;
};
```

## 347. Top K Frequent Elements

### Node:

- Priority Queue: O(nlogk)(enqueue is logk since size of heap is k or less than k)

### Time Complexity && Space Complexity

- Priority Queue

  - Time Complexity: O(nlogk)
  - Space Complexity: O(n)

    ```
    var topKFrequent = function(nums, k){
        const heap = new PriorityQueue({compare: (a,b) => a[1] - b[1]});
        const frequentMap = new Map();
        const res = [];
        for(const num of nums){
            if(frequentMap.has(num)){
                frequentMap.set(num, frequentMap.get(num) + 1);
            }else{
                frequentMap.set(num, 1);
            }
        }
        // O(nlogk)(enqueue is logk since size of heap is k or less than k)
        for(const [key, value] of frequentMap){
            heap.enqueue([key, value]);
            if(heap.size() > k){
                heap.dequeue();
            }
        }
        while(heap.size() > 0){
            res.push(heap.dequeue()[0]);
        }
        return res;
    }
    ```

- Array sort

  - Time Complexity: O(nlog(n))
  - Space Complexity: O(n)

    ```js
    var topKFrequent = function (nums, k) {
      const frequentMap = new Map();
      const arr = [];
      const res = [];
      for (const num of nums) {
        if (frequentMap.has(num)) {
          frequentMap.set(num, frequentMap.get(num) + 1);
        } else {
          frequentMap.set(num, 1);
        }
      }

      frequentMap.forEach((value, key) => arr.push([key, value]));
      // Olog(n)
      arr.sort((a, b) => b[1] - a[1]);
      for (let i = 0; i < k; i++) {
        res.push(arr[i][0]);
      }
      return res;
    };
    ```
