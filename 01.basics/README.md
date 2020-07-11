# Basics

## Types
``` javascript
// 8 types
const string = 'Hello World';      // String
const num = 123.45;                // Number (floating-point double-precision 64-bit)
const bigInt = 10000000000000000n; // BigInt
const bool = true;                 // Boolean
const nullVal = null;              // null
const undefinedVal = undefined;    // undefined
const symbol = new Symbol();       // Symbol
const obj = { lang: 'JS' };        // Object

// arrays are also objects
const arr = [1, 2, 3];

// functions are callable object
const func = function(a, b) {
    return a + b;
};
const res = func(1, 2);
```

## Variables
``` javascript
// const - a block-scoped variable that cannot be re-assigned
// preferred by default
const a = 1;
a = 2; // TypeError: Assignment to constant variable.

// let - a block-scoped variable
// used when a variable needs to be re-assigned
let b = 2;
b = 3;
console.log(b); // 3

// var - a function-scoped or global-scoped variable
// used if the environment doesn't support 'const' and 'let' e.g. old browsers
var c = 3;
```

## Functions
``` javascript
// There are multiple ways to define a function in JS:

// 1. function declaration
function add(param1, param2) {
    return param1 + param2;
}

// 2. function expression
const add = function(param1, param2) {
    return param1 + param2;
    return val;
}

// 3. arrow function
const add = (param1, param2) => {
    return param1 + param2;
}

// 4. arrow function expression
const add = (param1, param2) => param1 + param2;

console.log(add(2, 3)); // 5
```

``` javascript
// when using arrow functions
// parenthesis for a single parameter can be omitted
const times2 = val => val * 2;
console.log(times2(5));  // 10
```

``` javascript
// using default parameters
function multiply(x, y = 2) {
    return x * y;
}

multiply(5);    // 10
multiply(5, 4); // 20
```

``` javascript
// using rest parameters
function sum(initial, ...args) {
    let s = initial;
    for (let x of args) {
        s += x;
    }
    return s;
}

sum(1, 2);       // 3
sum(1, 2, 3, 4); // 10
sum(1);          // 1
```

``` javascript
// using generator functions
// it's is a special function that can be exited and re-entered saving the context across re-entrances
function* idGenerator() {
    let index = 1;
    while(true) {
        yield index++;
    }
}
const getId = idGenerator(); // 'getId' is a generator object
getId.next().value; // 1
getId.next().value; // 2
```

## Assignment
``` javascript
// compound assignment
let num = 2;
num += 3; // num = num + 3;
```

``` javascript
// increment / decrement
num++;
num--;
++num;
--num;
```

``` javascript
// destructuring assignment
// from an array
let [a, b] = [2, 3];
console.log(a); // 2;
console.log(b); // 3;
```

``` javascript
// from an object
let { a, b } = { a: 2, b: 3 };
console.log(a); // 2;
console.log(b); // 3;
```

``` javascript
// with rest parameters
let [a, b, ...rest] = [2, 3, 4, 5];
console.log(a); // 2;
console.log(b); // 3;
console.log(rest); // [4, 5];

let { a, b, ...rest } = { a: 2, b: 3, c: 4, d: 5 };
console.log(a); // 2;
console.log(b); // 3;
console.log(rest); // { c: 4, d: 5 }
```

``` javascript
// assignment separate from declaration
let a, b;
[a, b] = [2, 3];
```

``` javascript
// default values
let [a=1, b=2] = [3];
console.log(a); // 3;
console.log(b); // 2;
```

``` javascript
// a shortcut for swapping 2 variables
let x = 2, y = 3;
[x, y] = [y, x];
console.log(x); // 3
console.log(y); // 2
```

## Comparison
``` javascript
// === is more strict comparison than ==
// it's usually preferred
2 === 2;     // true
2 !== 2;     // false
2 === '2';   // false
0 === false; // false
0 === '';    // false
null === undefined; // false
```

``` javascript
2 == 2;     // true
2 != 2;     // false
2 == '2';   // true
0 == false; // true
0 == '';    // true
null == undefined; // true
```

## Type coercion
``` javascript
// when using a '+' to concatenate a string with a number or boolean
// operands are converted to a string
1 + '2';    // 12
'1' + true; // 1true
```

``` javascript
// boolean conversion
// when using '!' operands are converted to a boolean
!1;            // false
!'non-empty';  // false

// falsy values (values that are converted to false)
!0;          // true
!'';         // true
!NaN;        // true
!null;       // true
!undefined;  // true
```

``` javascript
// !! could be useful to convert any truthy value to true
const user = getUser();
const userExists = !!user;
console.log(userExists); // true
```

``` javascript
// some operators convert operands to a number
'3' - '2';   // 1
'3' - '2';   // 1
+'2';        // 2
4 > '5';     // false
```

