# Fundamentals

## Variable Declarations

### var

Old method to declare variables.
**Avoid using** for best practice.

### let

New method to declare variables, use this instead of `var`.

### const

`const` variables cannot be reassigned.

Use `const` if you don't plan to reassign the variable

You cannot declare a `const` without an initial value.

```js
const item; // ERROR
const item = ... // GOOD
```

You can modify the properties of mutable `const` variables such as **arrays** and **objects**.

Modifying the properties of mutable `const` variables doesn't involve reassigning the `const` itself. Whereas, reassigning a `const` itself will cause an error.

```js
const a = 1;
a = 5; // ERROR

const b = [1, 2, 3];
b[0] = 3; // b: [3, 2, 3]
b.push[0]
b = [3, 3, 3]; // ERROR
```

With the above code, you can see how we are able to modify the data inside the array. But if we try to reassign the `const` variable as a whole to something else, it won't let us.

## Data Types

### Dynamically typed language

**JavaScript** is a dynamically typed language.
Types are associated with values not variables.
The same variable can hold multiple types, you do not define a type for a variable.

### Static typed language

Languages such as **C#**, **Java** and **C++** require variables to have a type declared for it.

There are supersets of **JavaScript** and addons which allow static typing such as **TypeScript** and **Flow**.

### Primitive types

Primitive data types are stored directly in the location that the variable accesses.

They are stored on the stack because their sizes are **static**.

#### string

A sequence of characters

```js
const name = 'John Doe';
```

#### number

A generic number.  
Can be a float, decimal, integer, etc.  
There is no separate data type for each!

```js
const age = 45;
```

#### boolean

Either true or false

```js
const hasKids = true;
```

#### null

An intentional empty value

```js
const car = null;
console.log(typeof car)
// returns 'object', which is a bug!
```

#### undefined

a declared variable that isn't initialized

```js
let test;
```

#### symbol

A new primitive type introduced in ES6

```js
const sym = Symbol();
```

### Reference types

Reference data types are **objects** that are accessed by reference. The variable stores a pointer to that actual data.  
They are referred to as **objects**! Using `typeof` will always yield `object`.  
The **actual** data is stored on the heap because their sizes are **dynamic**.

There are many different reference types, here are a few examples:

#### array

A collection of data

```js
const hobbies = ['movies', 'music'];
```

#### object

An object literal

```js
const address = {
  city: 'Boston',
  state: 'MA'
}
```

#### function

We can reference a function using a variable.

```js
function add(a, b) {
  return a + b;
}

// This function is declared inside the variable rather than on its own like above
// This has effects on crap that we'll get to eventually
const test = function() {
  let a = null;
  console.log(typeof a);
  // OUTPUT: object <- this is a bug
}

let c = add(1, 1);
console.log(c);
// OUTPUT: 2

const d = add;
console.log(d(1, 1));
// OUTPUT: 2
```

### date

An object type used to represent dates

```js
const today = Date();
```

## Converting Variables

### Type Conversion

Changing the data type of a variable can be useful.

One common case is storing a `<form>` input into a variable. By default, the variable will be of type `string`, and so to be able to apply calculations for example, you would parse that string into a `number`.

There a few ways for each type of conversion.

#### to string

Use the `String()` method.

```js
  let val = 5;
  val.length; // undefined
  
  val = String(5);
  val.length; // 1

  val = String(10+10); // '20'
  val.length; // 2

  val = String(true); // 'true'

  val = String(new Date());
  // 'Sat Apr 03 2021 07:52:25 GMT+0100 (British Summer Time)'

  val = String([1, 2, 3, 4]);
  // '1,2,3,4'
```

You can also use the `.toString()` method.

```js
val = (5).toString();
```

#### to number

```js
let val = '5';
val.toFixed(2); // ERROR
val = Number('5');
val.toFixed(2); // 5.00

val = Number(true); // 1
val = Number(false); // 0
val = Number(null); // 0
val = Number('hello'); // ERROR: NaN
val = Number([1,2,3]); // ERROR: NaN
```

