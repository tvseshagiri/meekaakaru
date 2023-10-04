
    
#### Class-like structures in ES 5.
    
```js []
function Car () {
  this.fuel = 0;
  this.distance = 0;
}

Car.prototype.move = function () {
  if (this.fuel < 1) {
    throw new RangeError('Fuel tank is depleted')
  }
  this.fuel--
  this.distance += 2
}

Car.prototype.addFuel = function () {
  if (this.fuel >= 60) {
    throw new RangeError('Fuel tank is full')
  }
  this.fuel++
}    
```
    
```js []
var car = new Car();
car.addFuel();
car.move();
```

---


#### Class declaration in ES6 (1/2).
    
- ES6 classes are syntactic sugar over the prototype-based OO pattern. 
- Classes support prototype-based inheritance, super calls, instance and static methods and constructors.
    
```js []
class Car {
  constructor () {
    this.fuel = 0
    this.distance = 0
  }
    
  move () {
    if (this.fuel < 1) {
      throw new RangeError('Fuel tank is depleted')
    }
    this.fuel--
    this.distance += 2
  }
    
  addFuel () {
    if (this.fuel >= 60) {
      throw new RangeError('Fuel tank is full')
    }
    this.fuel++
  }
}    
```

---


#### Class declaration in ES6 (2/2).
    
__Important notes:__

- Class declarations begin with the `class` keyword followed by the name of the class.
- Commas are invalid between methods in a class.
- Properties that occur on the instance rather than the prototype, can only be created inside a class constructor or method. In the example these are `fuel` and `distance`.
- All methods are non-enumerable. They don't show up when you do a `for...in` loop over the object or use `Object.keys()` to get an array of property names. But you can iterate over class methods by `Object.getOwnPropertyNames(MyClass.prototype)`.
- Calling the class constructor without `new` throws an error.
- Attempting to overwrite the class name within a class method throws an error.

---


#### Class expressions (1/3)

Classes and functions are similar in that they have two forms: declarations and expressions.
- Function and class __declarations__ begin with an appropriate keyword (`function` or `class`, respectively) followed by an identifier.
- Functions have an __expression form__ that doesn't require an identifier after `function`, and similarly, classes have an expression form
that doesn't require an identifier after `class`.
    
```js []
let PersonClass = class {
  constructor(name) {
    this.name = name;
  }

  sayName() {
    console.log(this.name);
  }
};

let person = new PersonClass("Nicholas");
person.sayName();   // outputs "Nicholas"    
```

---


#### Class expressions (2/3)

The previous example used an __anonymous class expression__. The `name` property of `PersonClass` (`PersonClass.name`) is an empty string.
When using a class declaration, `PersonClass.name` would be `"PersonClass"`.
    
A __named class expression__ includes an identifier after the `class` keyword.
    
```js []
let PersonClass = class PersonClass2 {
    constructor(name) {
      this.name = name;
    }
  
    sayName() {
      console.log(this.name);
    }
};

console.log(typeof PersonClass);   // "function"
console.log(typeof PersonClass2);  // "undefined"  
```

The `PersonClass2` identifier exists only within the class definition. It is defined for use only inside the class.
Outside the class, `typeof PersonClass2` is `undefined` because no `PersonClass2` binding exists there.
    
---


#### Class expressions (3/3)

Another interesting use of class expressions is creating singletons by immediately invoking the class constructor.
To do so, you must use `new` with a class expression and include parentheses at the end.
    
```js []
let person = new class {
  constructor(name) {
    this.name = name;
  }

  sayName() {
    console.log(this.name);
  }
}("Nicholas");

person.sayName();   // "Nicholas"
```
    
---


#### Inheritance (1/4).
    
Classes make inheritance easier to implement by using the familiar `extends` keyword.
    
```js []
class Warrior {
  constructor(name) {
    this.name = name;
    this.health = 100;
  }
    
  heal(amount) {
    this.health = Math.min(this.health + amount, 100);
  }
}

class Ninja extends Warrior {
  constructor(name) {
    super(name);
  }

  heal(amount) {
    super.heal(amount * 1.2);
  }
}
```
    
---


#### Inheritance (2/4).
    
Derived classes require you to use `super()` if you specify a constructor; if you don't, an error will occur.
If you choose not to use a constructor, then `super()` is automatically called for you with all arguments upon
creating a new instance of the class. For instance, the following two classes are identical:

```js []
class Square extends Rectangle {
  // no constructor
}

// Is equivalent to

class Square extends Rectangle {
  constructor(...args) {
    super(...args);
  }
}
```
    
__Important notes:__
    
