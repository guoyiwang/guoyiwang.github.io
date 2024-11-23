---
title: Day29-Greedy03
date: 2024-11-23 07:22:31
tags:
  - Greedy
categories:
  - Algorithm
---

## 134. Gas Station

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```js
var canCompleteCircuit = function (gas, cost) {
  let start = 0;
  let currSum = 0;
  let totalSum = 0;
  for (let i = 0; i < gas.length; i++) {
    currSum += gas[i] - cost[i];
    totalSum += gas[i] - cost[i];
    if (currSum < 0) {
      currSum = 0;
      start = i + 1;
    }
  }
  if (totalSum < 0) return -1;
  return start;
};
```

## 135. Candy

### Node:

    - Add candy from the left side and add from the right side

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(n)

```js
var candy = function (ratings) {
  const candyRes = new Array(ratings.length).fill(1);
  for (let i = 1; i < ratings.length; i++) {
    if (ratings[i] > ratings[i - 1]) {
      candyRes[i] = candyRes[i - 1] + 1;
    }
  }

  for (let i = ratings.length - 2; i >= 0; i--) {
    if (ratings[i] > ratings[i + 1]) {
      candyRes[i] = Math.max(candyRes[i], candyRes[i + 1] + 1);
    }
  }
  return candyRes.reduce((a, b) => a + b, 0);
};
```

## 860. Lemonade Change

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n)
- Space Complexity: O(1)

```js
var lemonadeChange = function (bills) {
  const moneyMap = { 5: 0, 10: 0, 20: 0 };
  for (const bill of bills) {
    if (bill === 5) {
      moneyMap["5"]++;
    } else if (bill === 10) {
      if (moneyMap["5"] > 0) {
        moneyMap["5"]--;
        moneyMap["10"]++;
      } else {
        return false;
      }
    } else if (bill === 20) {
      if (moneyMap["5"] > 0 && moneyMap["10"] > 0) {
        moneyMap["5"]--;
        moneyMap["10"]--;
        moneyMap["20"]++;
      } else if (moneyMap["5"] > 2) {
        moneyMap["5"] -= 3;
        moneyMap["20"]++;
      } else {
        return false;
      }
    }
  }
  return true;
};
```

## 406. Queue Reconstruction by Height

### Node:

### Time Complexity && Space Complexity

- Time Complexity: O(n^2) O(nlogn) + O(n^2)
- Space Complexity: O(n)

```js
var reconstructQueue = function (people) {
  people.sort((a, b) => {
    if (a[0] !== b[0]) {
      return b[0] - a[0];
    } else {
      return a[1] - b[1];
    }
  });
  const res = [];
  for (const [height, index] of people) {
    res.splice(index, 0, [height, index]);
  }
  return res;
};
```
