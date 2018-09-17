<img src="images/cassify-header-logo.png" alt="Cassify logo" width="300">

# Useful JavaScript Info

<!-- TOC depthFrom:2 depthTo:2 orderedList:false updateOnSave:true withLinks:true -->

- [The DOM](#the-dom)
- [Looping over `Array`, `Object`, `NodeList` and `HTMLCollection`](#looping-over-array-object-nodelist-and-htmlcollection)
- [Converting a `NodeList` or an `HTMLCollection` to an `Array`](#converting-a-nodelist-or-an-htmlcollection-to-an-array)
- [Copying an `Array`](#copying-an-array)
- [Page lifecycle: DOMContentLoaded, load, beforeunload, unload](#page-lifecycle-domcontentloaded-load-beforeunload-unload)

<!-- /TOC -->

## The DOM

### Selecting Multiple DOM Elements/Nodes

#### Option 1

```JavaScript
document.getElementsByClassName('abc');
document.getElementsByTagName('ul');
document.children;
```

1.  Using these methods will select any matching _elements_ only and will return them in an `HTMLCollection`.
1.  An `HTMLCollection` in the HTML DOM is live; it is automatically updated when the underlying document is changed.

#### Option 2

```JavaScript
document.querySelectorAll('.abc');
document.body.childNodes;
```

1.  Using these methods will return a `NodeList` representing a list of the document's elements that match the specified group of selectors. This could include any node type (i.e. element, comment, text, etc.) not just element nodes.
1.  In some cases, the `NodeList` is a live collection, which means that changes in the DOM are reflected in the collection. For example, `Node.childNodes` is live.
1.  In other cases, the `NodeList` is a static collection, meaning any subsequent change in the DOM does not affect the content of the collection. `document.querySelectorAll()` returns a static `NodeList`.

## Looping over `Array`, `Object`, `NodeList` and `HTMLCollection`

_Note: See the **Selecting Multiple DOM Elements/Nodes** section about how a `NodeList` and an `HTMLCollection` can be a **live** collection or a **static** collection._

### Arrays

- `for` loop
- `while` loop
- `forEach()` method - _`break` and `continue` won't work with this method. Use `return` like you would use `continue` in a `for` loop. Also the `for` loop is generally faster._
- `for...in` statement - _this is solely meant for objects but will also work for arrays. However, be careful as this statement will iterate over any properties you may have assigned to the array as well as the values of the array, which could lead to unexpected results._
- `for...of` statement - _this is an ES6 addition._

### Objects

- `for...in` statement

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

If you only need to copy an array, you can use the `Array.from()` method we talked about yesterday.

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

It works, but I don’t like it for two reasons:

1.  It’s less explicit than using something like `Array.slice()`or `Array.from()`. Both were made specifically to copy or create arrays, and the latter in particular tells you exactly what it’s doing in the name.
2.  `Array.slice()` has exceptional backwards compatibility, and `Array.from()` is polyfillable.

### Browser Compatibility

- The `Array.slice()` method works in all modern browsers, and IE6 and up.

- The `Array.from()` method works in all modern browsers, too, but has no IE support (only Edge). Can be polyfilled.

- The spread syntax only works in the latest browsers and can’t be polyfilled.

## Page lifecycle: DOMContentLoaded, load, beforeunload, unload

You can find some useful information about the lifecycle of an HTML page at [JavaScript.info][onload].

[onload]: https://javascript.info/onload-ondomcontentloaded 'Page lifecycle: DOMContentLoaded, load, beforeunload, unload'
