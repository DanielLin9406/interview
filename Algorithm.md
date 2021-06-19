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
- BloomFilter
- LRU Cache

## Sort

### Bubble

- Very interesting to understand

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

> - Find the minmum swap at the end and put it at the beginning.

#### Pseudocode

> 1. Store the first element as the smallest value you've seen so far.
> 2. Compare this item to the next item in the array until you find a smaller number.
> 3. If a smaller number is found, designate that smaller number to be the new "minimum" is not the value(index) you initially began with, swap the two values.
> 4. Repeat this with the next element until the array is sorted.

```js
function selectionSort(arr) {
  const swap = (arr, idx1, idx2) =>
    ([arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]]);

  for (let i = 0; i < arr.length; i++) {
    let lowest = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[lowest]) {
        lowest = j;
      }
    }
    if (i !== lowest) swap(arr, i, lowest);
  }

  return arr;
}
selectionSort([34, 22, 10, 19, 17]);
```

### Insertion

> 1. Start by picking the second element in the array
> 2. Now compare the second element with the one before it and swap if necessary
> 3. COntinue to the next element and if it is in the incorrect order, iterate through the sorted portion(i.e. the left side) to place the element in the correct place.
> 4. Repeat until the array is sorted.

```js
function insertionSort(arr) {
  for (let i = 1; i < arr.length; i++) {
    let current = arr[i];
    // Find the correct sopt to insert
    for (let j = i - 1; j >= 0 && arr[j] > current; j--) {
      // search from the last to first
      // moving a[j] forward one by one
      arr[j + 1] = arr[j];
    }
    // [1,2,9,20 want to be here,76,76] 20
    arr[j + 1] = current;
  }
  return arr;
}

insertionSort([2, 1, 9, 76, 4]);
```

