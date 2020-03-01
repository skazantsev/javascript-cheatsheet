# Strings

## Construction
``` javascript
// new string
const singleQuotes = 'I contain \' and " characters';
const doubleQuotes = "I contain ' and \" characters";
const backticks = `I contain ' and " characters`;

// empty string
const empty = '';

// long string
const looong = 'This is a long string \
that is split across \
multiple lines!'
console.log(looong);
// This is a long string that is split across multiple lines!

// multi-line string
const multiline = `<body>
  <h1>Title</h1>
</body>`;
console.log(multiline);
//1 <body>
//2   <h1>Title</h1>
//3 </body>

// from array using join
['a', 'b', 'cd'].join(''); // 'abcd'

// from char codes
String.fromCharCode(72, 101, 108, 108, 111); // 'Hello'
String.fromCharCode(72); // 'H'

// string interpolation using template literals
const who = 'World';
console.log(`Hello ${who}`); // Hello World
console.log(`Hello ${who.toUpperCase()}`); // Hello WORLD

const a = 2, b = 3;
console.log(`a+b=${a+b}`); // a+b=5
```

## Access
``` javascript
const str = 'Hello';

// string length
console.log(str.length); // 5

// first character
console.log(str[0]); // 'H'

// last character
console.log(str[str.length - 1]); // 'o'

// accessing a non-existing index
console.log(str[10]); // undefined

// get a char code using charCodeAt(index)
'ABC'.charCodeAt(0); // 65
'ABC'.charCodeAt(1); // 66
[...'Hello'].map(x => x.charCodeAt(0)); // [72, 101, 108, 108, 111]
```

## Iterating
``` javascript
const str = 'Hello';

// naive for loop
for (let i = 0; i < str.length; ++i) {
    console.log(str[i]);
}

// for...of loop
for (const char of str) {
    console.log(char);
}

// convert to an array and use forEach
[...str].forEach(char => console.log(char));
```

## Parsing / conversion
``` javascript
// string -> array
[...'Hello'];       // ['H', 'e', 'l', 'l', 'o']
'Hello'.split('');  // ['H', 'e', 'l', 'l', 'o']

// array -> string
['H', 'e', 'l', 'l', 'o'].join(''); // Hello

// string -> number
// - parseInt(string, radix?) for integer numbers
// - parseFloat(string) for floating point numbers
parseInt('123', 10);        // 123
parseInt('-123', 10);       // -123
parseInt('123.456', 10);    // 123
parseFloat('123.456', 10);  // 123.456

// these are the same as parseInt and parseFloat
Number.parseInt(123, 10);         // 123
Number.parseFloat('123.456', 10); // 123.456

// number -> string
const num = 123.45;
num.toString(); // '123.45'
String(num);    // '123.45'
num + '';       // '123.45'
```

## Concatenation
``` javascript
// using a '+' operator
const str = 'Hello' + ' ' + 'World!'; // Hello World!

// using join
['red', 'green', 'refactor'].join(', '); // red, green, refactor
['H', 'e', 'l', 'l', 'o'].join(''); // Hello

// separator is ',' if not specified
['1', '2', '3'].join(); // 1,2,3

// using concat
'red'.concat(' ', 'green', ' ', 'refactor'); // red green refactor
''.concat(...['This', ' is', ' array']); // This is array
```

## Replace
``` javascript
// replace(str|regex, newStr|function(char, offset?, <matches?>, str))

// by default replace a first occurrence 
'is is is'.replace('is', 'was') // 'was is is'
'is is is'.replace(/is/, 'was') // 'was is is'

// use a regex with the 'global' flag to replace all occurrences
'is is is'.replace(/is/g, 'was') // 'was was was'

// it's also possible to pass a callback
// example: duplicate each character in a string
'abc'.replace(/./g, match => match + match); // aabbcc

// advanced example using the offset and str params
// reverse a string
'abcde'.replace(/./g, (match, offset, str) => str[str.length - 1 - offset]);
// edcba
```

## Simple search
``` javascript
// startsWith(str, fromIndex?)
'abcd'.startsWith('ab');    // true
'abcd'.startsWith('ab', 1); // false
'abcd'.startsWith('bc', 1); // true

// endsWith(str, length?)
'abcd'.endsWith('cd');      // true
'abcd'.endsWith('cd', 3);   // false
'abcd'.endsWith('bc', 3);   // true

// includes(str, fromIndex?)
'abcd'.includes('bc');      // true
'abcd'.includes('bc', 2);   // false

// indexOf(str, fromIndex?)
'abbbc'.indexOf('b');       // 1
'abbbc'.indexOf('bc');      // 3
'abbbc'.indexOf('b', 2);    // 2

// lastIndexOf(str, lastIndex?)
'abbbc'.lastIndexOf('b');    // 3
'abbbc'.lastIndexOf('b', 2); // 2

// for more complex scenarios you can use regular expressions
```

## Substring
``` javascript
// slice and substring are quite similar
// and can be used interchangeably in most cases