- You can only use `super()` in a derived class. If you try to use it in a non-derived class (a class that doesn't use extends), it will throw an error.
- You must call `super()` before accessing `this` in the constructor. Attempting to access `this` before calling `super()` results in an error.

---


#### Inheritance (3/4).
    
The methods on derived classes always shadow methods of the same name on the base class.
    
```js []
class Square extends Rectangle {
  constructor(length) {
    super(length, length);
  }

  // override and shadow Rectangle.prototype.getArea()
  getArea() {
    return this.length * this.length;
  }
}
```
    
You can also call the base class version of the method by using the `super`. E.g.
    
```js []
class Square extends Rectangle {
  ...    
  // override, shadow, and call Rectangle.prototype.getArea()
  getArea() {
    return super.getArea();
  }
}
```
    
---


#### Inheritance (4/4).
    
In ES5 and earlier, it was not possible to inherit from built-ins like `Array`, `RegExp`, etc. It is possible in ES6.
    
```js []
class MyArray extends Array {
  // empty
}

var colors = new MyArray();
colors[0] = "red";
console.log(colors.length);   // 1
```

Any method that returns an instance of the built-in will automatically return a derived class instance instead.
So, if you have a derived class called `MyArray` that inherits from `Array`, methods such as `slice()` return an instance of `MyArray`.
    
```js []
let items = new MyArray(1, 2, 3, 4),
    subitems = items.slice(1, 3);

console.log(items instanceof MyArray);      // true
console.log(subitems instanceof MyArray);   // true
```
    
---


#### Accessors (1/2).
    
We have the ability to define getters and setters for our fields. This feature allows to access the fields as any other object property.
    
```js []
class Warrior {
  constructor(name) {
    this._name = name;
    this._health = 100;
  }

  get health() {
    return this._health;
  }
    
  set health(newHealth){
    this._health = newHealth;
  }
}

let donatello = new Warrior("Donatello");
    
console.log(donatello.health);   // 100
donatello.health = 80;
```

---


#### Accessors (2/2).
    
When we define a getter and no setter, the variable with the getter / setter name becomes read-only.
    
```js []
class Warrior {
  constructor(name) {
    this._name = name;
    this._health = 100;
  }

  get health() {
    return this._health;
  }
}

let donatello = new Warrior("Donatello");
    
console.log(donatello.health);   // 100
donatello.health = 80;   // TypeError: Cannot set property health...
```

---

#### Static methods (1/3).
    
Adding additional methods directly onto constructors to simulate static members is a common pattern in ES5 and earlier.
    
```js []
function PersonType(name) {
  this.name = name;
}

// static method
PersonType.create = function(name) {
  return new PersonType(name);
};

// instance method
PersonType.prototype.sayName = function() {
  console.log(this.name);
};

var person = PersonType.create("Nicholas"); 
```

---


#### Static methods (2/3).
    
ES6 classes simplify the creation of static members by using the `static` annotation before the method or accessor property name.
    
```js []
class PersonClass {
  constructor(name) {
    this.name = name;
  }
    
  sayName() {
    console.log(this.name);
  }
    
  static create(name) {
    return new PersonClass(name);
  }
}

let person = PersonClass.create("Nicholas");
```

---

#### Static methods (3/3).
    
One thing you can do in JavaScript but can't in Java: from the derived class you can override and call your parents static method.
    
```js []
class Foo {
  static classMethod() {
    return 'hello';
  }
}

class Bar extends Foo {
  static classMethod() {
    return super.classMethod() + ', too';
  }
}
    
Bar.classMethod();   // 'hello, too'
```

---

#### Static fields.
    
There are no static fields in ES6, but there is a discussion about it for ES7.
Right now you can simulate the functionality like this:
    
```js []
class Foo {
  constructor() {}
}

const staticNumber = 5;
const staticObj = {prop: 5};

Foo.staticNumber = staticNumber;
Foo.staticObj = staticObj;  
```

---

#### Abstract classes.
    
This concept is not implemented in ES6 or ES7, but we can simulate abstract classes.
We can use `new.target` in class constructors to determine the constructor the class is being instantiated with.
    
```js []
// abstract base class
class Shape {
  constructor() {
    if (new.target === Shape) {
      throw new Error("This class cannot be instantiated directly.")
    }
  }
}

class Rectangle extends Shape {
  constructor(length, width) {
    super();
    this.length = length;
    this.width = width;
  }
}

var x = new Shape();   // throws error because new.target is Shape
var y = new Rectangle(3, 4);   // no error, new.target is Rectangle
```

---

#### Abstract methods.
    
This concept is not implemented too, but we can mimic abstract methods.
    
```js []
class Abstract {
  constructor() {
    if (this.method === undefined) {
      throw new TypeError("Must override method");
    }
  }
}

class Derived1 extends Abstract {}

class Derived2 extends Abstract {
  method() {}
}

const a = new Abstract(); // this.method is undefined; error
const b = new Derived1(); // this.method is undefined; error
const c = new Derived2(); // this.method is
                          // Derived2.prototype.method; no error    
```

---

#### Private fields.
    
Private fields are not supported in any ES right now, but there are a couple of new structures in ES6 that let you emulate the private scope.
    
```js []
const private = new WeakMap();

class Warrior {    
  constructor(name) {
    this._name = name;
    
    private.set(this, {
        health: 100
    });    
  }

  get health(){
    return private.get(this).health;
  }
}  
```

__Warning__: The above `WeakMap` is shared among all Warrior instances, so potentially you can access another warrior's health.

---

#### Functions overloading.
    
This functionality have never existed in JavaScript and there is no plan on supporting it.
If you have e.g. three methods of the same name `say`
    
```js []
class Person {    
  say(what) { //string
    console.log(thing);
  }

  say(things) { //array
    things.forEach(function(thing){
        console.log(thing);
    });        
  }

  say() {
    console.log("blah")
  }
}    
```

the last `say()` method wins (overwrites all other).
    
JavaScript has no type checking on arguments or required quantity of arguments,
so you can just have one implementation of `say()`.

---

#### Interfaces.
    
There is no concept of interfaces in any version of JavaScript.
    
You can find interfaces in TypeScript.
    
