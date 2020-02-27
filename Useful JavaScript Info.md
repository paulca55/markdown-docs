# Useful JavaScript Info

- [The DOM](#the-dom)
  - [Selecting Multiple DOM Elements/Nodes](#selecting-multiple-dom-elementsnodes)
- [Looping over `Array`, `Object`, `NodeList` and `HTMLCollection`](#looping-over-array-object-nodelist-and-htmlcollection)
  - [Arrays](#arrays)
  - [Objects](#objects)
  - [NodeLists](#nodelists)
  - [HTMLCollections](#htmlcollections)
- [Converting a `NodeList` or an `HTMLCollection` to an `Array`](#converting-a-nodelist-or-an-htmlcollection-to-an-array)
  - [Method 1 (for supporting IE8 and below)](#method-1-for-supporting-ie8-and-below)
  - [Method 2 (for supporting IE9 and above)](#method-2-for-supporting-ie9-and-above)
  - [Method 3](#method-3)
- [Copying an `Array`](#copying-an-array)
  - [The old school way](#the-old-school-way)
  - [The fancy new ES6 way](#the-fancy-new-es6-way)
  - [Browser Compatibility](#browser-compatibility)
- [Page lifecycle: DOMContentLoaded, load, beforeunload, unload](#page-lifecycle-domcontentloaded-load-beforeunload-unload)
- [Correct type-checking in JavaScript](#correct-type-checking-in-javascript)
  - [Type-checking numbers](#type-checking-numbers)
  - [Type-checking strings](#type-checking-strings)
  - [Type-checking booleans](#type-checking-booleans)
  - [Type-checking objects](#type-checking-objects)
  - [Type-checking arrays](#type-checking-arrays)

## The DOM

### Selecting Multiple DOM Elements/Nodes

#### Option 1

```JavaScript
document.getElementsByClassName('abc');
document.getElementsByTagName('ul');
document.children;
```

1.  Using these methods will select any matching _elements_ only and will return them in an `HTMLCollection`.
2.  An `HTMLCollection` in the HTML DOM is live; it is automatically updated when the underlying document is changed.

#### Option 2

```JavaScript
document.getElementsByName('up');
document.querySelectorAll('.abc');
document.body.childNodes;
```

1.  Using these methods will return a `NodeList` representing a list of the document's elements that match the specified group of selectors. This could include any node type (i.e. element, comment, text, etc.) not just element nodes.
1.  In some cases, the `NodeList` is a live collection, which means that changes in the DOM are reflected in the collection. For example, `Node.childNodes` is live.
1.  In other cases, the `NodeList` is a static collection, meaning any subsequent change in the DOM does not affect the content of the collection. `document.querySelectorAll()` returns a static `NodeList`.

## Looping over `Array`, `Object`, `NodeList` and `HTMLCollection`

_Note: See the **Selecting Multiple DOM Elements/Nodes** section about how a `NodeList` and a `HTMLCollection` can be a **live** collection or a **static** collection._

### Arrays

- `for` loop
- `while` loop
- `forEach()` method - _`break` and `continue` won't work with this method. Use `return` like you would use `continue` in a `for` loop. Also the `for` loop is generally faster._
- `for...in` statement - _this is solely meant for objects but will also work for arrays. However, be careful as this statement will iterate over any properties you may have assigned to the array as well as the values of the array, which could lead to unexpected results._
- `for...of` statement - _this is an ES6 addition._

### Objects

- `for...in` statement - _this enumerates properties in the protoype chain too._
- `Object.keys` method
- `Object.entries` method
- `Object.values` method

### NodeLists

- `for` loop
- `while` loop
- `Array.prototype.slice.call()` approach - _this will convert the `Nodelist` into a new array._
- `forEach()` method - _this is not widely supported on a `NodeList`._
- `for...of` statement - _this is an ES6 addition._

_Note: You can convert the `NodeList` to an Array and be able to use the methods/properties on the `Array.prototype`. See the section on array conversions._

### HTMLCollections

- `for` loop
- `while` loop
- `for...of` statement - _this is an ES6 addition._

_Note: You can convert the `HTMLCollection` to an Array and be able to use the methods/properties on the `Array.prototype`. See the section on array conversions._

## Converting a `NodeList` or an `HTMLCollection` to an `Array`

### Method 1 (for supporting IE8 and below)

If you need IE8 and below support, the easiest way of converting a NodeList to an Array is pushing each element from a NodeList into a new Array:

```JavaScript
var myNodeList = document.querySelectorAll('li');
var myArrayFromNodeList = [];
for (var i = 0; i < myNodeList.length; i++) {
  myArrayFromNodeList.push(myNodeList[i]);
}
```

### Method 2 (for supporting IE9 and above)

If you’re fortunate enough to not care about IE8 and below, then you can use a neat trick to convert your NodeList instantly using `Array.prototype.slice.call()`:

Accessing the Prototype Object here, we grab the `slice()` method, and pass our NodeList into it. This API then internally converts it to an Array using the `slice()` method (which returns a new Array). It cleverly pushes each Node into a new Array, yay!

Now we can access all the Array methods and use the `forEach()` method as intended:

```JavaScript
var elems = document.querySelectorAll('div');
var divs = Array.prototype.slice.call(elems);
divs.forEach(function () {
  //...
});
```

### Method 3

The new ECMAScript 6 Harmony standard introduces the `Array.from` method which makes Array-like Objects (such as the NodeList) and other iterable Objects (such as an `Object` or `String`) to Array conversion a breeze.

```JavaScript
var divs = document.querySelectorAll('div');
var arr = Array.from(divs); // Array of <div>s
```

## Copying an `Array`

### The old school way

The `Array.slice()` method creates a new array from an existing one.

It accepts two optional arguments. The first is the index of the item in the array to start copying from, and the second is the index to end on. If you omit the start index, it will start at the beginning. If you omit the end index, it will go to the end.

The original array is not be modified.

```JavaScript
var sandwiches = ['turkey', 'tuna', 'chicken salad', 'italian', 'blt', 'grilled cheese'];

// ['chicken salad', 'italian', 'blt', 'grilled cheese']
var fewerSandwiches = sandwiches.slice(2);

// ['chicken salad', 'italian', 'blt']
var fewerSandwiches2 = sandwiches.slice(2, 4);
You can start at the end and work backward by passing in a negative integer as the start index.

// ['italian', 'blt', 'grilled cheese']
var sandwichesFromTheEnd = sandwiches.slice(-3);
```

To create a brand new copy of an array in its entirety, you can use `Array.slice()` with no arguments.

```JavaScript
var sandwichesCopy = sandwiches.slice();
```

### The fancy new ES6 way

#### Array.from()

If you only need to copy an array, you can use the `Array.from()` method.

```JavaScript
var sandwiches = ['turkey', 'tuna', 'chicken salad', 'italian', 'blt', 'grilled cheese'];

// ['turkey', 'tuna', 'chicken salad', 'italian', 'blt', 'grilled cheese']
var sandwichesCopy = Array.from(sandwiches);
```

The `Array.from()` method also lets you optionally pass in a modifier function you can use to transform the items in the array.

Create a callback function, and pass in a variable for the individual items in the original array. In your callback, return a modified value for the new array.

For example, let’s say I wanted every sandwich to be in uppercase. I could do this.

```JavaScript
// (6) ['TURKEY', 'TUNA', 'CHICKEN SALAD', 'ITALIAN', 'BLT', 'GRILLED CHEESE']
var sandwichesUppercase = Array.from(sandwiches, function (sandwich) {
	return sandwich.toUpperCase();
});
```

#### Spread Syntax (...)

You could use **spread syntax** to copy an array like this:

```JavaScript
var sandwiches = ['turkey', 'tuna', 'chicken salad', 'italian', 'blt', 'grilled cheese'];
var newSandwiches = [...sandwiches];
```

Keep something in mind:

1. It’s less explicit than using something like `Array.slice()`or `Array.from()`. Both were made specifically to copy or create arrays, and the latter in particular tells you exactly what it’s doing in the name.
2. `Array.slice()` has exceptional backwards compatibility, and `Array.from()` is polyfillable.

### Browser Compatibility

- The `Array.slice()` method works in all modern browsers, and IE6 and up.

- The `Array.from()` method works in all modern browsers, too, but has no IE support (only Edge). Can be polyfilled.

- The spread syntax only works in the latest browsers and can’t be polyfilled.

## Page lifecycle: DOMContentLoaded, load, beforeunload, unload

You can find some useful information about the lifecycle of an HTML page at [JavaScript.info][onload].

[onload]: https://javascript.info/onload-ondomcontentloaded 'Page lifecycle: DOMContentLoaded, load, beforeunload, unload'

## Correct type-checking in JavaScript

### Type-checking numbers

#### Method 1

It is safe to use the `typeof` operator for numbers.

```js
var num = 99.66;

console.log(typeof num); // number

if (typeof num === 'number') {
  console.log("Yes it's a number!"); // Yes it's a number!
}
```

#### Method 2

You can also use the `Object.prototype` method but this is overkill for numbers.

```js
var num = 99.66;

console.log(Object.prototype.toString.call(num)); // [object Number]

if (Object.prototype.toString.call(num) === '[object Number]') {
  console.log("Yes it's a number!"); // Yes it's a number!
}
```

By adding the `slice` method this can be simplified.

```js
var num = 99.66;

console.log(
  Object.prototype.toString
    .call(num)
    .slice(8, -1)
    .toLowerCase()
); // number

if (
  Object.prototype.toString
    .call(num)
    .slice(8, -1)
    .toLowerCase() === 'number'
) {
  console.log("Yes it's a number!"); // Yes it's a number!
}
```

### Type-checking strings

#### Method 1

It is safe to use the `typeof` operator for strings.

```js
var str = 'dog';

console.log(typeof str); // string

if (typeof str === 'string') {
  console.log("Yes it's a string!"); // Yes it's a string!
}
```

#### Method 2

You can also use the `Object.prototype` method but this is overkill for strings.

```js
var str = 'dog';

console.log(Object.prototype.toString.call(str)); // [object String]

if (Object.prototype.toString.call(str) === '[object String]') {
  console.log("Yes it's a string!"); // Yes it's a string!
}
```

By adding the `slice` method this can be simplified.

```js
var str = 'dog';

console.log(
  Object.prototype.toString
    .call(str)
    .slice(8, -1)
    .toLowerCase()
); // string

if (
  Object.prototype.toString
    .call(str)
    .slice(8, -1)
    .toLowerCase() === 'string'
) {
  console.log("Yes it's a string!"); // Yes it's a string!
}
```

### Type-checking booleans

#### Method 1

It is safe to use the `typeof` operator for booleans.

```js
var bool = true;

console.log(typeof bool); // boolean

if (typeof bool === 'boolean') {
  console.log("Yes it's a boolean!"); // Yes it's a boolean!
}
```

#### Method 2

You can also use the `Object.prototype` method but this is overkill for booleans.

```js
var bool = true;

console.log(Object.prototype.toString.call(bool)); // [object Boolean]

if (Object.prototype.toString.call(bool) === '[object Boolean]') {
  console.log("Yes it's a boolean!"); // Yes it's a boolean!
}
```

By adding the `slice` method this can be simplified.

```js
var bool = true;

console.log(
  Object.prototype.toString
    .call(bool)
    .slice(8, -1)
    .toLowerCase()
); // boolean

if (
  Object.prototype.toString
    .call(bool)
    .slice(8, -1)
    .toLowerCase() === 'boolean'
) {
  console.log("Yes it's a boolean!"); // Yes it's a boolean!
}
```

### Type-checking objects

#### Method 1

It is **not safe** to use the `typeof` operator for objects. This is because `typeof` can report back a type of `object` when this isn't always the case.

```js
var obj = {
  type: 'fizzy',
  flavour: 'cola',
  price: 0.8,
};

console.log(typeof obj); // object
console.log(typeof []); // object
console.log(typeof null); // object
```

#### Method 2

A bulletproof way you can check the type is `object` is by using the `Object.prototype` method.

```js
var obj = {
  type: 'fizzy',
  flavour: 'cola',
  price: 0.8,
};

console.log(Object.prototype.toString.call(obj)); // [object Object]

if (Object.prototype.toString.call(obj) === '[object Object]') {
  console.log("Yes it's a object!"); // Yes it's a object!
}
```

By adding the `slice` method this can be simplified.

```js
var obj = {
  type: 'fizzy',
  flavour: 'cola',
  price: 0.8,
};

console.log(
  Object.prototype.toString
    .call(obj)
    .slice(8, -1)
    .toLowerCase()
); // object

if (
  Object.prototype.toString
    .call(obj)
    .slice(8, -1)
    .toLowerCase() === 'object'
) {
  console.log("Yes it's a object!"); // Yes it's a object!
}
```

### Type-checking arrays

#### Method 1

It is **not safe** to use the `typeof` operator for arrays. This is because `typeof` will report back a type of `object` for arrays.

```js
var arr = [1, 2, 3, 4];

console.log(typeof arr); // object
```

#### Method 2

It is safe to use the `instanceOf` operator for arrays, and is a quick way to check, but still isn't the best way to type check an array as we now have `Array.isArray()`, see other methods below.

```js
var arr = [1, 2, 3, 4];

console.log(arr instanceof Array); // true

if (arr instanceof Array === true) {
  console.log("Yes it's a array!"); // Yes it's a array!
}
```

#### Method 3

There is a new method (check for browser compatibility) called `Array.isArray()`, which is a really good method for type checking arrays.

```js
var arr = [1, 2, 3, 4];

console.log(Array.isArray(arr)); // true

if (Array.isArray(arr) === true) {
  console.log("Yes it's a array!"); // Yes it's a array!
}
```

#### Method 4

A bulletproof way you can check the type is `object` is by using the `Object.prototype` method.

```js
var arr = [1, 2, 3, 4];

console.log(Object.prototype.toString.call(arr)); // [object Array]

if (Object.prototype.toString.call(arr) === '[object Array]') {
  console.log("Yes it's a array!"); // Yes it's a array!
}
```

By adding the `slice` method this can be simplified.

```js
var arr = [1, 2, 3, 4];

console.log(
  Object.prototype.toString
    .call(arr)
    .slice(8, -1)
    .toLowerCase()
); // array

if (
  Object.prototype.toString
    .call(arr)
    .slice(8, -1)
    .toLowerCase() === 'array'
) {
  console.log("Yes it's a array!"); // Yes it's a array!
}
```