// slice(start, end?)
'abcdef'.slice(1);          // 'bcdef'
'abcdef'.slice(1, 4);       // 'bcd'

// substring(start, end?)
'abcdef'.substring(1);      // 'bcdef'
'abcdef'.substring(1, 4);   // 'bcd'

// substr(start, length?)
'abcdef'.substr(1);         // 'bcdef'
'abcdef'.substr(1, 4);      // 'bcde'
```

## Other functions
``` javascript
// split(separator, limit?)
'a b c d'.split(' ');   // ['a', 'b', 'c', 'd']);
'abcd'.split('', 3);    // ['a', 'b', 'c']);

// convert a string to lower case
'AbC'.toLowerCase();    // 'abc'

// convert a string to upper case
'AbC'.toUpperCase();    // 'ABC'

// trim whitespace: spaces, tabs, line terminators etc.
' \t abc \r\n '.trim(); // 'abc'
'  abc  '.trimStart();  // 'abc  '
'  abc  '.trimEnd();    // '  abc'

// repeat(count)
'ab'.repeat(2);         // 'abab'

// padStart(targetLength, padString?)
// padEnd(targetLength, padString?)
'abc'.padStart(5);      // '  abc'
'123'.padStart(5, '0'); // '00123'
'abc'.padEnd(5);      // 'abc  '
'123'.padEnd(5, '0'); // '12300'

```

## Regular expressions
``` javascript
// 1. match a string against a regular expression

// matchAll(regexp)
// - the most powerful and convenient matching method
// - is not supported by all browsers
// - more supported but slightly worse alternatives: RegExp.exec, String.match
// - returns an iterator of matches
// - a match is an array containing the match, groups and extra properties:
//     index - the starting index of the match
//     groups - an object representing named groups
//     input - a search string
const versions = 'Versions: 1.2.15 and 12.5.16';
const regexp = /(?<major>[0-9]+).(?<minor>[0-9]+).(?<patch>[0-9]+)/g;

for (let match of versions.matchAll(regexp)) {
    console.log(match[0]);              // matched string
    console.log(match[1]);              // a 1st group
    console.log(match.groups['major']); // named group
    console.log(match.index);           // match starting index
    console.log('-------');
}
// 1.2.15
// 1
// 1
// 10
// -------
// 12.5.16
// 12
// 12
// 21
// -------

// get an array of matches
const matches = [...versions.matchAll(regexp)];
console.log(matches[1][0]);              // 12.5.16
console.log(matches[1].groups['minor']); // 5

// if there no matches the array is empty
const noMatches = [...'abc'.matchAll(/[A-Z]+/g)];
const areThereAnyMatches = noMatches.length > 0;
console.log(noMatches);          // []
console.log(areThereAnyMatches); // false

// without the 'global' flag the iterator returns a single match
const arrayWithOneMatch = [...versions.matchAll(/[0-9]+.[0-9]+.[0-9]+/)];
console.log(arrayWithOneMatch.length); // 1
console.log(arrayWithOneMatch[0][0]); // 1.2.15


// 2. search a pattern in a string

// search(regexp) - returns the index of the first match or -1
'Version: 1.2.15'.search(/[0-9]+/); // 9
'Version: 1.2.15'.search(/[6-9]/);  // -1

// RegExp.test(str) - returns true or false
/[0-9]+/.test('Version: 1.2.15');   // true
/[6-9]+/.test('Version: 1.2.15');   // false


// 3. replace

// a. remove . ! and whitespaces (\s - matches any whitespace character)
'!!He l..lo!!'.replace(/[.!\s]+/g, ''); // 'Hello'

// b. remove all non-word characters (\w - matches any word character)
'!!He l..lo!!'.replace(/[^\w]+/g, '');  // 'Hello'


// 4. split
'1.2.3 and 2.3.1 or 3.2.1'.split(/[a-z ]+/);
// [ '1.2.3', '2.3.1', '3.2.1' ]
```

## Comparison
``` javascript
console.log('Alice' < 'Bob');              // true
console.log('Charlie' > 'Bob');            // true
console.log('Alice' === 'Alice');          // true
console.log('Alice'.localeCompare('Bob')); // -1
console.log('Bob'.localeCompare('Bob'));   // 0
console.log('Bob'.localeCompare('Alice')); // 1

// case-sensitive
console.log('BOB' === 'bob');            // false
console.log('BOB'.localeCompare('bob')); // 1

// case-insensitive
'BOB'.toUpperCase() === 'bob'.toUpperCase();                    // true
'BOB'.localeCompare('bob', undefined, { sensitivity: 'base' }); // 0

// sort characters within a string
[...'cebad'].sort().join(''); // abcde

// sort strings case-sensitive
[ 'bob', 'alice', 'Bob', 'Alice' ].sort();
// [ 'Alice', 'Bob', 'alice', 'bob' ]

// sort strings case-insensitive
[ 'bob', 'alice', 'Bob', 'Alice' ].sort((s1, s2) => {
    return s1.localeCompare(s2, undefined, { sensitivity: 'base' });
});
// ['alice', 'Alice', 'bob', 'Bob']
```
