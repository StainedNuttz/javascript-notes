# The DOM (Document Object Model)

Content

## Introduction

A structured representation of an HTML document.

Can be thought of as a tree of nodes/elements created by the browser.

We can use JavaScript to manipulate the DOM.

Nowadays, libraries such as jQuery isn't needed when we now have things like the `querySelector` in vanilla JavaScript.

## The Document Object

The `document` object stores the whole HTML document starting with `<!DOCTYPE html>` down to `</html>`.

### Document Properties

The collection of elements are **NOT** arrays, they are an HTML collection.

They refer to actual living HTML tags in the current document.

`document` property examples:

```js
document.all; // 32 [html, head, meta, meta, link, ...]
document.all[2]; // <meta>...</meta>
document.all.length; // 32
document.head; // <head>...</head>
document.body; // <body>...</body>
document.doctype; // <!DOCTYPE html>
document.domain; // 127.0.0.1
document.url; // http://127.0.0.1:5500/index.html
document.characterSet; // UTF-8
document.contentType; // text/html

document.forms; // [form#form1, form#form2]
document.forms[2]; // <form id="form2">...</form>
document.forms[3]; // undefined
document.forms[2].id; // form2
document.forms[2].action // https://127.0.0.1:5500/index.php
document.forms[2].method; // get

document.links; // [a.btn, a.btn, a.btn, a.btn.btn-clear]
document.links[3]; // <a class="btn btn-clear">...</a>
document.links[3].className; // ['btn', 'btn-clear']
document.links[3].classList[0]; // btn

document.images; // [] (no images)

document.scripts; // (3) [script, script, script]
document.scripts[2].getAttribute('src'); // 'home.js'
```

You can convert a Node list into an array so that you can perform array methods.

```js
let scripts = document.scripts;
let scriptsArr = Array.form(scripts);
scriptsArr.forEach(function(script) {
  console.log(script.getAttribute('src'));
});

// [app.js, sample.js, home.js]
```

### Document Selectors

jQuery was highly used for DOM manipulation.

Vanilla JavaScript is very good at doing this on its own now. Scripts that are dependent on jQuery, is one reason to use jQuery.

**Use** vanilla JavaScript for DOM manipulation.

#### Single Selectors

##### document.getElementById()

```js
const clearTasks = document.getElementById('clear-tasks');

clearTasks; // <a id="clear-tasks" class="btn btn-dark">...</a>
clearTasks.id; // 'clear-tasks'
clearTasks.className; // 'btn btn-dark'

clearTasks.style.background = '#333';
clearTasks.style.padding = '2rem';
clearTasks.style.display = 'none';

clearTasks.textContent = 'Clear Tasks';
clearTasks.innerText = 'Clear Tasks Forever';
clearTasks.innerHTML = '<span style="color:red">Clear Tasks</span>';
```

##### document.querySelector()

Very powerful.

We can just use CSS selectors!

```js
document.querySelector('#task-title');
document.querySelector('.btn');
document.querySelector('.btn.btn-dark');
// All return
// <a id="clear-tasks" class="btn btn-dark">...</a>

document.querySelector('h1');
// If multiple, selects first one
// <h1>My Document</h1>
```

We can use psuedo selectors too:

```js
document.querySelector('ul li').style.color = 'blue';
document.querySelector('li:last-child').style.color = 'red';
document.querySelector('li:after').position = 'absolute';
```

#### Multiple Selectors

##### document.getElementsByClassName

```js
const items = document.getElementsByClassName('item');
// NOT ARRAY, HTML COLLECTION!
// [li.item, li.item, li.item, li.item, li.item]

items[0]; // 0 : <li class="item"></li>
items[2].style.color = 'red';
items[2].textContent = 'hello world';
items[2]; // 2 : <li class="item" style="color: red;">hello world</li>

const listItems = document.querySelector('ul').getElementsByClassName('item'); // [li.item, li.item ...]
```

##### document.getElementsByTagName()

```js
const lis = document.getElementsByTagName('li');
// [li.item, li.item ...]

lis = Array.form(lis);
lis.reverse();
lis.forEach(function(li, index)) {
  conole.log(`${index} : ${li.className});
} 
// 1 : item
// 2 : item
// 3 : item
```

##### document.querySelectorAll()

Returns a node list, rather than an HTML collection.

Allows us to use array methods without having to convert anything to an array.

```js
const items = document.querySelectorAll('ul.items li.item');
//[0: li.item]
//[1: li.item]
//...

