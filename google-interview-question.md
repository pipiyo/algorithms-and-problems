Notes from https://medium.com/@bretcameron/4-ways-to-solve-a-google-interview-question-in-javascript-12e6eec87576
==========================

The Problem
==========================

## Example A
If we were given the `array [1, 2, 4, 9]` and the value `8` , our function should return `false` , because no two values in the array may be added together to get `8`.

## Example B
But, if we were given the `array [1, 2, 4, 4]` and the value `8` , our function should return `true` , because `4 + 4 = 8`.



# Solution 1: Brute Force
* Time Complexity: O(N²)
* Space Complexity: O(1)

```js
const findSum = (arr, val) => {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length; j++) {
      if (i !== j && arr[i] + arr[j] === val) {
        return true;
      };
    };
  };
  return false;
};
```



# Solution 2: Binary Search
* Time Complexity: O(Nlog(N))
* Space Complexity: O(N)

```js
const findSum = (arr, val) => {
  for (let i = 0; i < arr.length; i++){
    if (binarySearch(removeIndex(arr, i), val - arr[i])) {
      return true;
    }
  };
  return false;
};
const removeIndex = (arr, i) => {
  return arr.slice(0, i).concat(arr.slice(i + 1, arr.length));
};
const binarySearch = (arr, val) => {
  let start = 0;
  let end = arr.length - 1;
  let pivot = Math.floor(arr.length / 2);  
  while (start < end) {
    if (val < arr[pivot]) {
      end = pivot - 1;
    } else if (val > arr[pivot]) {
      start = pivot + 1;
    };
    pivot = Math.floor((start + end) / 2);
    if (arr[pivot] === val) {
      return true;
    }
  };
  return false;
};
```





# Solution 3: Linear Time
* Time Complexity: O(N)
* Space Complexity: O(1)

```js
const findSum = (arr, val) => {
  let start = 0;
  let end = arr.length - 1;
  while (start < end) {
    let sum = arr[start] + arr[end];
    if (sum > val) {
      end -= 1;
    } else if (sum < val) {
      start += 1;
    } else {
      return true;
    };
  };
  return false;
};
```



# Solution 4: Linear Time and Space
* Time Complexity: O(N)
* Space Complexity: O(N)

```js
const findSum = (arr, val) => {
  let searchValues = new Set();
  searchValues.add(val - arr[0]);
  for (let i = 1, length = arr.length; i < length; i++) {
    let searchVal = val - arr[i];
    if (searchValues.has(arr[i])) {
      return true;
    } else {
      searchValues.add(searchVal);
    }
  };
  return false;
};
```

```js
//refactory solution
const findSum = (arr, sum) =>
  arr.some((set => n => set.has(n) || !set.add(sum - n))(new Set));
```