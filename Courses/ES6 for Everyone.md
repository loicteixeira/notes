---
url: https://es6.io/
---

# ES6 for Everyone

## Variables scope

`var` is *function scoped*. `let` and `const` are *block scoped*.

`var`, `let` and `const` defined in a script will leak to the global scope (`window` in a browser) and might overwrite other variables. Prior to ES6, [Immediately-Invoked Function Expression (IIFE)])(http://benalman.com/news/2010/11/immediately-invoked-function-expression/) where used to prevent that but with ES6, `let` and `const` can simply be wrapped into a block.

```js
// Prevent leak to global scope with ES5
(function() {
    var foo = 'bar';
})();

// Prevent leak to global scope with ES6
{
    let foo = 'bar';
}
```

Because JavaScript is late binding, when defining a variable in a `for` loop with `var`, the value passed to asynchronous events will the value of the variable at the last iteration of the loop, while with `let` it will have the value of the corresponding iteration of the loop (because `var` is *function scoped* while `let` is *block scoped*.)

```js
for(var i = 0; i < 2; i++){
    console.log('Direct #' + i);
    setTimeout(function() {console.log('Timeout #' + i);}, 1000);
}
// -> Direct #0
// -> Direct #1
// -> Timeout #1
// -> Timeout #1

for(let i = 0; i < 2; i++){
    console.log('Direct #' + i);
    setTimeout(function() {console.log('Timeout #' + i);}, 1000);
}
// -> Direct #0
// -> Direct #1
// -> Timeout #0
// -> Timeout #1
```

Lastly, when using `var`, the variable is defined but *not* set at the top of the scope, this is known as the *Temporal Dead Zone*. This isn't the case with `let` and `const` which definition doesn't bubble at the top of the scope, but instead happens where it is defined in the code.

```js
// Will output `bar` as expected
var foo = 'bar';
console.log(foo);

// Will not raised undefined but output `undefined` instead
console.log(foo);
var foo = 'bar';

// Will raise ReferenceError
console.log(foo);
const foo = 'bar';
```

It is worth noting that `const` is not about immutability. It creates an immutable binding but it does not indicate that the value is immutable.

## Functions

### Default arguments

If the passed value is `undefined` (either because the argument is missing or because it was explicitely passed as `undefined`), it will use the provided default.

```javascript
function calculateBill(total, tax = 0.13, tip = 0.15) {
    return total + (total * tax) + (total * tip)
}

calculateBill(100) // total = 100, tax = 0.13, tip = 0.15
calculateBill(100, 0.2, 0.2) // total = 100, tax = 0.2, tip = 0.2
calculateBill(100, undefined, 0.2) // total = 100, tax = 0.13, tip = 0.2
```

Unlike in Python, default arguments do not need to be last.

### Arrow Functions

Written with a fat arrow `=>`, parenthesis can be omitted if there is only 1 argument or left empty if there are none.

```javascript
const noArgsFunc = () => { ... }
const oneArgsFunc = arg1 => { ... } // Same as `const oneArgsFunc = (args1) => { ... }`
const multipleArgsFunc = (arg1, arg2) => { ... }
```

Arrow functions have *implicit returns*, but only when not using curly brackets (i.e. as a one liner).

```javascript
const explicitReturn = (name) => {
    return `Hello ${name}!`
}
const implicitReturn = (name) => `Hello ${name}!`
```

This as the side effect that it is not possible to return an object literal directly, it will need to be wrapped in between parenthesis.

```javascript
(winner, i) => {name: winner, position: i} // Will raise SyntaxError
(winner, i) => ({name: winner, position: i}) // Works fine
```

Arrow functions do not (re)bind the value of `this`. In other words, the arrow function, will inherit the value of `this` from the parent scope. Therefore, arrow functions aren't a straight up replacement for regular functions and both function types have their uses.

```javascript
const box = document.querySelector('.box')

// Here, `this` will always refer to the value of `box` because
// the first callback (re)binds `this` the caller of the event listener (i.e. the box)
// while the second doesn't, keeping the value from the parent scope
box.addEventListener('click', function() {
    console.log(this)
    setTimeout(() => {
        console.log(this)
    }, 500)
})

// Here, `this` will always refer to the `window` because
// the first callback doesn't (re)binds `this`, keeping the value from the parent scope
// while the second (re)binds `this` the caller of the event listener (i.e. the window)
box.addEventListener('click', () => {
    console.log(this) // `this` will be the window because it hasn't been rebound
    setTimeout(function() {
        console.log(this)
    }, 500)
})

// FWIW, before arrow functions,
// it was needed to create a closure to keep the "correct" value of `this`
box.addEventListener('click', function() {
    var that = this;
    console.log(this);
    setTimeout(function() {
        console.log(that); // Cannot use `this` here
    }, 500);
});
```

More example of when regular functions should be used over arrow functions:

```javascript
// When you need a method to bind to an object
const person = {
    points: 23,
    score: function() {
        this.points++;
    }
}

// When you need to add a prototype method
class Car {
    constructor(make, colour) {
        this.make = make;
        this.colour = colour;
    }
}
const beemer = new Car('bmw', 'blue');
const subie = new Car('Subaru', 'white');

Car.prototype.summarize = function() {
    return `This car is a ${this.make} in the colour ${this.colour}`;
};

// When you need arguments object (for the function to accept n arguments)
// as the arguments object isn't set for arrow functions
const orderChildren = function() {
    const children = Array.from(arguments);
    return children.map((child, i) => {
        return `${child} was child #${i + 1}`;
    })
    console.log(arguments);
}
```

They are always anonymous functions so they won't show up in stack traces, even when assigned to a variable (is this second part still true?).