items.forEach(function(item, index) {
  item.textContent = `${index} : Hello`;
  // Each li.item says 'Hello' on the page
});

const liOdd = document.querySelectorAll('li:nth-child(odd)');
const liEven = document.querySelectorAll('li:nth-child(even)');

liOdd.forEach(function(li, index) {
  li.style.color = 'red';
});

for (let i = 0; i < liEven.length; i++) {
  liEven[i].style.background = '#000';
}
```

## Traversing the DOM

```js
const list = document.querySelector('ul.items');
list.childNodes; // NODE LIST
                 // 0: text, 1: li.item, 2: text, 3: li.item ...
list.childNodes[0]; // 0: text
list.childNodes[0].nodeName; // text
```

The above example returns **nodes**, which includes the text nodes.

The line breaks in the HTML count as text nodes.

To get elements, not nodes:

```js
list.children; // [li.item, li.item, li.item ...]
               // HTML COLLECTION
```

Let's say we wanted to get the first child element:

```js
list.firstChild; // #text (text node)
```

No! We don't want the useless text nodes, we want the first child ELEMENT:

```js
list.firstElementChild; // <li class="item">...</li>
```

Children element count:

```js
list.childElementCount; // 5
```

You can see how we can traverse the DOM:

```js
list; // li
list.parentElement; // li < ul
list.parentElement.parentElement; // li < ul < div
list.parentElement.parentElement.nextElementSibling; // footer
list.parentElement.parentElement.previousElementSibling; // header
list.parentElement.parentElement.previousElementSibling.children[0]; // header > h1
list.parentElement.parentElement.previousElementSibling.children.previousElementSibling; // null, no such element

```

### Node Type Values

- 1 : Element
- 2 : Attribute (deprecated)
- 3 : Text Node
- 8 : Comment
- 9 : Document itself
- 10 : Doctype

```js
const list = document.querySelector('ul.items');
list.childNodes; // NODE LIST
                 // 0: text, 1: li.item, 2: text, 3: li.item ...
list.childNodes[0]; // 0: text
list.childNodes[0].nodeName; // text

list.childNodes[0].nodeType; // 3
list.childNodes[1].nodeType; // 1
```

## Creating Elements

Adding a new `li.item` to the `ul.items`:

```js
const li = document.createElement('li');
li.className = 'item';
li.id = 'special-item';
li.setAttribute('title', 'New Item');
li.appendChild(document.createTextNode('hi'));

const closeBtn = document.createElement('a');
closeBtn.className = 'delete-item red';
closeBtn.innerHTML = '<i class="fa fa-remove"></i>';
closeBtn.href = "#";

li.appendChild(closeBtn);
document.querySelector('#items').appendChild(li);

/* 
<ul id="items">
  <li id="special-item" class="item" title="New Item">
    hi
    <a href="#" class="delete-item red">
      <i class="fa fa-remove"></i>
    </a>
  </li>
</ul>
*/
```

## Replacing Elements

We can also replace elements:

```js
/*
<a href="#" class="delete-item red">
  <i class="fa fa-remove"></i>
</a>
*/

const oldIcon = document.querySelector('.delete-item i');
const newIcon = document.create('i');
const parent = oldIcon.parentElement; // a

newIcon.className = 'potato';
oldIcon.replaceChild(newIcon, oldIcon);
/*
  <a href="#" class="delete-item red">
    <i class="potato"></i>
  </a>
*/
```

## Removing Elements

And we can remove elements:

```js
/*
<a href="#" class="delete-item red">
  <i class="fa fa-remove"></i>
</a>
*/

const icon = document.querySelector('i.fa.fa-remove');
icon.remove();

/*
<a href="#" class="delete-item red">
</a>
*/
```

You can also do:

```js
const parent = icon.parentElement;
parent.removeChild(icon);
```

## Editing Elements

We can edit the classes of an element:

```js
const li = document.querySelector('li');