Ref.[js-algorithms-and-data-structures-masterclass](https://www.udemy.com/course/js-algorithms-and-data-structures-masterclass)

### Merge

> This problem can be breaked down into two sub questions. Merging and MergeSort
> Exploits the fact that arrays of 0 or 1 element are always sorted.
> Works by decomposing an array into smaller arrays of 0 or 1 elements, then building up a newly sorted array.

#### Merging Arrays Pseudocode

> 1. Create an empty array, take a look at the smallest values in each input array
> 2. While there are still values we haven't looked at
>    2.1. If the value in the first array is smller than the value in the second array, push the value in the first array into our results and move on to the next value in the first array.
>    2.2. If the value in the first array is larger than the value in the second array, push the value in the second array into our results and move on to the next value in the second array
>    2.3. Once we exhaust one array, push in all remaining values from the other array.

```js
function merge(left, right) {
  const result = [];
  let il,
    rl = 0;
  while (il < left.length && rl < right.length) {
    if (left[il] < right[rl]) {
      result.push(left[il++]);
    } else {
      result.push(right[rl++]);
    }
  }
  return result.concat(left.slice(il)).concat(right.slice(rl));
}
```

#### MergeSort Pseudocode

> - Break up the array into halves until you have arrays that are empty or have one element
> - Once you have smaller sorted arrays, merge those arrays length of the array
> - Once the array has been merged back together, return the merged (and sorted!) array

```js
function mergeSort(arr) {
  if (arr.length <= 1) return arr;
  let mid = Math.floor(arr.length / 2);
  let left = mergeSort(arr.slice(0, mid));
  let right = mergeSort(arr.slice(mid));
  return merge(left, right);
}
```

Ref.[js-algorithms-and-data-structures-masterclass](https://www.udemy.com/course/js-algorithms-and-data-structures-masterclass)

### Quick

> - Like merge sort, exploits the fact that arrays of 0 or 1 element are always sorted
> - Works by selecting one element (call the "pivot") and finding the index where the pivot should end up in the sorted array
> - Once the pivot is positioned appropriately, quick sort can be applied on either side of the pivot

Ref.[js-algorithms-and-data-structures-masterclass](https://www.udemy.com/course/js-algorithms-and-data-structures-masterclass)

## BloomFilter

```js
const names = ['Abhin', 'Pai', ......]; // n names
const noOfHashFunction = 6; // number of hash functions
const storage = Array(Math.pow(2, 22) - 1).fill(0); // Bllom filter

const hash = (key) => {
  let hashNumbers = [];
  for (let i = 1; i <= noOfHashFunction; i++) {
    hashNumbers.push(
      Math.abs(
        key.split("").reduce((a, b) => ((a << i) - a + b.charCodeAt(0)) | 0, 0)
      )
    );
  }
  return hashNumbers;
};

// Initilizing bloom filter bit for a hash index
names.forEach((name) => {
  let indexes = hash(name);
  indexes.forEach((index) => (storage[index] = 1));
});
```

```js
// Traditional single name search
console.time("Single Traditional Search");
const isValueContain = (searchString) => {
  let result;
  names.forEach((name) => {
    if (name === searchString) {
      result = true;
      return;
    }
  });
  return result ? true : false;
};
console.log(isValueContain("Pai"));
console.timeEnd("Single Traditional Search");
// End of traditional Search

let result = [];
// Bloom filter single name search
console.time("Single Bloom Filter Search");
const isValueContainInBloom = (searchString) => {
  let hashes = hash(searchString);
  let result = hashes.filter((index) => !storage[index]);
  return result.length > 0 ? false : true;
};
console.log(isValueContainInBloom("Pai"));
console.timeEnd("Single Bloom Filter Search");
// End of Bloom Filter Search

// Tranditional Search for 1000 names
console.time("Traditional Search");
names.forEach((name) => {
  result.push(isValueContain(name));
});
console.log(result.filter((res) => !res));
console.timeEnd("Traditional Search");
// End of tranditional Search for 1000 names

// Boolm filter search for 1000 names
console.time("Bloom Filter");
names.forEach((name) => {
  result.push(isValueContainInBloom(name));
});
console.log(result.filter((res) => !res));
console.timeEnd("Bloom Filter");
// End of Boolm filter search for 1000 names
```

Ref.[Bloom Filter in Javascript](https://dev.to/abhinpai/bloom-filter-in-javascript-1efe)

## LRU Cache

> - To start with we can use a List. The ideal choice here would be a **Doubly Linked List**. Using a doubly linked list will allow us to remove an element from the cache in O(1) time complexity which is very important for us.
> - We also need a way to access the element in O(1) time complexity. To do so, we need a **Map data structure**. In Javascript, we can achieve this by using **Javascript Objects**.

```js
class LRUCache {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
    this.maxSize = 4;
    this.cache = {};
  }
  put(key, value) {
    let newNode;

    // if the key not present in cache
    if (this.cache[key] === undefined) newNode = new Node(key, value);

    //if we have an empty list
    if (this.size === 0) {
      this.head = newNode;
      this.tail = newNode;
      this.size++;
      this.cache[key] = newNode;
      return this;
    }

    if (this.size === this.maxSize) {
      //remove from cache
      delete this.cache[this.tail.key];

      //set new tail
      this.tail = this.tail.prev;
      this.tail.next = null;
      this.size--;
    }

    //add an item to the head
    this.head.prev = newNode;
    newNode.next = this.head;
    this.head = newNode;
    this.size++;

    //add to cache
    this.cache[key] = newNode;
    return this;
  }
  get(key) {
    if (!this.cache[key]) {
      return undefined;
    }

    let foundNode = this.cache[key];

    if (foundNode === this.head) return foundNode;

    let previous = foundNode.prev;
    let next = foundNode.next;

    if (foundNode === this.tail) {
      previous.next = null;
      this.tail = previous;
    } else {
      previous.next = next;
      next.prev = previous;
    }

    this.head.prev = foundNode;
    foundNode.next = this.head;
    foundNode.prev = null;
    this.head = foundNode;

    return foundNode;
  }
}
```

Ref.[LRU Cache Implementation using Javascript Linked List and Objects](http://progressivecoder.com/lru-cache-implementation-using-javascript-linked-list-and-objects/)
