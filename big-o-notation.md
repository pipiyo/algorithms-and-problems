Notes from https://medium.com/@bretcameron/ace-your-coding-interview-by-understanding-big-o-notation-and-write-faster-code-6b60bd498040
==========================

What is Big O Notation?
==========================

* how quickly the run-time grows relative to the input, as the input increases.

# O(1)

No matter the amount of data you feed in, the algorithm will always take the same amount of time.
Any function that spits out one value — regardless of the input size.

```js
function(array) {
  return array[0];
}
```

# O(N) — Linear Time

As the length of the Data increases, the amount of processing required increases at the same rate.

```js
function logArray(array) {
  for (let i = 0; i < array.length; i++) {
    console.log(array[i]);
  }
}
```

```js
//worst case scenario
function findTheMeaningOfLife(array){
  for (let i = 0; i < array.length; i++) {
    if (array[i] === 42) {
      return i;
    }
  }
}
```

# O(N²) — Quadratic Time

An algorithm with an efficiency of `O(N²)` increases at twice the relative rate of `O(N)`. The maximum number of passes that might be needed

```js
let array = [1, 2, 3]
function(array){
  for (let i = 0; i < array.length; i++){
    for (let j = 0; j < array.length; j++){
      console.log(array[j]);
    }
  }
}
```

This will print `1 2 3 1 2 3 1 2 3` to the console.
That’s 9 numbers, compared to the 3 printed by logArray . And so it follows that `3² = 9`, and this function has a performance of `O(N²)`.

## Bubble Sort =  O(N²)
```js
function bubbleSort(array) {
  let length = array.length;
  // This loop handles the passes
  for (let i = 0; i < length; i++) {
  // This loop handles the swapping during a single pass
    for (let j = 0; j < (length - i - 1); j++) {
      if (array[j] > array[j + 1]) {
        let tmp = array[j];
        array[j] = array[j + 1];
        array[j + 1] = tmp;
      }
    }
  }
  return array;
}
```

## O(N³), O(N⁴) — Cubic Time, Quartic Time, and so on
```js
function(array){
  for (let i = 0; i < array.length; i++){
    for (let j = 0; j < array.length; j++){
      for (let k = 0; k < array.length; k++){
        for (let l = 0; l< array.length; l++){
          console.log(l);
        }
      }
    }
  }
}
```

# Logarithms
Take this statement: `2⁶ = 64`  
We can also express this as: `log₂(64) = 6`  
`“Log base 2 of 64 equals 6”`






# O(logN) — Binary Search
Every time you double the data-set, an algorithm with performance O(logN) only has to add in 1 more step.
```js
function binarySearch(array, searchValue) {
// Define start, end and pivot (middle)
  let start = 0;
  let end = array.length - 1;
  let pivot = Math.floor((start + end) / 2);
// As long as the pivot is not our searchValue and the array is greater than 1, define a new start or end
  while (array[pivot] !== searchValue && start < end) {
    if (searchValue < array[pivot]) {
      end = pivot - 1
    } else {
      start = pivot + 1
    }
// Every time, calculate a new pivot value
    pivot = Math.floor((start + end) / 2);
  };
// If the current pivot is out search value, return it's index. Otherwise, return false.
  return array[pivot] === searchValue ? pivot : false;
};
```

# O(NlogN) — Quicksort
```js
function quicksort(array) {
  // If a sub-array has only 1 value, the array is sorted and can be returned
  if (array.length <= 1) {
    return array;
  }
  // Define pivot, and create empty "left" and "right" sub-arrays
  let pivot = array[0];
  let left = [];
  let right = [];
  // Go through the array, comparing values to the pivot, and sorting them into the "left" and "right" sub-arrays
  for (let i = 1; i < array.length; i++) { 
    array[i] < pivot ? left.push(array[i]) : right.push(array[i]);
  }
  // Repeat using recursion
  return quicksort(left).concat(pivot, quicksort(right));
};
```

# Space Complexity in Bubble Sort, Binary Search and Quicksort

## Bubble Sort
We only had to define a single new variable, tmp. In fact, no matter the size of the input, we would still only need the one tmp variable. So that means the space complexity of the algorithm is just O(1).

## Binary Search
Binary Search also has a space complexity of O(1), because the number of new variables created does not change relative to the size of the input.

## Quicksort
The space complexity depends on the implementation, since new arrays are created in the process. In our implementation, space complexity is O(logN).