`NaN` is an actual value in JavaScript, meaning "not a number".

There is also the `parseInt()` and `parseFloat()` method.

```js
val = parseInt('100'); // 100
val = parseInt('100.52'); // 100
val = parseFloat('100.52'); // 100.52
```

### Type Coercion

Type conversion is where we take a value and convert it into another.

Type coercion is where JavaScript does it for us.

```js
let val1 = 5;
let val2 = 6;
let val3 = val1 + val2; // 11 : number

val1 = String(5);
val2 = 6;
val3 = val1 + val2; // 56 : string
val3 = Number(val1 + val2); // 56 : number
```

JavaScript sees that `val1` is a `string` and therefore decides to convert `val2` into a string aswell, so that the values can be concatenated into a new string.

## The Math Library

The Math library has many useful methods.

```js
let val;

val = Math.PI; // 3.141...
val = Math.E; // 2.718...
val = Math.round(2.4); // 2
val = Math.ceil(2.4); // 3
val = Math.floor(2.8); // 2
val = Math.sqrt(64); // 8
val = Math.abs(-3); // 3
val = Math.pow(5, 2); // 25
val = Math.min(2, 33, 4, 1, 55, -6, 3); // -6
val = Math.max(2, 33, 4, 1, 55, -6, 3); // 55

val = Math.random(); // Random decimal between 0 and 1
val = Math.floor(Math.random() * 100 + 1); // Random number between 1 and 100, rounded down to an integer
```

## Strings

### Concatenation

```js
const firstName = 'William';
const lastName = 'Johnson';
let val;

val = firstName + lastName; // WilliamJohnson
val = firstName + ' ' + lastName // William Johnson 
```

### Appending

```js
val = 'Stian '; // Stian
val += 'Hazelgrove'; // Stian Hazelgrove
```

### Escaping

Escaping involves the `\` character.

Escaping simply takes the power away from syntax characters, treating the character as a normal text character.

This is useful because certain characters that define the JavaScript syntax, e.g. single quotes, can be escaped so that they act like a normal character in a string instead of ending the string like it normally would.

```js
val = 'That\'s awesome, I can\'t wait';
```

### Methods & Properties

#### .length

```js
val = firstName.length; // 7
```

#### concat()

```js
val = firstName.concat(' ', lastName); // William Johnson
```

#### Uppercase & Lowercase

```js
val = firstName.toUpperCase(); // WILLIAM
val = firstName.toLowerCase(); // william
```

#### Indexing Strings

You can index strings like arrays

```js
val = firstName[0]; // W
val = firstName[5]; // a
```

Strings are immutable so you cannot index a string to replace characters!

```js
val[5] = val[5].toUpperCase(); // stays as William
// Desired effect: WilliAm
```

#### indexOf()

Character matching is case-sensitive.

The `indexOf()` method returns `-1` if no such character exists.

```js
val = firstName.indexOf('W'); // 0
val = firstName.indexOf('w'); // -1
val = firstName.indexOf('l'); // 2 (first l in the string)
val = firstName.lastIndexOf('l'); // 3 (last l in the string) 
```

#### charAt()

Similar to indexing the string.

An out of range index results in an empty string.

```js
val = firstName.charAt('2'); // l
val = firstName.charAt(2); // l
val = firstName.charAt(10); // empty string
val = firstName.charAt(firstName.length - 1); // m
```

#### substring()

Extracts a section of a string

```js
val = firstName.substring(0, 4); // Will
```

#### slice()

Similar to the `substring()` method, but can use negative numbers to get the last `n` characters.

```js
val = firstName.slice(0, 4); // Will
val = firstName.slice(1); // illiam
val = firstName.slice(-3); // iam
```

#### split()

Very useful method. Splits a string into an array using a separating identifier (usually spaces).

```js
const greeting = "Hello! My name is William."
val = greeting.split(' '); // 0: Hello!
                           // 1: My
                           // 2: Name
                           // 3: is
                           // 4: William.

val = greeting.split('!'); // 0: Hello
                           // 1: My Name is William.
