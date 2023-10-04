
#### What is destructuring?
    
- Destructuring is a convenient way to extract values from data stored in Objects and Arrays (also nested).
 This is an opposite operation to structuring (constructing data).*

```js []
var obj = {first: 'Jane', last: 'Leo'};
```

Destructuring in ECMAScript 6 enables the same syntax for extracting data. Just as the object literal lets us create
multiple properties at the same time, the object pattern lets us extract multiple properties at the same time.
    
```js []
var {first: a, last: b} = obj;
// a = 'Jane', b = 'Leo'

var [x, y] = ['Jane', 'Leo'];
// x = 'Jane', y = 'Leo'
```

---

#### Object destructuring.

```js []
var foo = {bar: 'pony', baz: 3};
var {bar: a, baz: b} = foo;

console.log(a)
// 'pony'
console.log(b)
// 3
```
    
ES5 equivalent
    
```js []
var foo = {bar: 'pony', baz: 3};
var a = foo.bar;
var b = foo.baz;
```

---

#### Object destructuring, shorthand notation.
    
Only for object literals: If the value of a property is provided via a variable whose name is the same as the property name,
you can omit the property name.

```js []
var {x, y} = {x: 11, y: 8};
    
console.log(x)
// 11
console.log(y)
// 8  
```
    
This declaration is equivalent to:

```js []
var {x: x, y: y} = {x: 11, y: 8};
```

---

#### Object destructuring, nested properties.

You can also pull properties as deep as you want.
    
```js []
var foo = {bar: {deep: 'pony', smile: 'lol'}};
var {bar: {deep, smile: sure}} = foo;
    
console.log(deep);
// 'pony'
console.log(sure);
// 'lol'
```

ES5 equivalent
    
```js []
var foo = {bar: {deep: 'pony', smile: 'lol'}};
var deep = foo.bar.deep;
var sure = foo.bar.smile;
```

---

#### Array destructuring.
    
Destructuring works for arrays as well. How? By using square brackets in the destructuring side of the declaration.
    
```js []
var [a, b, c] = [1, 2, 3];

console.log("A is " + a + ", B is " + b + ", C is " + c);
// A is 1, B is 2, C is 3
```

The `rest` operator lets you extract the remaining elements of an array into an array.
You can only use this operator as the last part inside an array.
    
```js []
var [x, ...y] = ['a', 'b', 'c'];
// x = 'a', y = ['b', 'c']
``` 

Attention: The same syntax (...) is used by the `spread` operator!

---

#### Pick what you need.
    
If you destructure an object, you mention only those properties that you are interested in.
    
```js []    
var {x} = {x: 7, y: 3, z: 10};
// x = 7
```

If you destructure an array, you can choose to only extract a prefix.
    
```js [] 
var [x, y] = ['a', 'b', 'c'];
// x = 'a', y = 'b';
```
    
You can also conveniently skip over elements that you don’t care about.

```js []
var [, , a, b] = [1, 2, 3, 4, 5];
// a = 3, b = 4;
    
function f() {return [1, 2, 3];}

var [a, , b] = f();
// a = 1, b = 3;
```

---

#### Mix objects and arrays.
    
We can also mix objects and arrays together and use theirs literals.

```js []
var mixed = {
  one: 1, two: 2, values: [3, 4, 5]
};

var {one: a, two: b, values: [c, , e]} = mixed;

console.log(a, b, c, e);
// 1 2 3 5
```
    
The same with return value of a function:
    
```js []
function mixed () {
  return {
    one: 1, two: 2, values: [3, 4, 5]
  };
}

var {one: a, two: b, values: [c, , e]} = mixed();
```

---

#### If a part has no match (1/3).
    
If the value of a destructuring assignment isn't match, it evaluates to `undefined`.
Just like when accessing not defined properties on an object with the dot or bracket notation.
    
```js []
var [x, y] = [];
    
console.log(x);  // undefined
console.log(y);  // undefined    
    
var point = {
  x: 1
};

var {x: a, y: b} = point;
    
console.log(a);  // 1
console.log(b);  // undefined
```

