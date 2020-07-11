# Basics

## Types

8 types in JavaScript:
``` javascript
const string = 'Hello World';      // String
const num = 123.45;                // Number (floating-point double-precision 64-bit)
const bigInt = 10000000000000000n; // BigInt
const bool = true;                 // Boolean
const nullVal = null;              // null
const undefinedVal = undefined;    // undefined
const symbol = new Symbol();       // Symbol
const obj = { lang: 'JS' };        // Object
```

Arrays are objects:
``` javascript
const arr = [1, 2, 3];
typeof arr; // object
```

Functions are callable object:
``` javascript
const func = function(a, b) {
    return a + b;
};
const res = func(1, 2);

typeof func; // function
```

## Variables

`const` - a block-scoped variable that cannot be re-assigned. Preferred by default.
``` javascript
const a = 1;
a = 2; // TypeError: Assignment to constant variable.
```

`let` - a block-scoped variable. Used when a variable needs to be re-assigned.
``` javascript
let b = 2;
b = 3;
console.log(b); // 3
```

`var` - a function-scoped or global-scoped variable. Used if the runtime doesn't support `const` and `let` e.g. old browsers.
``` javascript
var c = 3;
```

## Functions

There are multiple ways to define a function in JS.

I. function declaration
``` javascript
function add(param1, param2) {
    return param1 + param2;
}
```

II. function expression
``` javascript
const add = function(param1, param2) {
    return param1 + param2;
    return val;
}
```

III. arrow function
``` javascript
const add = (param1, param2) => {
    return param1 + param2;
}
```

IV. arrow function expression
``` javascript
const add = (param1, param2) => param1 + param2;
```

When using arrow functions parenthesis for a single parameter can be omitted.
``` javascript
const times2 = val => val * 2;
console.log(times2(5));  // 10
```

Using default parameters:
``` javascript
function multiply(x, y = 2) {
    return x * y;
}

multiply(5);    // 10
multiply(5, 4); // 20
```

Using rest parameters:
``` javascript
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

Using generator functions.

It's is a special function that can be exited and re-entered saving the context across re-entrances.
``` javascript
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

Compound assignment:
``` javascript
let num = 2;
num += 3; // num = num + 3;
```

Increment / decrement:
``` javascript
num++;
num--;
++num;
--num;
```

Destructuring assignment from an array:
``` javascript
let [a, b] = [2, 3];
console.log(a); // 2;
console.log(b); // 3;
```

Destructuring assignment from an object:
``` javascript
let { a, b } = { a: 2, b: 3 };
console.log(a); // 2;
console.log(b); // 3;
```

Destructuring assignment with rest parameters:
``` javascript
let [a, b, ...rest] = [2, 3, 4, 5];
console.log(a); // 2;
console.log(b); // 3;
console.log(rest); // [4, 5];

let { a, b, ...rest } = { a: 2, b: 3, c: 4, d: 5 };
console.log(a); // 2;
console.log(b); // 3;
console.log(rest); // { c: 4, d: 5 }
```

Destructuring assignment with default values:
``` javascript
let [a=1, b=2] = [3];
console.log(a); // 3;
console.log(b); // 2;
```

Assignment separate from declaration:
``` javascript
let a, b;
[a, b] = [2, 3];
```

A shortcut for swapping 2 variables:
``` javascript
let x = 2, y = 3;
[x, y] = [y, x];
console.log(x); // 3
console.log(y); // 2
```

## Comparison

`===` is more strict comparison than `==` and it's usually preferred.
``` javascript
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

### Type coercion

When using a `+` to concatenate a string with a number or boolean operands are converted to a string.
``` javascript
1 + '2';    // 12
'1' + true; // 1true
```

boolean conversion - when using `!` operands are converted to a boolean.
``` javascript
!1;            // false
!'non-empty';  // false
```

falsy values:
``` javascript
!0;          // true
!'';         // true
!NaN;        // true
!null;       // true
!undefined;  // true
```

`!!` could be useful to convert any truthy value to true.
``` javascript
const user = getUser();
const userExists = !!user;
console.log(userExists); // true
```

Some operators convert operands to a number.
``` javascript
'3' - '2';   // 1
'3' - '2';   // 1
+'2';        // 2
4 > '5';     // false
```

## Conditions

`if else`
``` javascript
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

Conditional ternary operator `?:`
``` javascript
console.log(num % 2 === 0 ? 'even' : 'odd');
```

Nullish coalescing operator `??`
``` javascript
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

Optional chaining `?.`
``` javascript
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
```

Optional chaining with arrays:
``` javascript
function getFirst(arr) {
    return arr?.[0];
}
```

Combining optional chaining with nullish coalescing:
``` javascript
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

`switch`
``` javascript
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

`for` loop:
``` javascript
for (let num = 1; num < 10; ++num) {
    console.log(num);
}
```

`for...of` loop:
``` javascript
for (let num of [1, 2, 3, 4]) {
    console.log(num);
}
```

`while` loop:
``` javascript
let num = 1;
while (num < 10) {
    console.log(num);
    num++;
}
```

`do...while` loop:
``` javascript
let num = 1;
do {
    console.log(num);
    num++;
} while (num < 10)
```

Using `break` to terminate a loop:
``` javascript
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

Using `continue` to terminate the current iteration:
``` javascript
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

is `string`:
``` javascript
typeof 'Hello World' === 'string'; // OK, but doesn't work for "new String('Hello World')"
toString.call('Hello World') === '[object String]'; // handles corner cases
```

is `number`:
``` javascript
typeof 3.14 === 'number'; // OK, but doesn't work for "new Number(3.14)"
Number.isFinite(3.14); // handles corner cases
```

is integer `number`:
``` javascript
Number.isInteger(3);
```

is `boolean`:
``` javascript
typeof true === 'boolean'; // OK, but doesn't work for "new Boolean(true)"
toString.call(true) === '[object Boolean]'; // handles corner cases
```

is not `undefined` (strict):
``` javascript
if (value !== undefined) { /* ... */ }
```

is not `null` (strict):
``` javascript
if (value !== null) { /* ... */ }
```

is not `null` or `undefined`:
``` javascript
if (value != null) { /* ... */ }
```

is `array`:
``` javascript
Array.isArray([1, 2, 3]);
```

is `function`:
``` javascript
typeof Math.floor === 'function';
toString.call(Math.floor) === '[object Function]';
```

is instance of `class`:
``` javascript
class Animal { }
class Dog extends Animal { }
const dog = new Dog();
dog instanceof Dog;    // true
dog instanceof Animal; // true, because Animal is a super class
```

### Exceptions

Throwing an exception:
``` javascript
function getDayOfWeek(dayNo) {
    const days = [ 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];
    if (!days[dayNo])
        throw new Error('Invalid day number.');

    return days[dayNo];
}
```

Catching an exception:
``` javascript
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