```

The identifier is excluded in the array.

#### replace()

Simply replaces a substring with a new substring

```js
val = greeting.replace('William', 'Josef'); // Hello! My name is Josef
```

#### includes()

Returns whether the substring exists in a string

```js
val = greeting.includes('W'); // true
val = greeting.includes('Wi'); // true
val = greeting.includes('Wii'); // false
val = greeting.includes('foo'); // false
```

## Template Literals

Template literals are a feature of ES5 and are compatible with all modern browsers.

Declaring some variables

```js
const name = 'John';
const age = 30;
const job = 'Web Developer';
const city = 'Miami';
let html;
```

Without template literals (horrible):

```js
html = 
"<ul>" +
"<li>Name: " + name + "</li>" +
"<li>Age: " + age + "</li>" +
"<li>Job: " + job + "</li>" +
"<li>City: " + city + "</li>" +
"</ul>";

document.body.innerHTML = html;
```

With template literals:

```js
html = `
  <ul>
    <li>Name: ${name}</li>
    <li>Age: ${age}</li>
    <li>Job: ${job}</li>
    <li>City: ${city}</li>
  </ul>
`;
```

Temporal literal blocks are defined by back ticks.

A placeholder for data is defined by:
`${ ... }`

Both of the code blocks achieve the exact same result onto the web page. Thank the lord for temporal literals!

You can even input other types of data such as expressions, conditionals, calculations and much more!

```js
`<li>${2 + 2}</li>`
`<li>${age > 18 ? 'adult' : 'child'}</li>`
```

## Arrays

Arrays are very useful

Arrays, just like variables, can contain anything

```js
// numbers
const numbers = [1, 2, 3, 4, 5];
// strings
const cars = ['BMW', 'Audi', 'Volkswagen', 'Kia'];
// mixed
const mixed = ['cool', 1, null, undefined, {a:1, b:1}, true, new Date()];
```

Arrays can also be initialized by using the `Array()` constructor!

```js
const numbers2 = new Array(1, 2, 3, 4, 5);
```

### Array Methods & Properties

```js
const numbers = [1, 2, 3, 4, 5];
let val; // undefined

val = numbers.length; // 5
val = Array.isArray(numbers); // true
val = numbers[0]; // 1
val = numbers.indexOf(3); // 2
```

### Mutating Arrays

Unlike strings, arrays are mutable so you can change their values by index and do other things to change up the array.

#### Adding and Taking off values

```js
// Replacing a value at a specific index
numbers[2] = 1; // [1, 2, 1, 4, 5]

// Adding on
numbers.push(6); // [1, 2, 1, 4, 5, (6)]
numbers.unshift(0); // [(0), 1, 2, 1, 4, 5, 6]

// Taking off
numbers.pop(); // [0, 1, 2, 1, 4, 5] -> (6)
numbers.shift(); // (0) <- [1, 2, 1, 4, 5]
```

#### splice()

Removes a subarray from the array: `splice(startingPoint, endingPoint)`

The starting and end points are **inclusive**.

```js
numbers = [1, 2, 3, 4, 5];
numbers.splice(1, 3); // [1, 5]
```

#### reverse()

Simply reverses the array's contents

```js
const numbers = [1, 2, 3, 4, 5];
numbers.reverse(); // [5, 4, 3, 2, 1]
```

#### concat()

Concatenates arrays together

```js
const numbers1 = [1, 2, 3, 4, 5];
const numbers2 = [6, 7, 8, 9, 10];
numbers1.concat(numbers2); // returns [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

#### sort()

```js
const names = ['Stian', 'Sandra', 'Josef', 'Rosi', 'Mario'];
names.sort(); // returns ['Josef', 'Mario', 'Rosi', 'Sandra', 'Stian']

const numbers = [21, 32, 34, 11, 4, 121, 1945];
numbers.sort(); // returns [11, 121, 1945, 21, 32, 34, 4] 
```

By default, the `sort()` method sorts the array's values by converting the values to strings and comparing their Unicode values.

If you pass in a callback function, the `sort()` method will sort the array defined by that function.

