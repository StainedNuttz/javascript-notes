# Variables

## Declarations

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

Modifying the properties of mutable `const` variables doesn't involve reassigning the `const` itself, whereas reassigning a `const` would cause an error.

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
The same variable can hold multiple types, you do not define a type for the variable.

### Static typed language

Languages such as **C#**, **Java** and **C++** require variables to have a type declared for it.

There are supersets of **JavaScript** and addons which allow static typing such as **TypeScript** and **Flow**.

## Primitive types

Primitive data types are stored directly in the location that the variable accesses.

They are stored on the stack because their sizes are **static**.

### string

A sequence of characters

```js
const name = 'John Doe';
```

### number

A generic number.  
Can be a float, decimal, integer, etc.  
There is no separate data type for each!

```js
const age = 45;
```

### boolean

Either true or false

```js
const hasKids = true;
```

### null

An intentional empty value

```js
const car = null;
console.log(typeof car)
// returns 'object', which is a bug!
```

### undefined

a declared variable that isn't initialized

```js
let test;
```

### symbol

A new primitive type introduced in ES6

```js
const sym = Symbol();
```

## Reference types

Reference data types are **objects** that are accessed by reference. The variable stores a pointer to that actual data.  
They are referred to as **objects**! Using `typeof` will always yield `object`.  
The **actual** data is stored on the heap because their sizes are **dynamic**.

There are many different reference types, here are a few examples:

### array

A collection of data

```js
const hobbies = ['movies', 'music'];
```

### object

An object literal

```js
const address = {
  city: 'Boston',
  state: 'MA'
}
```

### function

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

## Type Conversion

Changing the data type of a variable can be useful.

One common case is storing a `<form>` input into a variable. By default, the variable will be of type `string`, and so to be able to apply calculations for example, you would parse that string into a `number`.

There a few ways for each type of conversion.

### → string

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

### → number

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

## Type Coercion

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
