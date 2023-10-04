  
#### Default parameters (1/3).

In ECMAScript 5 and earlier, there is the following pattern to create a function with default parameters values:

```js []
function makeRequest(url, timeout, callback) {
timeout = timeout || 2000;
callback = callback || function() {};
...
}
```
- both `timeout` and `callback` are optional parameters that get default values if they are not provided.
- The OR operator `||` always returns the second operand when the first is falsy. 

---

#### Default parameters (2/3).

```js []
function makeRequest(url, timeout, callback) {
timeout = (typeof timeout !== "undefined") ?
timeout : 2000;
callback = (typeof callback !== "undefined") ?
callback : function() {};

...
}
```

This approach still requires a lot of extra code for a very basic operation. ECMAScript 6 makes it easier!

```js []
function makeRequest (
url, timeout = 2000, callback = function() {}) {

...
}
```

This function only expects the first parameter to always be passed. The other parameters have default values.

---

#### Default parameters (3/3).

Examples how the function can be called:

```js []
// uses default timeout and callback
makeRequest("/foo");

// uses default callback
makeRequest("/foo", 500);

// doesn't use defaults
makeRequest("/foo", 500, function(body) {...});
```

In the case of default parameter values, a value of `null` is considered to be valid.

```js []
// uses default timeout (undefined = missing parameter)
makeRequest("/foo", undefined, function(body) {...});

// doesn't use default timeout
makeRequest("/foo", null, function(body) {...});
```

---

#### Default parameters and arguments.

`arguments` object remains detached from the named parameters.

```js []
function doSomething(first, second = "b") {
console.log(arguments.length);
console.log(first === arguments[0]);
console.log(second === arguments[1]);
first = "c";
second = "d";
console.log(first === arguments[0]);
console.log(second === arguments[1]);
}

doSomething("a");
```

The outputs:

```js []
1 // length is 1 because only one argument was passed
true // first is equal to arguments[0]
false // because arguments[1] is undefined
false // changing first has no effect on arguments
false // changing second has no effect on arguments
```

---

#### Default parameters expressions.

The default value need not be a simple value. It can be any valid expression,
even a function to retrieve the default parameter value.

```js []
function getValue() {
return 5;
}

function add(first, second = getValue()) {
return first + second;
}

console.log(add(1, 1)); // 2
console.log(add(1)); // 6
```

__Important__: The default value expressions are lazily evaluated, meaning they're only run when they're needed
(when a parameter's argument is omitted or is `undefined`).

---

#### Default parameters with cross-usage.

You can use a previous parameter as the default for a later parameter.

```js []
function add(first, second = first) {
return first + second;
}

console.log(add(1, 1)); // 2
console.log(add(1)); // 2
```

```js []
function getValue(value) {
return value + 5;
}

function add(first, second = getValue(first)) {
return first + second;
}

console.log(add(1, 1)); // 2
console.log(add(1)); // 7
```

---

#### Default parameters and scopes.

The formal parameters in a function declaration are in their own scope.
A reference to an identifier in a default value expression first matches the formal parameters' scope
before looking to an outer scope. Example:

```js []
var w = 1, z = 2;

function foo(x = w + 1, y = x + 1, z = z + 1) {
console.log(x, y, z);
}

foo(); // ReferenceError
```

The `w` in the `w + 1` default value expression looks for `w` in the formal parameters' scope, but does not find it,
so the outer scope's `w` is used. Next, the `x` in the `x + 1` default value expression finds `x` in the formal
parameters' scope, and luckily `x` has already been initialized, so the assignment to `y` works fine.

However, the `z` in `z + 1` finds `z` as a not-yet-initialized-at-that-moment parameter variable,
so it never tries to find the `z` from the outer scope and throws a `ReferenceError`.

---

#### Spread operator (1/2).

ES6 introduces a new `...` operator that's typically referred to as the __spread__ or __rest__ operator,
depending on where/how it's used. When `...` is used in front of an *iterable* (Array, Set, Map, ...),
it acts to "spread" it out into its individual values.

__A typical usage__: Specify an array, split it into items which are passed in as separate arguments to a function.

```js []
function foo(x, y, z) {
console.log(x, y, z);
}

foo(...[1,2,3]); // 1 2 3
```

ES5 way:

```js []
foo.apply(null, [1,2,3]); // 1 2 3
```

That means, the spread operator acts as a simple syntactic replacement for the `apply()` method.

---

#### Spread operator (2/2).

The spread operator can be used to spread out a value in other contexts as well, such as inside another array
declaration:

```js []
var a = [2, 3, 4];
var b = [1, ...a, 5];

console.log(b); // [1, 2, 3, 4, 5]
```

Here, `...` is replacing `concat()`, as it behaves like `[1].concat(a, [5])`.

Another example for mixing the spread operator with other arguments:

```js []
let values = [-25, -50, -75, -100];
console.log(Math.max(...values, 0)); // 0
```

ES5 equivalent:

```js []
let values = [-25, -50, -75, -100];
console.log(Math.max.apply(Math, values.concat([0]))); // 0
```

---

#### Rest parameters (1/3).

The other common usage of `...` can be seen as the opposite - instead of spreading a value out, the `...` *gathers*
a set of values together into an array.

```js []
function foo(x, y, ...z) {
console.log(x, y, z);
}

foo(1, 2, 3, 4, 5); // 1 2 [3,4,5]
```

The `...z` in this snippet is saying: "gather the rest of the arguments (if any) into an array called `z`".

The `...z` is called __rest parameters__ because you're collecting the rest of the parameters.

The rest parameters can be used as a better alternative to `arguments` (`arguments` is not really an array, but an
array-like object).

Rest parameters were designed to replace `arguments` in ECMAScript.

---

#### Rest parameters (2/3).

ES5

```js []
function foo() {
// turn arguments into a real array and remove the first element
var args = Array.prototype.slice.call(arguments);

args.shift();

console.log.apply(console, args);
}
```

ES6 way (rest parameters and spread operator together)

```js []
function foo(...args) {
// args is already a real array, remove the first element
args.shift();

console.log(...args);
}
```

---

#### Rest parameters (3/3).

There are two __restrictions__ on rest parameters.

__1.__ There can be only one rest parameter, and the rest parameter must be last.

```js []
// Syntax error: Can't have a named parameter after rest parameters
function doSomething(foo, ...bars, last) {
...
}
```

__2.__ Rest parameters cannot be used in an object literal setter.

```js []
let object = {
// Syntax error: Can't use rest param in setter
set name(...value) {
// do something
}
};
```

Object literal setters are restricted to a single argument and rest parameters have, by definition,
an infinite number of arguments.

---
class: center, middle, inverse

#### That's all folks, thanks for your attention!

.back[[Back to the homepage](http://ova2.github.io/es6-presentations/)]

Slideshow created with [remark](https://github.com/gnab/remark)

</textarea>
<script>
  var slideshow = remark.create({
    highlightLanguage: 'javascript', highlightStyle: 'idea', navigation: { scroll: false }
  });
</script>
</body>

</html>