The `sort()` method calls the callback function for each array element **and** the element preceding it, so that it can compare both of them.

With the callback function, you want to return either a:

* negative number
* zero
* positive number

The `sort()` method does something with those two elements determined by the return value of the callback function.

`negative number = values are not swapped`

`zero (same number basically) = values are not swapped but count as sorted`

`positive number = values are swapped`

So in conclusion, if you would `return a - b`, you're basically comparing the numbers in ascending order:

* if a < b, then no swap
* if a = b, then no swap, but count as sorted
* if a > b, then swap

Likewise for `return b - a`, you're comparing the numbers in descending order:

* if b < a, then no swap
* if b = a, then no swap, but count as sorted
* if b > a, then swap

```js
let val;
val = numbers.sort(function(a, b) {
  return a - b;
}); // val = [4, 11, 21, 32, 34, 121, 1945]

val = numbers.sort(function(a, b) {
  return b - a;
}); // val = [1945, 121, 34, 32, 21, 11, 4]
```

`a - b` and `b - a` are the ones to remember

#### find()

Finds the first value in an array, that satisfies the provided function.

```js
const ages = [2, 8, 44, 31, 5, 66];
function over18(num) {
  return num > 18;
}

ages.find(over18); // returns 44
```

## Object Literals

Simple way to define objects and access their properties and methods.

`this` is used to refer to itself when accessing properties from inside the object.

```js
const person = {
  firstName: 'Steve';
  age: 56;
  email: 'steve@gmail.com';
  hobbies: ['music', 'sports'];
  address: {
    city: 'Berlin',
    houseNumber: 4
  }
  getBirthYear: function() {
    return 2021 - this.age;
  }
}

let val;

val = person; // object
val = person.firstName; // 'Steve'
val = person['firstName'] // 'Steve'
val = person.age; // 79
val = person.hobbies[1]; // 'sports'
val = person.address.city; // 'Berlin'
val = person.getBirthYear(); // returns 1942
```

`person.firstName` is preferred over `person['firstName']`

## Dates & Times

Dates & times are very important in programming, JavaScript has the `Date` object which defines methods and properties for using dates & times.

The default constructor for `Date` returns the current time and date.

```js
const today = new Date();
// logs Sat Apr 03 2021 13:04:35 GMT+0100 (British Summer Time)
```

### Creating Date Objects

There are many ways to create dates in JavaScript:

```js
let date = new Date('8 1 2001');
// logs Wed Aug 01 2001 00:00:00 GMT+0100 (British Summer Time)

date = new Date('8 1 2001 18:32:42');
// logs Wed Aug 01 2001 18:32:42 GMT+0100 (British Summer Time)

date = new Date('August 1 2001');
// Wed Aug 01 2001 18:32:42 GMT+0100 (British Summer Time)

date = new Date('3/4/2016');
// logs Fri Mar 04 2016 00:00:00 GMT+0000 (Greenwich Mean Time)

console.log(typeof date); // object
```

### Getting Properties

Because `Date` is an object, we can access its methods!

```js
let val;
const today = new Date();
// Sat Apr 03 2021 13:15:42 GMT+0100 (British Summer Time)

val = today.getMonth();
// returns 3
// getMonth() is zero-based

val = today.getDate();
// returns 3 (day of the month)

val = today.getDay();
// returns 6 (Sun-Sat (0 - 6))

val = today.getFullYear();
// returns 2021

val = today.getHours();
// 13

val = today.getMinutes();
// 22

val = today.getSeconds();
// 42

val = today.getMilliseconds();
// 821

val = today.getTime();
// 1614777647420 -> seconds since 1-1-1970 00:00:00
```

### Setting Properties

We can also access the defined `set` methods to manipulate the data on a `Date` object!

```js
const birthday = new Date('August 1 2001');
birthday.setMonth(1);
birthday.setDate(31);
birthday.setFullYear(1066);
birthday.setHours(14);
birthday.setMinutes(30);
birthday.setSeconds(59);

console.log(birthday);
// logs: Sat Mar 03 1066 14:30:59 GMT-0001 (Greenwich Mean Time)
```

