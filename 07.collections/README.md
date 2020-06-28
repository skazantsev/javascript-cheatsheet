# Collections

## Map
``` javascript
const map = new Map();

// set items
map.set('red', 3);
map.set('green', 4);
map.set('blue', 2);
map.set('green', 5);
console.log(map); // Map { 'red' => 3, 'green' => 5, 'blue' => 2 }

// size
console.log(map.size); // 3

// check if an item is in the map
console.log(map.has('green')); // true
console.log(map.has('yellow')); // false

// to array of keys and values
const arr = [...map];
console.log(arr); // [ [ 'red', 3 ], [ 'green', 5 ], [ 'blue', 2 ] ]

// enumerate
// the order is not defined
for (let key of map.keys()) {
    console.log(key);
}

for (let val of map.values()) {
    console.log(val);
}

for (let [key, val] of map) {
    console.log(key, val);
}

// delete
map.delete('green');    // true
map.delete('yellow');   // false
console.log(map);       // Map { 'red' => 3, 'blue' => 2 }

// clear
map.clear();
console.log(map); // Map {}

// initialize Map from Array of keys and values
const map2 = new Map([ [ 'red', 3 ], [ 'green', 5 ], [ 'blue', 2 ] ]);

// example: given a bucket of marble balls find the most frequent marble color.
const marbles = ['red', 'green', 'yellow', 'blue', 'green', 'green', 'orange', 'red', 'blue', 'yellow', 'blue', 'red', 'green'];

const colorToCount = new Map();
for (let marble of marbles) {
    colorToCount.set(marble, (colorToCount.get(marble) || 0) + 1);
}
const max = Math.max(...colorToCount.values());
const winner = [...colorToCount].find(([key, value]) => value === max);
console.log(`The ${winner[0]} is the most frequent marble ball.`);
```

## Set
``` javascript
const set = new Set();

// add items
set.add(1);
set.add(2)
set.add(3);
set.add(1);
console.log(set); // Set { 1, 2, 3 }

// size
console.log(set.size);   // 3

// check if an item is in the set
console.log(set.has(1)); // true
console.log(set.has(4)); // false

// to array
const arr = [...set];
console.log(arr); // [1, 2, 3]

// enumerate
// the order is not defined
for (let val of set) {
    console.log(val);
}

// delete
set.delete(1); // true
set.delete(4); // false
console.log(set); // Set { 2, 3 }

// clear
set.clear();
console.log(set); // Set {}

// initialize Set from Array
const set2 = new Set([1, 2, 3, 2, 1, 3]);
console.log(set2); // Set { 1, 2, 3 }

// example: find a number of unique elements in an array
const items = [2, 3, 1, 2, 5, 3, 2, 1];
const ans = new Set(items).size;
console.log(ans); // 4
```

## Queue
JavaScript doesn't have a built-in queue.

Implementing the queue via Array's `push(x)` and `shift()` is not a good idea since the time complexity of `shift()` is `O(N)`.

``` javascript
// AVOID THIS
const queue = [];
queue.push(1);
queue.push(2);

queue.shift(); // 1
```

If removing of elements is not needed you can use an array with an index indicating the top of the queue.

``` javascript
const queue = [];
let topIndex = 0;
queue.push(1);
queue.push(2);

queue[topIndex++]; // 1

queue.push(3);

queue[topIndex++]; // 2
queue[topIndex++]; // 3
```

A simple queue can be implemented using a linked list.
``` javascript
class Queue {
    constructor() {
        this.head = null;
        this.tail = null
        this.size = 0;
    }

    enqueue(val) {
        const item = { val: val, next: null };
        this.size++;

        if (this.size === 1) {
            this.head = this.tail = item;
            return;
        }

        this.tail.next = item;
        this.tail = this.tail.next;
    }

    dequeue() {
        if (this.size === 0)
            throw new Error('The queue is empty');

        this.size--;

        const val = this.head.val;
        this.head = this.head.next;
        if (this.head == null) {
            this.tail = null;
        }

        return val;
    }
}

const queue = new Queue();
queue.enqueue(1);
queue.enqueue(2);
queue.dequeue();  // 1
queue.enqueue(3);
queue.dequeue();  // 2
queue.dequeue();  // 3
```

## Stack
A stack could implemented using Array's `push(x)` and `pop()`.

``` javascript
const stack = [];
stack.push(1);
stack.push(2);

stack.pop(); // 2
```

## Heap
JavaScript doesn't have a built-in heap.

A simple binary heap implementation can be found at https://github.com/skazantsev/heap-javascript/blob/master/src/heap.js
