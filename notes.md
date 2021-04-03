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

## String Methods

### Simple Concatenation

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

### .length

```js
val = firstName.length; // 7
```

### concat()

```js
val = firstName.concat(' ', lastName); // William Johnson
```

### Uppercase & Lowercase

```js
val = firstName.toUpperCase(); // WILLIAM
val = firstName.toLowerCase(); // william
```

### Indexing Strings

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

### indexOf()

Character matching is case-sensitive.

The `indexOf()` method returns `-1` if no such character exists.

```js
val = firstName.indexOf('W'); // 0
val = firstName.indexOf('w'); // -1
val = firstName.indexOf('l'); // 2 (first l in the string)
val = firstName.lastIndexOf('l'); // 3 (last l in the string) 
```

### charAt()

Similar to indexing the string.

An out of range index results in an empty string.

```js
val = firstName.charAt('2'); // l
val = firstName.charAt(2); // l
val = firstName.charAt(10); // empty string
val = firstName.charAt(firstName.length - 1); // m
```

### substring()

Extracts a section of a string

```js
val = firstName.substring(0, 4); // Will
```

### slice()

Similar to the `substring()` method, but can use negative numbers to get the last `n` characters.

```js
val = firstName.slice(0, 4); // Will
val = firstName.slice(1); // illiam
val = firstName.slice(-3); // iam
```

### split()

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

### replace()

Simply replaces a substring with a new substring

```js
val = greeting.replace('William', 'Josef'); // Hello! My name is Josef
```

### includes()

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

```js
numbers = [1, 2, 3, 4, 5];
numbers.reverse(); // [5, 4, 3, 2, 1]
```
