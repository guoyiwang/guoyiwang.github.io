---
title: AlgorithmSummary.md
date: 2024-09-10 12:24:44
tags:
  - Summary
categories:
  - Algorithm
---

## String(Immutable in JS)
### Common solutions
- Combine two string, check the combined include the orignal one
- Reverse the whole sentence and reverse the every word, with start and end pointer
- Remove target element, with fast and slow pointers, fast skip the target, slow point to the target, and then `arr[slowIndex] = arr[fastIndex]`, remove the target element
- KMP

#### KMP
```
val findSubString = function(haystack, needle){
  const getNext = function(needle){
    const next = [];
    let j = 0;
    next.push(j);
    for(let i = 1; i < needle.length; i++){
      while(j > 0 && needle[i] !== needle[j]){
        j = next[j-1];
      }
      if(needle[i] === needle[j]){
        j++;
      }
      next.push(j);
    }
    return next;
  }
  const next = getNext(needle);
  let j = 0;
  for(let i = 0; i < haystack.length; i++){
    while(j > 0 && haystack[i] !== needle[j]){
      j = next[j-1];
    }
    if(haystack[i] === needle[j]){
      j++;
    }
    if(j === needle.length){
      return i+1-needle.length;
    }
  }
  return -1;
}
```

## Stack && Queue(Immutable in JS)

### Note
- arr.push(value)// return the length of arr
- arr.shift() // O(n)
- Use if/not for using map to count frequent of value, don't use Conditional (ternary) operator
  - NOT USE: 
    - `map.set(key, map.has(key) ? map.get(key).push(index) : [index]);`
    - `obj[key] = obj[key] === undefined? [index] : [...obj[key], index];`
      - I worte this in interview, BIG MISTAKE `obj[key] = obj[key] === undefined? [index] : obj[key].push(index);`

#### Priority Queue

```
class myPriorityQueue{
    constructor({compare = (a,b) => a-b}){
        this.compare = compare;
        this.data = [];
    }
    swap(i, j){
        [this.data[i], this.data[j]] = [this.data[j], this.data[i]];
    }
    size(){
        return this.data.length;
    }
    peak(){
        if(this.size() === 0) return null;
        return this.data[0];
    }
    push(value){
        this.data.push(value);
        this.bubbleUp(this.data.length - 1);
    }
    // pop the highest priority item
    // use array shift will be O(n)
    // swap the first and last is O(1)
    pop(){
        if(this.size() > 0){
            const ans = this.data[0];
            const last = this.data.pop();
            if(this.size() > 0){
                this.data[0] = last;
                this.bubbleDown(0);
            }
            
            return ans;
        }
        return null;
    }
    bubbleUp(index){
        while(index > 0){
            let parentIndex = Math.floor((index-1)/2);
            if(parentIndex >= 0 && this.compare(this.data[index], this.data[parentIndex]) < 0){
                this.swap(index, parentIndex);
                index = parentIndex;
            }else{
                break;
            }
        }
    }
    bubbleDown(index){
        while(index < this.size()){
            const leftChildIndex = index*2 + 1;
            const rightChildIndex = index*2 + 2;
            let smallestIndex = index;
            if(leftChildIndex < this.size() && this.compare(this.data[leftChildIndex], this.data[smallestIndex]) < 0){
                smallestIndex = leftChildIndex;
            }
            if(rightChildIndex < this.size() && this.compare(this.data[rightChildIndex], this.data[smallestIndex]) < 0){
                smallestIndex = rightChildIndex;
            }
            if(smallestIndex !== index){
                this.swap(smallestIndex, index);
                index = smallestIndex;
            }else{
                break;
            }
        }
    }
}
```

## Space Complexity
- A string variable, like `const a = "sdfwefewfewfwefew"`, the space complexity depends on the size of the string stored in memory.
- arr in a for loop
    - Space Complexity should be the O(arr.length): JavaScript's garbage collector automatically frees memory for any object (or string) that is no longer referenced
- variable in the recusive
    - Space Complexity should be the O(recusive.depth*variable.length): JavaScript's garbage collector automatically frees memory for any object (or string) that is no longer referenced, but the variable is still be referenced in the recusive