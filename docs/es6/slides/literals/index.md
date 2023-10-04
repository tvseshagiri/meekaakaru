

#### Template literals.

- __Template literals__ is a new feature in ES6 to make working with strings and string templates easier.
- Multiline strings without hacks.
- String formatting - the ability to substitute parts of the string for values contained in variables. 
- Tagged templates - string tagging for safe HTML escaping, localisation and more.

Basic syntax:

```js []
let message = `Hello world!`;

console.log(message); // "Hello world!" 
console.log(typeof message); // "string"
```

---

#### Multiline strings (1/3).

In ES5, when using double or single quotes, strings must be completely contained on a single line. There are workarounds
for this shortcoming.

Workarounds with  `join` and `\n`.

```js []
var message = "Multiline \
string";

console.log(message); // "Multiline string"

var message1 = [
"Multiline ",
"string"
].join("\n");

let message3 = "Multiline \n" +
"string";
```

---

#### Multiline strings (2/3).

In ES6, template literals make multiline strings easy.

```js []
let message = `Multiline
string`;

console.log(message); // "Multiline
// string"
```

All whitespaces inside the backticks are parts of the string, so be careful with indentation.

```js []
let message = `Multiline
string`;

console.log(message); // "Multiline
// string"
```

---

#### Multiline strings (3/3).



Another Example:

```js []
let html = `
<div>
  <h1>Title</h1>
</div>`;
```

---

#### String substitution (1/3).

- Substitutions allow any valid JavaScript expression inside a template literal and output the result as part
of the string.
- Substitutions are delimited by an opening `${` and a closing `}` that can have any JavaScript expression inside.

```js []
var term = "John";
const url = `https://itunes.apple.com/search?term=${term}&media=music&limit=20`;
console.log(url);
// => https://itunes.apple.com/search?term=John&media=music&limit=20

var a = 10;
var b = 10;
console.log(`The number of JS MVC frameworks is
${2 * (a + b)} and not ${10 * (a + b)}.`);
// => The number of JS frameworks is 40 and not 200.
```

---

#### String substitution (2/3).

The `${}` works fine with any kind of expression, including member expressions, function and method calls.

```js []
function fn() {
return "I am a result. Rarr";
}

console.log(`foo ${fn()} bar`);

// => foo I am a result. Rarr bar.
```

```js []
var user = {
name: 'Max Mustermann'
};

console.log(`Thanks for helping us, ${user.name.toUpperCase()}.`);

// => "Thanks for helping us, MAX MUSTERMANN";
```

---

#### String substitution (3/3).

Advanced example of building HTML structures.

```js []
var li = (obj) => `<li><a href="${obj.url}">${obj.label}</a></li>`;
var ul = (arr) => `<ul>${arr.map((obj) => li(obj)).join('\n')}</ul>`;
var arr = [
{url: "http://www.twitter.com", label: "Twitter"},
{url: "http://www.linkedin.com", label: "Linked In"},
{url: "http://www.facebook.com", label: "Facebook"}
];

document.getElementById('list').innerHTML = ul(arr);
```

This will generate the following output:

```js []
<ul>
  <li><a href="http://www.twitter.com">Twitter</a></li>
  <li><a href="http://www.linkedin.com">Linked In</a></li>
  <li><a href="http://www.facebook.com">Facebook</a></li>
</ul>
```

---