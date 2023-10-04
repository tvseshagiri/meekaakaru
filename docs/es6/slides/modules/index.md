  
#### What are modules?
    
- ES6 introduced built-in modules. 
- Defined in its own file.
- functions or variables defined in a module are not visible outside explicitly export them. 
- To export certain variables from a module use the keyword `export`.
- Similarly, to consume the exported variables in a different module you use `import`.
- Modules are singletons. imported multiple times, only a single "instance" of it exists.

---

#### Exporting declarations.
    
 `export` in front of any variable, function or class  export it from the module.
    
```js []
// export data
export let color = "red";

// export function
export function sum(num1, num2) {
  return num1 + num1;
}

// export class
export class Rectangle {
  constructor(length, width) {
    ...
  }
}
```

---


#### Exporting statements and renaming.
    
Declare a variable, function or class and export it later.
    
```js []
// define a function and then export it later
function multiply(num1, num2) {
  return num1 * num2;
}

export { multiply };    
```
    
Can use the `as` keyword to specify a new name for importing.
    
```js []
class ZipCodeValidator extends StringValidator {
    isAcceptable(value) {
        return value.length === 5 && numberRegexp.test(value);
    }
}

export { ZipCodeValidator as mainValidator }; 

```

---


#### Re-exporting.
    
There may be a time when you'd like to re-export something that your module has imported. Use cases:
- You're creating a library out of several small modules.
- Modules extend other modules, and partially expose some of their features.
    
```js []
// re-export sum from the module "./example.js"
export { sum } from "./example.js";
    
// sum is imported from "./example.js" and then exported as add
export { sum as add } from "./example.js";
    
// re-export everything from "./example.js"
export * from "./example.js";
```

__Note:__ If you'd like to export everything from another module, you can use the `*` pattern.

---

#### Importing single, multiple bindings or all.
    
Once you have a module with exports, you can access the functionality in another module by using the `import` keyword.
    
```js []
// import just one or multiple bindings
import { sum } from "./example.js";
import { multiply, magicNumber } from "./example.js";

console.log(sum(1, magicNumber));
console.log(multiply(1, 2));
```
Import the entire module as a single object.
    
```js []
// import everything
import * as example from "./example.js";

console.log(example.sum(1, example.magicNumber));
console.log(example.multiply(1, 2));
```

---

#### Renaming imports.
    
If the module importing a variable, function or class wants to use a different name, it can use `as`.
    
Example:
    
```js []
// import the add() function and renames it to sum()
import { add as sum } from "./example.js";
    
console.log(typeof add);   // "undefined"
console.log(sum(1, 2));    // 3
```
    
__Note:__ There is no identifier named `add` in this module.

---


#### Exporting and importing default values.
    
- The default value for a module is a single variable, function or class as specified by the `default` keyword,
- only set one default export per module. Examples:
    
```js []
export default function(num1, num2) {
    return num1 + num2;
}
```

```js []
function sum(num1, num2) {return num1 + num2;}

export default sum;
```
    
- For importing __no curly braces__ are used.
- It is also possible to import non default and default things in one `import` statement.

---

#### Examples

```js []
import sum from "./example.js";
```
    
```js []
import sum, { add } from "./example.js";
``` 

---

#### Resolving paths for importing.
    
A module can import things from other modules. 
    
- Relative paths (`'../model/user'`) relatively to the location of the importing module. The file extension can usually be omitted.
- Absolute paths (`'/lib/js/helpers'`) which point directly to the file of the module to be imported.
- Names (`'util'`). What modules names refer to has to be configured. A typically configuration in JavaScript projects refers to the `node_modules` directory as root.

---

#### All supported syntax at a glance.
    
```js []
// import a module without any import bindings
import 'jquery';
// import the default export of a module
import $ from 'jquery';
// import a named export of a module
import { $ } from 'jquery';
// import a named export to a different name
import { $ as jQuery } from 'jquery';
// import an entire module instance object
import * as crypto from 'crypto';
    
// export a named function
export function foo() {};
// export the default export as a function
export default function foo() {};
// export an existing variable
export { encrypt };
// export a variable as a new name
export { decrypt as dec };
// export an export from another module
export { encrypt as en } from 'crypto';
// export all exports from another module
export * from 'crypto';
```

---

#### Loading modules in browsers.
    
To support modules, the __module__ value was added as a `type` option of the `script` element.
Setting type to __module__ tells the browser to load any inline code or code contained in the file
specified by `src` as a module.
    
```js []
<!-- load a module JavaScript file -->
<script type="module" src="module.js"></script>
    
<!-- include a module inline -->
<script type="module">
import { sum } from "./example.js";

let result = sum(1, 2);
</script>
```

---