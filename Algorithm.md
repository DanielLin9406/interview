# Algorithm

## Index of Contents

- Sort
  - [Bubble](#bubble)
  - [Selection](#selection)
  - Insertion
  - Merge
  - Quick
  - Radix
- Array
  - Merge
  - Implement flatten using iterator
- Sleep Function

## Sort

### Bubble

#### Pseudocode

> 1. Start looping from with a variable called i the end of the array toward the beginning
> 2. Start an inner loop with a variable called j from the beginning until i-1
> 3. If arr[j] is greater that arr[j+1], swap those two values
> 4. Return the sorted array

```js
function bubbleSort(array = []) {
  let swaps;
  do {
    swaps = false;
    for (let i = 0; i < array.length - 1; i++) {
      if (array[i] > array[i + 1]) {
        let smallOne = array[i + 1];
        // Bubble up
        array[i + 1] = array[i];
        // Restore small one
        array[i] = smallOne;
        swaps = true;
      }
    }
  } while (swaps);

  return array;
}
```

Ref.[js-algorithms-and-data-structures-masterclass](https://www.udemy.com/course/js-algorithms-and-data-structures-masterclass)

### Selection

### Insertion

### Merge

```js

```

### Quick

### Radix
