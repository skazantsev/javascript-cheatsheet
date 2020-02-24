# Arrays

## Construction
``` javascript
// new array
const nums = [1, 2, 3];

// empty array
[];

// 2D array
[
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
];

// array of length N
[...Array(3)];             // [undefined, undefined, undefined]
[...new Array(3)];         // [undefined, undefined, undefined]
Array(3).fill();           // [undefined, undefined, undefined]
Array.from({ length: 3 }); // [undefined, undefined, undefined]

// filling an array
// syntax: fill(value, start?, end?): end is exclusive
Array(4).fill(0);           // [0, 0, 0, 0]
Array(4).fill(0, 1);        // [undefined, 0, 0, 0]
Array(4).fill(0, 1, 3);     // [undefined, 0, 0, undefined]

// array from string using a spread operator
[...'abc'];                 // ['a', 'b', 'c']

// array from string using Array.from
Array.from('abc');          // ['a', 'b', 'c']

// array from string using split('')
'abc'.split('');            // ['a', 'b', 'c']

// range from 0 using a spread operator
[...Array(4).keys()];       // [0, 1, 2, 3]


// for more complex scenarios a map function can be used
// syntax: mapFn(value, index?, array?)
// Array.from also accepts mapFn as a 2nd parameter.

[1, 2, 3].map(val => val * val);
Array.from([1, 2, 3], val => val * val);
// [1, 4, 9]

// range from 0 using map
[...Array(4)].map((_, i) => i);
Array.from({ length: 4 }, (_, i) => i);
// [0, 1, 2, 3]

// range from 5
[...Array(4)].map((_, i) => i + 5);
Array.from({ length: 4 }, (_, i) => i + 5);
// [5, 6, 7, 8]

// range from 5 with step 2
[...Array(4)].map((_, i) => i * 2 + 5);
Array.from({ length: 4 }, (_, i) => i * 2 + 5);
// [5, 7, 9, 11]

// a 2D array of zeros
[...Array(2)].map(_ => Array(3).fill(0));
Array.from({ length: 2 }, _ => Array(3).fill(0));
// [
//   [0, 0, 0],
//   [0, 0, 0]
// ]
```

## Access
``` javascript
const nums = [1, 2, 3];

// array length
console.log(nums.length); // 3

// first element
console.log(nums[0]); // 1

// last element
console.log(nums[nums.length - 1]); // 3

// accessing a non-existing index
console.log(nums[3]); // undefined
```

## Iterating
``` javascript
const nums = [1, 2, 3];

// naive for loop
for (let i = 0; i < nums.length; ++i) {
    console.log(nums[i]);
}

// for...of loop
for (const x of nums) {
    console.log(x);
}

// forEach
nums.forEach(x => console.log(x));
// or
nums.forEach(x => {
    console.log(x);
});

// iterating with index
for (const [index, value] of nums.entries()) {
    console.log(index, value);
}
```

## Add / remove elements: pop, push, shift, unshift, splice
``` javascript
// push(<elements>) - adds element(s) to the end; returns the array length
const arr1 = [1, 2, 3];
arr1.push(7);               // 4
console.log(arr1);          // [1, 2, 3, 7]

// it's possible to push multiple elements
arr1.push(8, 9);            // 6
console.log(arr1);          // [1, 2, 3, 7, 8, 9]


// pop() - removes an element from the end; returns the removed element
const arr2 = [1, 2, 3, 4];
arr2.pop();                 // 4
console.log(arr2);          // [1, 2, 3]

// pop() on an empty array returns undefined
[].pop(); // undefined


// unshift(<elements>) - adds element(s) to the beginning; returns the array length
const arr3 = [1, 2, 3];
arr3.unshift(4);            // 4
console.log(arr3);          // [4, 1, 2, 3]

// it's possible to add multiple elements
arr3.unshift(5, 6);         // 6
console.log(arr3);          // [5, 6, 4, 1, 2, 3]


// shift() - removes an element from the beginning; returns the removed element
const arr4 = [1, 2, 3, 4];
arr4.shift();               // 1
console.log(arr4);          // [2, 3, 4]

// shift() on an empty array returns undefined
[].shift(); // undefined


// splice(start, deleteCount?, <elements>?)
// - modifies an array in-place
// - can be used to remove and/or insert elements at any index
// - returns an array of removed elements

// remove an element at index 2
const arr5 = [1, 2, 3, 4];
arr5.splice(2, 1);          // [3] - removed
console.log(arr5);          // [1, 2, 4]

// clear the array
const arr6 = [1, 2, 3, 4];
const len = arr6.length;
arr6.splice(0, len);        // [1, 2, 3, 4] - removed
console.log(arr6);          // []

// insert elements 5, 6 starting at index 1
const arr7 = [1, 2, 3, 4];
arr7.splice(1, 0, 5, 6);    // [] - removed
console.log(arr7);          // [1, 5, 6, 2, 3, 4]

// remove 2 elements starting from index 1 and insert elements 5, 6
const arr8 = [1, 2, 3, 4];
arr8.splice(1, 2, 5, 6);    // [2, 3] - removed
console.log(arr8);          // [1, 5, 6, 4]
```

## Copy, slicing, concat: spread operator, slice, concat
``` javascript
const nums = [1, 2, 3, 4];

// copy using a spread operator
const copy = [...nums];

// copy using slice from index 0
const anotherCopy = nums.slice(0);

// slice(start, end?)
// - creates an array slice
// - 'start' is inclusive, 'end' is exclusive
nums.slice(2);              // [3, 4] - slice from index 2 until the end
nums.slice(0, 2);           // [1, 2]
nums.slice(1, 2);           // [2]


// concat using a spread operator
[...nums, ...[5, 6]];     // [1, 2, 3, 4, 5, 6]

// concat(<arrays or elements>)
nums.concat([5, 6]);      // [1, 2, 3, 4, 5, 6]
nums.concat(5, 6);        // [1, 2, 3, 4, 5, 6]
nums.concat([5, 6], [7]); // [1, 2, 3, 4, 5, 6, 7]
```