Note how `February 31st` rolls over to `March 3rd`!

## Conditions

### Comparisons

#### Equality

`===` is preferred over `==` as it compares the type as well as the value, this stops issues from arising, e.g:

```js
'100' == 100
// true

'100' === 100
// false
```

Use **===** and **!==**

#### Undefined Checking

In other languages you might want to check if a variable is `null` or undefined by just using:

```txt
if (id) {
  print("ID!");
} else {
  print("NO ID!");
}
```

In JavaScript, this shoots out an error.

So instead, we check the type of the variable.

```js
if (typeof id !== 'undefined') {
  console.log(`ID IS ${id}`);
} else {
  console.log('NO ID');
}
```

#### Logical Operators

The logical operators are defined as:

* AND &&
* OR ||

#### Ternary Operator

A shorthand for an IF statement:

`(condition statement) ? value1 : value2`

If the condition is true, return value1  
Otherwise, return value2

```js
function calculatePrice(isMember) {
  return isMember ? '$2.00' : '$10.00';
}

calculatePrice(true); // '$2.00'
calculatePrice(false); // '$10.00'
calculatePrice(null); // '$10.00'
```

### Switch Statements

Switch statements are preferred over IF ELSE blocks.

```js
let day;

switch(new Date().getDay()) {
  case 0:
    day = 'Sunday';
    break;
  case 1:
    day = 'Monday';
    break;
  case 2:
    day = 'Tuesday';
    break;
  case 3:
    day = 'Wednesday';
    break;
  case 4:
    day = 'Thursday';
    break;
  case 5:
    day = 'Friday';
    break;
  case 6:
    day = 'Saturday';
    break;
  default:
    day = 'Payday';
    break;
}

console.log(`Today is ${day}`);
```

A default case is met when no cases are met.

## Functions

### Function Declaration

```js
function functionName(a, b, c) {}
```

Avoid doing this for argument validation:

```js
function greet(firstName) {
  if (typeof firstName === 'undefined') { firstName = 'John' }
  return firstName;
}
```

Do this instead:

```js
function greet(firstName = 'John') {
  return firstName;
}
```

### Function Expressions

Function expressions have benefits over function declarations for more advanced things such as closures & hoisting.

```js
const square = function(x) {
  return x * x
};

console.log(square(8)); // 64

```

An **anonymous** function is declared in the above code.

### Immediately Invokable Function Expressions (IIFE's)

Functions that are declared and called at the same time, very useful for the module design pattern.

```js
(function(name){
  console.log('Hello ' + name);
})('Stian');

// 'Hello Stian'
```

### Functions in Objects

```js
const food = {
  name: 'Apple',
  eat: function(name = this.name) {
    console.log('eating ' + name);
  },
  throw: function(name = this.name) {
    console.log('throwing ' + name);
  }
}

food.eat('Orange'); // 'eating Orange'
food.throw(); // 'throwing Apple'

food.pickUp = function(name = this.name) {
  console.log('picking up ' + name);
}

food.pickUp(); // 'picking up Apple'
```

## Loops

### Do While Loop

Do while loops are similar to while loops, except that they always run **one** interation no matter what.

```js
let i = 100;

do {
  console.log('Number: ' + i);
  i++;
}

while (i < 10);

// OUTPUT: 'Number 100'
```

### Array.forEach()

```js
const people = ['John', 'Alex', 'Sandra', 'Max'];

people.forEach(function(person) {
  if (person !== 'Sandra') {
    console.log('Person ' + person + ' is annoying');
  }
});
```

`forEach()` can take 3 arguments:

```js
Array.forEach(iterator, index, array);
// iterator is the current value
// index is the index of the current value
// array is the entire array
```

### map()

```js
const users = [
  { id: 1, name: 'Apple' },
  { id: 2, name: 'Orange' },
  { id: 3, name: 'Banana' } 
];

const ids = users.map(function(user) {
  return user.id;
});
```

### For in Loop

Used for objects!

