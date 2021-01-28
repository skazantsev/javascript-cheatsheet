# Math

## Operations
``` javascript
// basic operators: + - * / ++ --
2 + 3;  // 5
2++;    // 3
10 / 3; // 3.3333333333333335
```

``` javascript
// remainder
10 % 3; // 1
```

``` javascript
// exponent
2 ** 3;         // 8
// or
Math.pow(2, 3); // 8
```

``` javascript
// bitwise operations: & | ^  ~ << >>
3 & 5: // 1
```

## Getting max / min / abs
``` javascript
Math.max(2, 3);     // 3
Math.min(2, 3);     // 2
```

``` javascript
// can accept multiple params
Math.max(2, 3, 5);  // 5
```

``` javascript
// using with an array
const arr = [2, 3, 5];
Math.max(...arr);   // 5
```

``` javascript
Math.abs(3);  // 3
Math.abs(-3); // 3
```

## Trunc, floor, ceil, round
``` javascript
// get the integer part of a number
Math.trunc(3.33);   // 3
Math.trunc(-3.33);  // -3
```

``` javascript
// get the greatest integer less than or equal to the input number
Math.floor(3.33);   // 3
Math.floor(-3.33);  // -4
```

``` javascript
// get the least integer greater than or equal to the number
Math.ceil(3.33);    // 4
Math.ceil(-3.33);   // -3
```

``` javascript
// rounding to the nearest integer
Math.round(3.33);   // 3
Math.round(3.66);   // 4
Math.round(3.50);   // 4
Math.round(-3.50);  // -3
```

## Generating random numbers
``` javascript
// get a floating-point number in the range of [0, 1)
Math.random();
```

``` javascript
// get a floating-point number in the range of [min, max)
const getRandomFloat = (min, max) => min + Math.random() * (max - min);
console.log(getRandomFloat(4, 8));
```

``` javascript
// get an integer number in the range [min, max);
const getRandomInt = (min, max) => Math.trunc(min + Math.random() * (max - min));
console.log(getRandomInt(4, 8)); // one of 4, 5, 6, 7
```

``` javascript
// get an integer number in the range [min, max];
const getRandomIntInclusive = (min, max) => Math.trunc(min + Math.random() * (max - min + 1));
console.log(getRandomIntInclusive(4, 8)); // one of 4, 5, 6, 7, 8
```

## Constants
``` javascript
// Math.PI
// calculating a circle area
const circleRadius = 10;
const circleArea = Math.PI * (circleRadius ** 2)
console.log(circleArea); // 314.1592653589793
```

``` javascript
// Math.E
// calculating continuous compound interest
const amount = 100;
const years = 35;
const interestRate = 0.1; // 10%
const compoundInterest = amount * Math.E ** (interestRate * years);
console.log(compoundInterest);
// 3311.5451958692306
```

## Other functions
``` javascript
// Square root
Math.sqrt(9);   // 3
Math.sqrt(12);  // 3.4641016151377544
```

``` javascript
// natural logarithm - ln(x)
Math.log(1000); // 6.907755278982137
```

``` javascript
// logarithm of x to base b
const baseLog = (b, x) => Math.log(b) / Math.log(x);
baseLog(2, 1024);   // 10
baseLog(10, 10000); // 4
```
