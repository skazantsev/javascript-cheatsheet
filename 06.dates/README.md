# Dates

## Creation
``` javascript
// current date and time
new Date();

// from unix epoch
const epoch = 946684800; // 2000-01-01T00:00:00.000Z
new Date(epoch * 1000);

// from string
new Date('2000-01-01');               // parsed as UTC
new Date('2000-01-01T12:00:00.000Z'); // parsed as UTC
new Date('1 January 2000');           // parsed in the local timezone;
                                      // if the local timezone is UTC+1 the result is 1999-12-31T23:00:00.000Z

// explicit construction (local timezone)
// - new Date(year, monthIndex, day?, hours?, minutes?, seconds?, milliseconds?);
// - monthIndex starts from 0
new Date(2000, 0, 1);                 // 1999-12-31T23:00:00.000Z
new Date(2000, 0, 1, 12, 0, 0, 0);    // 2000-01-01T11:00:00.000Z

// explicit construction (UTC)
new Date(Date.UTC(2000, 0, 1));                 // 2000-01-01T00:00:00.000Z
new Date(Date.UTC(2000, 0, 1, 12, 0, 0, 0));    // 2000-01-01T12:00:00.000Z

// clone
const now = new Date();
const cloned = new Date(now.getTime());
```

## Conversion to milliseconds or unix epoch
``` javascript
// number of milliseconds from 1970-01-01T00:00:00.000Z
Date.now(); // 946684800000
// or
new Date().getTime();

// get unix epoch (seconds)
Math.round(Date.now() / 1000); // 946684800
```

## Compare
``` javascript
// dates are compared by reference
const now = new Date();
const cloned = new Date(now.getTime());
console.log(now === cloned);                     // false

// use getTime to compare by value
console.log(now.getTime() === cloned.getTime()); // true

// sort example
const dates = [
    new Date(Date.UTC(2000, 0, 1)),
    new Date(Date.UTC(2001, 0, 1)),
    new Date(Date.UTC(1990, 0, 1)),
];
dates.sort((x, y) => x.getTime() - y.getTime());
// [
//   1990-01-01T00:00:00.000Z,
//   2000-01-01T00:00:00.000Z,
//   2001-01-01T00:00:00.000Z
// ]
```

## Get / set
``` javascript
const date = new Date(Date.UTC(2000, 1, 2, 13, 15, 24, 200)); // 2000-02-02T13:15:24.200Z

// get methods (based on the local timezone)
date.getFullYear();      // 2000
date.getMonth();         // 1 (0 - January, 1 - February)
date.getDate();          // 2 - day of the month
date.getHours();         // 14
date.getMinutes();       // 15
date.getSeconds();       // 24
date.getMilliseconds();  // 200
date.getDay();           // 3 - day of the week (0 - Sunday, 3 - Wednesday)

// get methods (based on UTC)
date.getUTCFullYear();      // 2000
date.getUTCMonth();         // 1 (0 - January, 1 - February)
date.getUTCDate();          // 2 - day of the month
date.getUTCHours();         // 13
date.getUTCMinutes();       // 15
date.getUTCSeconds();       // 24
date.getUTCMilliseconds();  // 200
date.getUTCDay();           // 3 - day of the week (0 - Sunday, 3 - Wednesday)

// get milliseconds from 1970-01-01
date.getTime();

// get timezone offset in minutes
date.getTimezoneOffset();  // -60

// set methods (based on the local timezone)
date.setFullYear(2001);
date.setMonth(0);
date.setDate(1);
date.setHours(10);
date.setMinutes(30);
date.setSeconds(25);
date.setMilliseconds(150);
console.log(date.toISOString());  // 2001-01-01T09:30:25.150Z

// set methods (based on UTC)
date.setUTCFullYear(2001);
date.setUTCMonth(0);
date.setUTCDate(1);
date.setUTCHours(10);
date.setUTCMinutes(30);
date.setUTCSeconds(25);
date.setUTCMilliseconds(150);
console.log(date.toISOString());  // 2001-01-01T10:30:25.150Z

// set time
date.setTime(946684800000);
console.log(date.toISOString());  // 2000-01-01T00:00:00.000Z

// example: get start of today and yesterday
const today = new Date(new Date().getTime());
today.setUTCHours(0, 0, 0, 0);
console.log(today); // 2020-06-28T00:00:00.000Z

const yesterday = new Date(today.getTime());
yesterday.setUTCDate(today.getUTCDate() - 1);
yesterday.log(today); // 2020-06-27T00:00:00.000Z
```

## Formatting
``` javascript
const date = new Date(Date.UTC(2000, 0, 1));

// ISO 8601
date.toISOString();        // '2000-01-01T00:00:00.000Z'

// toLocaleString(locales?, options?)
date.toLocaleString();                             // formatted according to the current timezone
date.toLocaleString('en-US');                      // 1/1/2000, 1:00:00 AM
date.toLocaleString('en-US', { hour12: false });   // 1/1/2000, 1:00:00
date.toLocaleString('en-GB', { timeZone: 'UTC' }); // 01/01/2000, 00:00:00

// toLocaleDateString(locales?, options?)
date.toLocaleDateString('nl-NL'); // 1-1-2000

// toLocaleTimeString(locales?, options?)
date.toLocaleTimeString('en-US', { timeZone: 'UTC' }); // 12:00:00 AM

// using Intl.DateTimeFormat
// https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Intl/DateTimeFormat/DateTimeFormat
const dateFormatter = new Intl.DateTimeFormat('en-US', { year: 'numeric', month: 'short', day: 'numeric' });
const timeFormatter = new Intl.DateTimeFormat('en-US', { hour: '2-digit', minute: '2-digit', hour12: false });

console.log(`${dateFormatter.format(date)} ${timeFormatter.format(date)}`); // Jan 1, 2000 01:00

// methods to avoid
date.toString();           // 'Sat Jan 01 2000 01:00:00 GMT+0100 (Central European Standard Time)'
date.toDateString();       // 'Sat Jan 01 2000'
```
