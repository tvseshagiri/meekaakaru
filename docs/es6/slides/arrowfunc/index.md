

## Arrow Functions

---

#### Arrow functions. Syntax (1/4)

  - Arrow functions are anonymous functions that use an "arrow" __=>__. 
  - The syntax for arrow functions comes in many variations.
  - All variations begin with _function arguments_, followed by the _arrow_, followed by the _body_ of the function. 
  - __Single argument__ can be used directly without any parentheses.
  - The expression to the right of the arrow is evaluated and returned.



---

#### Arrow functions. Syntax (1/4)

  ```js [] []
  // ES6
  [1, 2, 3].map(num => num * 2);

 // ES5 equivalent
  [1, 2, 3].map(function(num) {return num * 2;});
  ```
  No `return` keyword is required with a single statement.

---

#### Arrow functions. Syntax (2/4).

 - Must include parentheses around the arguments if there are more than one argument.

  ```js []
  //ES6
  var sum = (num1, num2) => num1 + num2;

  //ES5 equivalent
  var sum = function(num1, num2) {
  return num1 + num2;
  };
  ```

 - No arguments (the same syntax as for many arguments).

  ```js []
  var doNothing = () => {};
  ```

---

#### Arrow functions. Syntax (3/4).

  - if function has more statements and not just an expression to
  return,
  you have to use brackets.

  ```js []
  //ES6
  [1, 2, 3, 4].map(num => {
  var multiplier = 2 + num;
  return num * multiplier;
  });
  
  //ES5 equivalent
  [1, 2, 3, 4].map(function(num) {
  var multiplier = 2 + num;
  return num * multiplier;
  });
  ```

---

#### Arrow functions. Syntax (4/4).

  There is a special case - an arrow function that wants to return an object literal `{...}`. In this case,
  the function body must wrap the literal in parentheses.

  ```js []
  //ES6
  var getSomeObject = id => ({key: id, value: "unknown"});

  //ES5 equivalent
  var getSomeObject = function(id) {
  return {
     key: id,
     value: "unknown"
    };
  };
  ```

---

#### Arrow functions. IIFEs.

  Immediately-invoked function expressions (IIFEs) allow you to define an anonymous function and call it immediately
  without saving a reference.

  ```js []
  let person = function(message) {
  return {
        getGreeting: function() {
        return message;
      }
   };
  }("Hell World!");

//Using arrow Functions

  let person = ((message) => {
  return {
     getGreeting: function() {
      return message;
    }
  };
  })("Hell World!");
  ```