li.className; // 'item item-fruit'
li.classList; // DOM Token List [item, item-fruit]
li.classList[1]; // 'item-fruit'
li.classList.add('show');
li.classList; // DOM Token List [item, item-fruit, show]
```

We can also edit the attributes of an element:

```js
li.getAttribute('href'); // null
li.hasAttribute('href'); // false

li.setAttribute('href', '#');
li.getAttribute('href'); // #
li.hasAttribute('href'); // true

li.removeAttribute('href');
li.getAttribute('href'); // null
li.hasAttribute('href'); // false
```

## The Event Object & Event Listeners

```js
//<a href="https://stianhazel.xyz"></a>

document.querySelector('a').addEventListener('click',
function(e) {
  console.log('hello world');
});
```

When we click, we will see `'hello world'` in the console but immediately after, redirect to `https://stianhazel.xyz`.

We can prevent this default behaviour:

```js
document.querySelector('a').addEventListener('click',
function(e) {
  console.log('hello world');
  e.preventDefault();
});
```

This stops the redirect.

When you hover over the link, it will still highlight that it redirects to `https://stianhazel.xyz`, even though we prevented the default behaviour. This is because we did this on the `click` event, not anywhere else!

### Event Details

You can print the details of an event:

```js
//<a href="https://stianhazel.xyz"></a>

document.querySelector('a').addEventListener('click',
function(e) {
  e.target; // <a href="https://stianhazel.xyz"></a>
  e.type; // click
  e.timeStamp; // 3723

  // coordinates relative to the window
  e.clientY; // 540 (540px from the top)
  e.clientX; // 216 (77px from the left)
  
  // coordinates relative to the element
  e.offsetY; // 32px (32px from the left)
  e.offsetX; // 140px (140px from the top)


});
```

### Mouse Events

```js
const clearBtn = document.querySelector('#clear-tasks');
const card = document.querySelector('.card');

function runEvent(e) {
  console.log(`EVENT: ${e.type}`);
}

// on click
clearBtn.addEventListener('click', runEvent);
// on double click
clearBtn.addEventListener('dblclick', runEvent);

// on holding mouse down
clearBtn.addEventListener('mousedown', runEvent);
// on releasing mouse hold
clearBtn.addEventListener('mouseup', runEvent);
// on ANY mouse movement
clearBtn.addEventListener('mousemove', runEvent);  
```

#### mouseenter/mouseleave & mouseover/mouseout

`mouseenter` is fired when the mouse enters the bounds of the element. Any children of this element are **apart** of the element's bounds. So upon leaving the main element's bounds, `mouseleave` is fired.

`mouseover` on the other hand, is fired when the mouse enters the bounds of the element, but any children elements are **not apart** of the element's bounds. So upon entering a child element of the main element, `mouseout` is fired.

`mouseover` is fired again once the mouse leaves the child element and re-enters the main element's bounds.

### Input & Form Events

```js
const form = document.querySelector('form');
const input = document.querySelector('input[type="text"]');

input.addEventListener('keydown', function(e) {
  // get the event target's value
  let txt = e.target.value;
});

form.addEventListener('submit', function(e) {
  // prevent redirect ,m
  console.log(input.value);
  e.preventDefault();
});
```

There is also:

```js
input.addEventListener('focus');
input.addEventListener('blur');

input.addEventListener('cut');
input.addEventListener('paste');

// any input interaction (typing, clicking, etc) fires this event
input.addEventListener('input');

const select = document.querySelector('select');
// fired when value changed
select.addEventListener('change');
```

## Event Bubbling & Delegation

### Event Bubbling

When an event is fired, events are bubbled up through the DOM.

An event on any element will bubble up to its parent (if the parent has the same event listener), then that parent's parent, then that parent's parent's parent, and so on...

```js
document.querySelector('.card-title').addEventListener('click', function() {
  console.log('card title');
});

document.querySelector('.card-container').addEventListener('click', function() {
  console.log('card container');
});

document.querySelector('.card').addEventListener('click', function() {
  console.log('card');
});

document.querySelector('.container').addEventListener('click', function() {
  console.log('main container');
});

// when clicking on the card-title element:

// card title
// card container
// card
// main container
```

`e.target` is still recognized as the original clicking point.

For example, if we click on `.card-title`, the event bubbles up the DOM, firing parent `click` events.

