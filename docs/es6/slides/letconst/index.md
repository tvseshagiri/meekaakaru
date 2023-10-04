
#### ES6 Variable types

- ES6 introduced three new variable types: __let, const, and var.__

`let` variables are block-scoped, meaning that they can only be accessed within the block in which they are declared.

``` js []

{
  let name = "John";
  console.log(name); // "John"
}

console.log(name); // ReferenceError: name is not defined

```

---

#### Const

- `const` variables are also block-scoped, but they are also immutable, meaning that their values cannot be changed.

```js []
const age = 25;

// Trying to reassign the value of age will result in a TypeError.
age = 26; // TypeError: Assignment to constant variable.
```

---

#### Var

- `var` variables are function-scoped, meaning that they can be accessed anywhere within the function in which they are declared, even within nested blocks.

```js []
function myFunction() {
  var name = "John";

  {
    console.log(name); // "John"
  }

  console.log(name); // "John"
}

myFunction();

```

---


#### Benefits of using `let` and `const`

- `let` and `const` variables offer several benefits over `var` variables:

  - They are more block-scoped, which can help to prevent variable collisions.
  - They are more concise and readable.
  - They can help to prevent errors, such as typos and reassignment of immutable variables.

---


#### When to use `let`, `const`, and `var`

  - Use `let` to declare a variable that you need to reassign within a block.
  - Use `const` to declare a variable that you do not need to reassign within a block.
  - Use `var` to declare a variable that you need to access from outside of a function.

