# Learning to code by JavaScript
I use this repo to track examples of tricky JS code, which will help me to imrove my knowledges.
See examples of code and answers or explanation below.
Code examples divided by topics.

## Table of Contents

- [Primitive types](#primitive-types)
- [References types](#references-types)
- [Variables](#variables)
- [Operators](#operators)
- [Functions](#functions)
- [Arrow functions](#arrow-functions)
- [Pass-by-references vs pass-by-value)(#pass-by-references-vs-pass-by-value)
- [Loops](#loops)
- [Array methods](#array-methods)
- [Closure](#closure)
- [.bind, .call, .apply](#bind-call-apply)
- [Class](#class)

## Primitive types

Primitives types are
- undefined,
- Boolean,
- Number,
- String,
- Symbol,
- BigInt and
- special primitive type null

[see code examples >>](https://github.com/julia-dizhak/code-examples/blob/master/concepts/primitive-types.md)

## References types

References types tare
- Objects
- and Functions

Examples related to
- Object.create()
- Object.assign()

[see code examples >>](https://github.com/julia-dizhak/code-examples/blob/master/concepts/references-types.md)


## Variables

### Does immutability of strings play a role here, and what role does it play? What will be in console?
```
 let pet = 'Narwhal';
 pet = 'The Kraken';
 console.log(pet); // ?
```

<details>
  <summary>Explanation</summary>
   The answer is "The Kraken" — immutability of strings doesn’t play a role.
   Variables are not values.
   Variables point to values.
</details>


### Nouns and verbs: read next code
```
 function double(x) {
  x = x * 2;
 }

 let money = 10;
 double(money);
 console.log(money); // ?
```

<details>
  <summary>Explanation</summary>
  If we thought double(money) was passing a variable, we could expect that x = x * 2 would double that variable.
  But that’s not how it works. We know that double(money) means “figure out the value of money, and then pass that value to double”.
 So the answer is 10.
</details>

### Assignment
```
 null = 10
 console.log(null)
```

<details>
  <summary>Explanation</summary>

  This code produce an error `Uncaught SyntaxError: Invalid left-hand side in assignment`.
  It is error because the left side of assignment must always be 'wire'.
  Variables are wires, so they can appear on the left side.

  A literal like `null` is not a 'wire',
  so trying to assign something to it is meaningless.
</details>


### What will be value of y?
```
 let x = 10;
 let y = x;
 x = 0;
```
<details>
  <summary>Explanation</summary>
  Declare a variable called x. Make a wire for the x variable. Assign to x the value of 10. Point x’s wire to the value 10.


  Declare a variable called y. Make a wire for the y variable. Assign to y the value of x.

  Evaluate the expression: x. The x expression resulted in the value 10. Therefore, assign to y the value of 10. Point y’s wire to the value 10.

  Assign to x the value of 0. Point x’s wire to the value 0.

 `At the end, the x variable points to the value 0, and the y variable points to the value 10.`
</details>


## Operators

- operator typeof
- operator concatenation
- operator delete


[see code examples >>](https://github.com/julia-dizhak/code-examples/blob/master/concepts/operators.md)

## Functions

- Functions parameters and scope, localness of variables
- Function declaration vs function expression
- Arrow functions

[see code examples >>](https://github.com/julia-dizhak/code-examples/blob/master/concepts/functions.md)


## Pass-by-references vs pass-by-value
- Pass--by-references
- Pass-by-value

[see code examples >>](https://github.com/julia-dizhak/code-examples/blob/master/concepts/pass-by-references-by-value.md)

## Loops

- for loop
- do while
- while

[see code examples >>](https://github.com/julia-dizhak/code-examples/blob/master/concepts/loop.md)


## Array methods

- Array.prototype.map()

```
  const arr = [1, 4, 9, 16];
  const map1 = arr.map(x => x * 2);
  console.log(map1);  // expected output: Array [2, 8, 18, 32]
```

- Array.prototype.forEach()

[see code examples >>](https://github.com/julia-dizhak/code-examples/blob/master/concepts/array-methods.md)


## Closure

A closure is an inner function that has access to the outer (enclosing) function’s variables - scope chain.

- defining a closure
- setTimeout and closure

[see code examples >>](https://github.com/julia-dizhak/code-examples/blob/master/concepts/closure.md)

 ## .bind, .call, .apply

 ### Read next code

```
const obj1= {
  num: 1
}
const obj2 = {
  num: 2
}

let addToThis = function(a,b,c) {
  const sum = this.num + a + b + c;
  console.log('sum', sum);
  return sum;
}

addToThis.call(obj1, 1, 2, 3) // -> sum is 7
addToThis.apply(obj2, [1,2,3]) // -> sum is 8

let bound1 = addToThis.bind(obj1);
let bound2 = addToThis.bind(obj2);
bound1(1,2,3) // -> sum is 7
bound2(1,2,3) // -> sum is 8
```

[see code examples >>](https://github.com/julia-dizhak/code-examples/blob/master/concepts/bind.md)


## Class

### Defining a Class

ES5 syntax

```
// constructor
// just create this as an empty {} and return this behind a scene
function Building(floors) {
  this.what = 'building'
  this.floors = floors;

  // this.countFloors =  ...
  // it's not a good practice tot create method in constructor
  // because the same function creates for each object
}

// prototype is just an object
Building.prototype.countFloors = function() {
  if (this.floors >= 10) {
    console.log('I have', this.floors, 'floors')
  }
}

const myHouse = new Building(2);
myHouse.countFloors(); // -> condition is false

const officeBuilding = new Building(12);
officeBuilding.countFloors(); // -> I have 12 floors

const whateverHouse = {}
whateverHouse.countFloors() // -> whateverHouse.countFloors is not a function
// you can not call this method, because it doesn't exist
// you can run only countFloors for instance created from Building
```


ECMAScript 2015 (ES6) syntax
```
  class Building {
    constructor(floors) {
      this.what = 'building';
      this.floors = floors
    }

    countFloors() {
      if (this.floors >= 2) {
        console.log('I have', this.floors, 'floors')
      }
    }
}

const myFlat = new Building(2);
myFlat.countFloors(); // I have 2 floors
```

[see code examples >>](https://github.com/julia-dizhak/code-examples/blob/master/concepts/class.md)
