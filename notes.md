<style>:not(pre) > code { color: purple !important; }</style>

# Variables
## `var`
Old method to declare variables.
**Avoid using** for best practice.

## `let`
New method to declare variables, use this instead of `var`.

## `const`
`const` variables cannot be reassigned.

Use `const` if you don't plan to reassign the variable

You can modify the properties of mutable `const` variables such as **arrays** and **objects**.

Modifying the properties of mutable `const` variables doesn't involve reassigning the `const` itself, whereas reassigning a `const` would cause an error.
```javascript
const a = 1;
a = 5; // ERROR

const b = [1, 2, 3];
b[0] = 3; // b: [3, 2, 3]
b.push[0]
b = [3, 3, 3]; // ERROR
```
With the above code, you can see how we are able to modify the data inside the array. But if we try to reassign the `const` variable as a whole to something else, it won't let us.

# Data Types

## Dynamically typed language
**JavaScript** is a dynamically typed language.
Types are associated with values not variables.
The same variable can hold multiple types, you do not define a type for the variable.

## Static typed languages
Languages such as **C#**, **Java** and **C++** require variables to have a type declared for it.

There are supersets of **JavaScript** and addons which allow static typing such as **TypeScript** and **Flow**.

#

## Primitive types
Primitive data types are stored directly in the location that the variable accesses.

They are stored on the stack because their sizes are **static**.

<br>

`string`

A sequence of characters
```js
const name = 'John Doe';
```
<br>

`number`

A generic number can be a float, decimal, integer, etc. 

There is no separate data type for each!
```js
const age = 45;
```
<br>

`boolean`

Either true or false
```js
const hasKids = true;
```
<br>

`null`

An intentional empty value
```js
const car = null;
console.log(typeof car) // returns 'object', which is a bug
```
<br>

`undefined`

a declared variable that isn't initialized
```js
let test;
```
<br>

`symbol`

A new primitive type introduced in ES6
```js
const sym = Symbol();
```

<br>

## Reference types
Reference data types are **objects** that are accessed by reference. The variable stores a pointer to that actual data.

They are referred to as **objects**! Using `typeof` will always yield `object`.

The **actual** data is stored on the heap because their sizes are **dynamic**.

There are many different reference types, here are a few examples.

<br>

`array`

A collection of data
```js
const hobbies = ['movies', 'music'];
```
<br>

`object`

An object literal
```js
const address = {
  city: 'Boston',
  state: 'MA'
}
```
<br>

`function`

We can reference a function using a variable.
```js
function add(a, b) {
  return a + b;
}

// This function is declared inside the variable rather than on its own like above
// This has effects on crap that we'll get too eventually
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
<br>

`date`

An object type used to represent dates

```js
const today = Date();
```