---

#### If a part has no match (2/3).
    
Example of deep objects:
    
```js []
var {
  prop1: x,
  prop2: {
    prop3: {
      nested: [ , , y]
    }
  }
} = {prop: "Hello", prop2: {prop3: {nested: ["a", "b", "c"]}}};
```

--
    
__Question__: What are the values of variables `x` and `y`?
    
--
    
```js []
console.log(typeof x);  // undefined
console.log(y);         // 'c'
```

---

#### If a part has no match (3/3).
    
If you're trying to access a deeply nested property of a parent that doesn't exist, then you'll get an exception.
    
```js []
var {foo: {bar}} = {baz: 'something'};
    
// Exception: TypeError
```
    
It makes sense if you rewrite destructuring in ES5:

```js []
var temp = {baz: 'something'};
var bar = temp.foo.bar;
    
// Exception: TypeError
```

---

#### Default values (1/3).
    
If a part (an object property or an array element) has no match in the source, it is matched against:
    
- its *default value* (if specified)
- *undefined* (otherwise)
    
Providing a default value is optional. Example with array:
    
```js []
var [x = 3, y] = [];
// x = 3; y = undefined
```
__Explanation__: The element at index 0 has no match on the right-hand side. Therefore, destructuring continues
`y` matching `x` against 3, which leads to `x` being set to 3.
    
Example with object:

```js []
var {foo: x = 3, bar: y} = {};
// x = 3; y = undefined
```

---

#### Default values (2/3).

`undefined` triggers default values. Default values are also used if a part does have a match and that match is `undefined`.
    
```js []
var {prop: y = 2} = {prop: undefined};
// y = 2
```    

Default values are computed when they are needed (on demand). This

```js []
var {prop: y = someFunc()} = someValue;
```

is equivalent to
    
```js []
var y;
if (someValue.prop === undefined) {
    y = someFunc();
} else {
    y = someValue.prop;
}
```

---

#### Default values (3/3).

So far we have only seen default values for variables, but you can also associate them with object itself:
    
```js []
var [{prop: x} = {}] = [];
```
    
What does this mean? The element at index 0 has no match, which is why destructuring continues with:
    
```js []
var {prop: x} = {};
// x = undefined
```
    
Another example with complex default values:
    
```js []
var [{prop: x} = {prop: 123}] = [];
// Destructuring continues as follows:
var {prop: x} = {prop: 123};
// x = 123
```

---

#### Destructuring in a function's parameter list.

You can also use destructuring in a function's parameter list.
    
```js []
function greet({name: greeting = 'she', age}) {
  console.log(`${greeting} is ${age} years old.`)
}
    
greet({name: 'nico', age: 27});
// nico is 27 years old
    
greet({age: 24});
// she is 24 years old
```
 
Next advanced example:
    
```js []
var ajax = function({url = 'sbb.ch', port: p = 80}, ...data) {
  console.log("Url:", url, "Port:", p, "Rest:", data);
};
    
ajax({url: "localhost"}, "more", "data", "hello");
// => Url: localhost Port: 80 Rest: ['more', 'data', 'hello']
```

---

#### Destructuring with computed property names.

Computed property names are another object literal feature that also works for destructuring.
You can specify the name of a property via an expression, if you put it in square brackets.
    
```js []
var KEY = 'z';
var {[KEY]: foo} = {z: 'bar'};

console.log(foo);
// 'bar'
```

[Reference to computed property names](http://droidscript.org/javascript/Operators/Object_initializer.html)


---

#### Good to know.
    
If we try to omit `var`, `let` or `const`, it will throw an error, because block code can't be a destructuring assignment.
    
```js []
let point = {
  x: 1
};

{x: a} = point; // throws error
```   
  
__Solution:__ We have to wrap it in parentheses.
    
```js []
let point = {
  x: 1
};

({x: a} = point);

console.log(a);
// 1
```
    
---
    
