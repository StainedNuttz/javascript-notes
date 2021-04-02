<style>:not(pre) > code { color: purple !important; }</style>

# Variables
**Do not** use `var`

Use `let` instead

`const` variables cannot be reassigned

Use `const` if you don't plan to reassign the variable

You can however modify the properties of certain `const` variables such as **arrays** and **objects**

```js
const a = 1;
a = 5; // ERROR

const b = [1, 2, 3];
b[0] = 3; // b: [3, 2, 3]
b.push[0]
b = [3, 3, 3]; // ERROR
```

## Data Types
### Primitive
Primitive data types are stored directly in the location the variable accesses
Stored on the stack
<br><br>
#### string
```js
const name = 'John Doe';
```

- number
- boolean
- null
  - Intentional empty value
- undefined
  - Non-initalized variable, only declared
- symbols (ES6)

### Reference
Accessed by reference
Object that are stored on the heap
A pointer to a location in memory
- arrays
- object literals
- functions
- dates
- anything else...

## Dynamically typed
**JavaScript** is a dynamically typed language.
Types are associated with values not variables.
The same variable can hold multiple types, you do not define a type for the variable.

### Static typed languages
Languages such as **C#**, **Java** and **C++** require variables to have a type declared for it.

There are supersets of **JavaScript** and addons which allow static typing such as **TypeScript** and **Flow**.