```js
const human = {
  bones: true,
  skin: true,
  blood: true,
  canFly: false,
  lifeSpan: 70
}

for (let x in human) {
  console.log(`${x} : ${human[x]}`);
}
```

## The Window Object

The global object in client-side JavaScript is the `window` object.

`document` and `console` are apart of `window`

We could use:

```js
window.alert();
window.console.log();
window.document.getElementById();
```

But we don't need the `window` as we are already at the top of `window` because it's the global object on the client.

### Window Methods

Old school methods, but `alert()` is still used.

#### Alert

```js
alert('hello');
```

#### Prompt

```js
const input = prompt();
alert(input);
```

#### Confirm

```js
if (confirm('Are you sure?')) {
  console.log('yes');
} else {
  console.log('no');
}
```

### Window Properties

'window' has many useful properties we might want to use.

#### Outer Height & Width

Outer measurements are the browser window dimensions.

```js
window.outerHeight;
window.outerWidth;
```

#### Inner Height & Width

Inner measurements are the browser window dimensions **but** including any scrollbars, the dev tools menu, etc.

```js
window.innerHeight;
window.innerWidth;
```

#### Scroll Points

Scroll points are the positions you are on the scroll axis, useful for sites that have certain animations triggering at a certain scroll point threshold (usually scrollY).

```js
window.scrollY;
window.scrollX;
```

### Location Object

The location object contains values such as the hostname, port, URL search parameters, and much more!

#### Various Location Properties

Various properties that can be returned.

```js
window.location;
window.location.hostname; // domain name
window.location.port;
window.location.href; // url
window.location.search; // gets search parameters
```

#### location.href

Redirects you to the entered URL.

```js
window.location.href = 'https://stianhazel.xyz';
```

#### location.reload()

Reloads the page.

```js
window.location.reload();
```

The above method being used globally would cause the page to reload infinitely.

### History Object

Used to get browser history data.

#### history.go()

Redirects you to the `n`th url in the browser history stack.

```js
window.history.go(-2); // sends you 2 pages back
```

#### history.length

Returns the browser history stack length

```js
window.history.length; // 6 (6 sites behind us)
```

### Navigator Object

The `navigator` object contains data about the browser application, **not** the webpage.

```js
window.navigator;
window.navigator.appName; // 'Netscape' (unless on IE)
window.navigator.appVersion; // '5.0 (X11)'
window.navigator.userAgent; // 'Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:87.0) Gecko/20100101 Firefox/87.0'
window.navigator.platform; // 'Linux x86_64'
window.navigator.vendor; // ''
window.navigator.language; // 'en-GB'
```


## Scopes

### Function Scopes

Declared within a function

```js
// global scope
var a = 1;
let b = 2;
const c = 3;

function test() {
  // function scope
   var a = 4;
   let b = 5;
   const c = 6;
   console.log(a, b, c);
}
test(); // 4 5 6
console.log(a, b, c); // 1 2 3
```

`var`, `let` and `const` variables can be declared in the function scope, independent of the global scope.

### Block Scopes

Includes loops, if statements, switch statements

```js
var a = 1;
let b = 2;
const c = 3;

if (true) {
  // block scope
  var a = 10;
  let b = 20;
  const c = 30;
  console.log(a, b, c); // 10 20 30
}

console.log(a, b, c); // 10 2 3
```

`var` variables don't have a block scope, they are declared in the global scope when used in block statements. This is why the global `var a` changed; it was redeclared in the if statement because `var` has no block scope.

ES6 introduced the `let` and `const` keywords, these keywords could declare variables within the block scope, independent of the global scope.

This was an important feature because `var` declarations in block statements were still in the global scope and therefore caused problems.

Another example:

```js
var a = 1;
let b = 2;
const c = 3;

for (var a = 0; a < 10; a++) {
  // loop scope
  console.log(`Loop: ${a}`);
  // Loop: 1 - 9
}

console.log(a, b, c); // 1 2 10
```

Not good. This loop scope defines `var a = 0` and therefore redeclares the global `var a`.

This is why `var` sucks.

This is one main reason why `let` and `const` was created!

**Stop using `var`!**