But each event that is fired from bubbling, it will still recognize the `event.target` being `.card-title` (the original clicking point).

### Event Delegation

Event delegation is basically when we add an event listener on a parent of what we're looking for and using a condition to find the desired target to add functionality to.

Let's say we have this HTML and we want to have each `delete-item` button to fire a `click` event.

```html
<ul>
  <li class="item">
    <a href="#" class="delete-item">
      <i class="fa fa-remove"></i>
    </a>
  </li>
  <li class="item">
    <a href="#" class="delete-item">
      <i class="fa fa-remove"></i>
    </a>
  </li>
  <li class="item">
    <a href="#" class="delete-item">
      <i class="fa fa-remove"></i>
    </a>
  </li>
</ul>
```

```js
const deleteItem = document.querySelector('.delete-item');
deleteItem.addEventListener('click', function() {
  console.log('delete item');
});
```

This event fires **only** when clicking on the first `.delete-item` element in the `ul`.

This is one situation where we need to use event delegation.

Another situation is if we had inserted a new `.delete-item` element into the `ul` through JavaScript that wasn't there when the page loaded.

If we want the same event to be fired on each `.delete-item` element, we can do this:

```js

document.body.addEventListener('click', function(e) {
  console.log(e.target);
  console.log('delete item');
})
```

We add a click event for the whole `body`, then we filter out everything except the `.delete-item` clicks.

```js
document.body.addEventListener('click', function(e) {
  if (e.target.className = 'delete-item') {
    console.log(e.target);
    console.log('delete item');
  }
})
```

Unfortunately, because of the `<i>` tag it's firing the event on the `<i>` tag rather than on the `<a>` tag, so we check if the `<i>` tag was clicked, then grab the parent to access the `<a>` associated with the click.

```js
document.body.addEventListener('click', function(e) {
  if (e.target.parentElement.className === 'delete-item') {
    console.log(e.target.parent);
    console.log('delete item');
  }
})
```

Great, everything works!

But, if we wanted to add more classes to the `<a>` tag, then we would have to update the class string in this code every time.

There is an easy way to have the code just look for the `delete-item` class and therefore ignore the rest of the classes on that element.

This is great because we can add as many classes as we want, as long as `delete-item` exists in the class.

```js
document.body.addEventListener('click', function(e) {
  if (e.target.parentElement.classList.contains('delete-item') {
    console.log(e.target.parent);
    console.log('delete item');
  }
})
```

As you can see, we use the `classList` property to return the classes of the `<a>` element as an array rather than one string. We use the `contains()` method to look for `delete-item`.

## Local & Session Storage

The `window` object has the `localStorage` and `sessionStorage` API, to store data in the browser.

With **local storage**, you have to manually clear the data out of your browser settings to delete the data.

**Session storage** is cleared once the session ends (browser closes).

Local and session storage use the same methods and properties, so knowing one means you know the other one.

### Methods & Properties

Data has to be stored as a string, we can do this using `JSON.stringify`

```js
localStorage.setItem('name', 'John');
localStorage.setItem('age', '30');

localStorage.getItem('age'); // '30'
localStorage.getItem('name'); // 'John'

localStorage.clear();

localStorage.getItem('age'); // null
localStorage.getItem('name'); // null
```

With the following HTML, let's save inputted data

```html
  <form action="index.php">
    <input id="text" type="text"></input>
    <input id="btn-submit" type="submit"></input>
  </form>
```

```js
document.querySelector('form').addEventListener('submit', function(e) {
  const text = document.getElementById('text').value;
  localStorage.setItem('item', text);

  e.preventDefault();
});
```

This is great, but if we try to add a new item to local storage then we will override the data that is already in there, so we can instead use an array to store the data:

```js
document.querySelector('form').addEventListener('submit', function(e) {
  const item = document.getElementById('text').value;

  let items;

  // first time adding item, create the array
  if (localStorage.getItem('items') === undefined) {
    items = [];
  } else {
    items = JSON.parse(localStorage.getItem('items'));
  }

  items.push(item);
  localStorage.setItem('item', JSON.stringify(text) );
  
  e.preventDefault();
});
```

Brilliant! Data isn't overwritten anymore!