## Search: find, findIndex, indexOf, lastIndexOf
``` javascript
const people = [
    { id: 1, age: 35 },
    { id: 2, age: 26 },
    { id: 3, age: 19 },
    { id: 4, age: 42 },
];

// find((element, index?, array?) => condition)
// - finds a first element satisfying a condition
people.find(x => x.age < 20);           // { id: 3, age: 19 }

// if an element is not found 'undefined' is returned
people.find(x => x.id === 5);           // undefined

// find a person with age greater than 20 and index greater than 2
const person = people.find((person, index) => {
    return index > 2 && person.age > 20;
});
console.log(person);                   // { id: 4, age: 42 }


// find an index of a first element satisfying a condition
people.findIndex(x => x.age === 26);   // 1


// indexOf(element, fromIndex?)
// - get a first index of an element
[1, 2, 2, 3].indexOf(2);                // 1
[1, 2, 2, 3].indexOf(2, 2);             // 2

// returns -1 if the element is not found
[1, 2, 2, 3].indexOf(2, 3);             // -1

// find a last index of an element
[1, 2, 2, 3].lastIndexOf(2);            // 2
```

## Functional: map, filter, reduce, some, every
``` javascript
// map((element, index?, array?) => new_element)
// filter((element, index?, array?) => condition) 
// reduce((accumulator, value, index?, array?) => new_value, initialValue)
const sumOfEvenSquares = [1, 2, 3, 4]
    .map(val => val * val)
    .filter(val => val % 2 === 0)
    .reduce((total, val) => total + val, 0);
console.log(sumOfEvenSquares);          // 20

// every((element, index?, array?) => condition)
[3, 9, 21].every(x => x % 3 === 0);     // true

// some((element, index?, array?) => condition)
[3, 9, 21].some(x => x === 9);          // true


// More examples:

// N first fibonacci numbers
const sequence = [...Array(10)].reduce((ans, val, i) => {
    const nextValue = i <= 1 ? 1 : ans[i - 1] + ans[i - 2];
    ans.push(nextValue);
    return ans;
}, []);
console.log(sequence); // [ 1,  1,  2,  3,  5, 8, 13, 21, 34, 55 ]

// sum of differences between adjacent elements
const sumOfDiffs = [1, 2, 5, 1].reduce((ans, val, i, arr) =>
    i === 0 ? ans : ans + Math.abs(val - arr[i - 1])
, 0);
console.log(sumOfDiffs); // 8

// compound interest
const amount = 100;
const years = 35;
const interest = 0.1; // 10%
const total = [...Array(years)].reduce((total, val) => total + total * interest, amount);
console.log(total);   // 2810.243684806425
```


## Sorting
``` javascript
// the default sorting compares elements as strings
[2, 10, 1, 3].sort();                // [1, 10, 2, 3]

// sort numbers (ascending)
[2, 10, 1, 3].sort((x, y) => x - y); // [1, 2, 3, 10]

// sort numbers (descending)
[2, 10, 1, 3].sort((x, y) => y - x); // [10, 3, 2, 1]

// sort ASCII strings (ascending)
['b', 'a', 'c'].sort();                             // [ 'a', 'b', 'c' ]

// sort ASCII strings (descending)
['b', 'a', 'c'].sort((x, y) => x > y ? -1 : 1);     // [ 'c', 'b', 'a' ]

// sort strings with non-ASCII characters (ascending)
['b', 'a', 'ä'].sort((x, y) => x.localeCompare(y)); // [ 'a', 'ä', 'b' ]

// sort strings with non-ASCII characters (descending)
['b', 'a', 'ä'].sort((x, y) => y.localeCompare(x)); // [ 'b', 'ä', 'a' ]

// the method sorts elements in-place and returns a reference to a sorted array
const arr = ['green', 'red', 'blue'];
const sorted = arr.sort();
console.log(arr);               // ['blue', 'green', 'red']
console.log(sorted);            // ['blue', 'green', 'red']
console.log(arr === sorted);    // true

// make a sorted array copy using a spread operator
const arr2 = ['green', 'red', 'blue'];
const sorted2 = [...arr2].sort();
console.log(arr2);               // ['green', 'red', 'blue']
console.log(sorted2);            // ['blue', 'green', 'red']
console.log(arr2 === sorted2);   // false
```

## Other methods
``` javascript
// join(separator?) - concatenates elements into a string
[1, 2, 3, 4].join(' ');         // '1  2  3  4'
[1, 2, 3, 4].join('-->');       // '1-->2-->3-->4'

// if a separator is not specified, ',' is used
[1, 2, 3, 4].join();            // '1, 2, 3, 4'


// reverse()
[1, 2, 3, 4].reverse();          // [4, 3, 2, 1]
[...'abcd'].reverse().join('');  // dcba

// includes(value, fromIndex?)
[1, 2, 3, 4].includes(2);        // true
[1, 2, 3, 4].includes(5);        // false
[1, 2, 3, 4].includes(2, 2);     // false

// Array.isArray
Array.isArray([1, 2, 3]);        // true

// toString()
[1, 2, 3].toString()            // 1,2,3

// Array destructuring
const [x, y, ...rest] = [1, 2, 3, 4];
console.log(x);     // 1
console.log(y);     // 2
console.log(rest);  // [3, 4]
```
