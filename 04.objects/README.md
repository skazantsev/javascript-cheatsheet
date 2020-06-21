# Objects

## Construction / access
``` javascript
// empty object
const empty = {};

// with properties
const person = {
    name: 'John Doe',
    age: 20,
    langs: [ 'JavaScript', 'Python' ]
};

// accessing a property
console.log(person.name);      // 'John Doe'

// accessing a property using a bracket notation
console.log(person['name']);   // 'John Doe'

// a bracket notation is useful when a property name is dynamic
const propName = Math.random() > 0.5 ? 'name' : 'age';
console.log(person[propName]); // 'John Doe' or 20

// accessing a non-existing property
console.log(person.test);      // undefined
console.log(person['test']);   // undefined

// setting a property
person.jobTitle = 'Software Engineer';
console.log(person.jobTitle);  // 'Software Engineer'
console.log(person);
// { name: 'John Doe', age: 20, langs: [ 'JavaScript', 'Python' ], jobTitle: 'Software Engineer' }

// deleting a property
delete person.jobTitle;        // true - deleted
console.log(person.jobTitle);  // undefined
console.log(person);
// { name: 'John Doe', age: 20, langs: [ 'JavaScript', 'Python' ] }


// nested object
const nested = { address: { country: 'Netherlands' } };
console.log(nested.address.country); // 'Netherlands'

// an object with a function
const obj = {
    x: 2,
    y: 3,
    add: function() {
        // using 'this' to access object properties
        return this.x + this.y;
    }
};
console.log(obj.add()); // 5
```

## Comparison, copy, merge
``` javascript
const obj = { langs: [ 'JavaScript', 'Python' ] };

const anotherRef = obj;
console.log(obj == anotherRef);    // true - variables point to the same object
console.log(obj === anotherRef);   // true

const anotherObj = { langs: [ 'JavaScript', 'Python' ] };
console.log(obj == anotherObj);    // false - variables point to different objects
console.log(obj === anotherObj);   // false

// shallow copy using spread
const obj2 = { ...obj };
console.log(obj === obj2);             // false - obj and obj2 are different objects
console.log(obj.langs === obj2.langs); // true - 'langs' points to the same array

// shallow copy using assign
const obj3 = Object.assign({}, obj);
console.log(obj === obj3);             // false
console.log(obj.langs === obj3.langs); // true

// deep copy using serialization
const obj4 = JSON.parse(JSON.stringify(obj));
console.log(obj === obj4);             // false
console.log(obj.langs === obj4.langs); // false - obj.langs and obj4.langs are different arrays

// merge objects
const obj_a = { a: '1' };
const obj_b = { b: '2' };
const obj_c = { c: '3' };
const merged = Object.assign({}, obj_a, obj_b, obj_c);
console.log(merged); // { a: '1', b: '2', c: '3' }

// merge by changing a target object
const target = { a: '1' };
const source = { b: '2' };
const merged2 = Object.assign(target, source);
console.log(target); // { a: '1', b: '2' }
console.log(target === merged2); // true - target and merged2 point to the same object
```

## Enumerating
``` javascript
const person = {
    name: 'John Doe',
    age: 20
};

// get an array of non-inherited property keys
console.log(Object.keys(person)); // ['name', 'age']

// iterate through non-inherited property keys
for (let key of Object.keys(person)) {
    console.log(key);
}


// get an array of non-inherited property values
console.log(Object.values(person)); // ['John Doe', 20]

// iterate through non-inherited property values
for (let value of Object.values(person)) {
    console.log(value);
}


// get an array of non-inherited property keys and values
console.log(Object.entries(person));
// [
//   ['name', 'John Doe'],
//   ['age', 20]
// ]

// iterate through non-inherited property keys and values
for (let [key, value] of Object.entries(person)) {
    console.log(key, value);
}


// using for...in to iterate through all properties (including inherited ones)
const developer = Object.create(person);
developer.lang = 'JavaScript';

for (let key in developer) {
    console.log(`${key}: ${developer[key]}`);
}
// > lang: JavaScript
// > name: John Doe
// > age: 20
//
// Object.keys() and Object.values() would output only 'lang'


// using objects as a hashtable
//
// example: finding even numbers that appear in the array more than 2 times.
const nums = [5, 6, 2, 1, 2, 3, 6, 5, 4, 5, 2, 6];
const freqMap = {};
for (let n of nums) {
    if (freqMap[n] == null) {
        freqMap[n] = 0;
    }
    freqMap[n]++;
}

const ans = Object.keys(freqMap)
    .filter(key => parseInt(key, 10) % 2 === 0 && freqMap[key] > 2)
    .map(key => parseInt(key))
    .sort((x, y) => x - y);

console.log(ans);
// > [2, 6]
```
