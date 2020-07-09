# Modules

``` javascript
// individual named exports

// lib.js
export const VALUE = 42;

export function sum(a, b) {
    return a + b;
}

export const subtract = (a, b) => a - b;

export class Calculator { }

// client.js
import { VALUE, sum, subtract, Calculator } from './lib';

console.log(VALUE);
console.log(sum(2, 3));
```

``` javascript
// list of named exports

// lib.js
const VALUE = 42;

function sum(a, b) {
    return a + b;
}

const subtract = (a, b) => a - b;

class Calculator { }

export { VALUE, sum, subtract, Calculator };
```

``` javascript
// wildcard import of named exports

// lib.js
export let value = 42;

export const increment = () => value++;

export const decrement = () => value--;

// client.js
import * as counter from './lib';

console.log(counter.value);
counter.increment();
console.log(counter.value);
```

``` javascript
// renaming exports during export

// lib.js
const VALUE = 42;

function sum(a, b) {
    return a + b;
}

export { VALUE as val, sum as add };

// client.js
import { val, add } from './lib';

console.log(val);
console.log(add(2, 3));
```

``` javascript
// renaming exports during import

// lib.js
export const VALUE = 42;

export function sum(a, b) {
    return a + b;
}

// client.js
import { VALUE as val, sum as add } from './lib';

console.log(val);
console.log(add(2, 3));
```

``` javascript
// default exports

// lib.js
// only one default export per file
export default {
    value: 42,
    increment() {
        this.value++;
    },
    decrement() {
        this.value--;
    }
};

// client.js
// a default export can be imported with any name
import counter from './lib';

console.log(counter.value);
counter.increment()
console.log(counter.value);
```

``` javascript
// re-exporting to simplify export on the client-side

// component1.js
export const a = 2;

// component2.js
export const b = 3;

// lib.js
export * from './component1';
export * from './component2';

// client.js
import { a, b } './lib';

console.log(a, b);
```

``` javascript
// combining default and named exports

// lib.js
export let value = 42;

const increment = () => value++;

const decrement = () => value--;

export default { increment, decrement };

// client.js
import counter, { value } from './lib';

console.log(value);
counter.increment();
console.log(value);
```