## Conditions
``` javascript
// if else
const num = Math.floor(Math.random() * 100); // [0, 99]
if (num % 3 === 0 && num % 5 === 0) {
    console.log('FizzBuzz');
} else if (num % 3 === 0) {
    console.log('Fizz');
} else if (num % 5 === 0) {
    console.log('Buzz');
} else {
    console.log(num);
}
```

``` javascript
// conditional ternary operator (?:)
console.log(num % 2 === 0 ? 'even' : 'odd');
```

``` javascript
// nullish coalescing operator (??)
function printName(name) {
    const nameToPrint = name ?? 'Anonymous';
    console.log(nameToPrint);
}
printName('John Doe'); // John Doe
printName();           // Anonymous

// longer version
function printName_long(name) {
    const nameToPrint = name == undefined ? 'Anonymous' : name;
    console.log(nameToPrint);
}
```

``` javascript
// optional chaining (?.)
function getName(obj) {
    return obj?.name;
}
console.log(getName({ name: 'John Doe' })); // John Doe
console.log(getName({ key: 'value' }));     // undefined
console.log(getName());                     // undefined

// longer version
function getName_long(obj) {
    return obj == undefined ? undefined : obj.name; 
}

// optional chaining with arrays
function getFirst(arr) {
    return arr?.[0];
}
```

``` javascript
// combining optional chaining with nullish coalescing
// ?. + ?? = ♥
function getNameLength(obj) {
    return obj?.name?.length ?? -1;
}
console.log(getNameLength({ name: 'John Doe' })); // 8
console.log(getNameLength({ key: 'value' }));     // -1
console.log(getNameLength());                     // -1

// longer version
function getNameLength_long(obj) {
    if (obj == null || obj.name == null)
        return -1;

    return obj.name.length;
}
```

``` javascript
// switch
const animal = 'fox';
switch (animal) {
    case 'cat':
        console.log('meow');
        break;
    case 'dog':
        console.log('woof');
        break;
    default:
        console.log('...');
}
```

## Loops
``` javascript
// for loop
for (let num = 1; num < 10; ++num) {
    console.log(num);
}
```

``` javascript
// for...of loop
for (let num of [1, 2, 3, 4]) {
    console.log(num);
}
```

``` javascript
// while loop
let num = 1;
while (num < 10) {
    console.log(num);
    num++;
}
```

``` javascript
// do...while loop
let num = 1;
do {
    console.log(num);
    num++;
} while (num < 10)
```

``` javascript
// using 'break' to terminate a loop
for (let num of [1, 2, 2, 3, 4]) {
    if (num == 2) {
        console.log('+');
        break;
    }
    console.log('-');
}
// -
// +
```

``` javascript
// using 'continue' to terminate the current iteration
for (let num of [1, 2, 2, 3, 4]) {
    if (num == 2) {
        console.log('+');
        continue;
    }
    console.log('-');
}
// -
// +
// +
// -
// -
```

### Type checking / validation
``` javascript
// is string
typeof 'Hello World' === 'string'; // OK, but doesn't work for "new String('Hello World')"
toString.call('Hello World') === '[object String]'; // handles corner cases
```

``` javascript
// is number
typeof 3.14 === 'number'; // OK, but doesn't work for "new Number(3.14)"
Number.isFinite(3.14); // handles corner cases
```

``` javascript
// is integer
Number.isInteger(3);
```

``` javascript
// is boolean
typeof true === 'boolean'; // OK, but doesn't work for "new Boolean(true)"
toString.call(true) === '[object Boolean]'; // handles corner cases
```

``` javascript
// is not undefined (strict)
if (value !== undefined) { /* ... */ }
```

``` javascript
// is not null (strict)
if (value !== null) { /* ... */ }
```

``` javascript
// is not null or undefined
if (value != null) { /* ... */ }
```

``` javascript
// is array
Array.isArray([1, 2, 3]);
```

``` javascript
// is function
typeof Math.floor === 'function';
toString.call(Math.floor) === '[object Function]';
```

``` javascript
// is instance of class
class Animal { }
class Dog extends Animal { }
const dog = new Dog();
dog instanceof Dog;    // true
dog instanceof Animal; // true, because Animal is a super class
```

### Exceptions
``` javascript
// a method that throws an exception
function getDayOfWeek(dayNo) {
    const days = [ 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];
    if (!days[dayNo])
        throw new Error('Invalid day number.');

    return days[dayNo];
}
```

``` javascript
// catching an exception
try {
    const dayNo =  Math.floor(Math.random() * 10); // [0, 9]
    const name = getDayOfWeek(dayNo);
    console.log(name);
} catch (e) {
    console.log(e.message);
} finally {
    console.log('always prints');
}
```
