# Learning to code by JavaScript
I use this repo to track examples of tricky JS code, which will help me to imrove my knowledges.
See examples of code and answers or explanation below.
Code examples divided by topics.

## Operator typeof

### What will return next line of code?
```
 typeof(typeof(value))
```
<details>
  <summary>Correct Answer</summary>

  `typeof(typeof(value))` is always "string".

  We know `typeof(value)` always gives us one of the predetermined strings: "undefined", "boolean", "number", and so on.
  So typeof any of them is "string". Because they’re strings!
</details>


########################################################
## Primitive types

### What are the values of `a` and `b` after it runs?
```
 let a = 10; // declare a variable called a -> set it to 10
 let b = a; // declare a variable called b -> set it to a; a is 10; so b is 10 too
 a = 0 // set the a variable to 0
```
<details>
  <summary>Correct Answer</summary>
  a is 0 now, and b is 10.
</details>


### What do you expect it to do?
```
let reaction = 'yikes';
reaction[0] = 'l';
console.log(reaction);
```
<details>
  <summary>Correct Answer</summary>
  This code will either print "yikes" or throw an error depending on whether you are in strict mode.
  It will never print "likes" -> yikes.
</details>


### What will console display?
```
let answer = true
answer.opposite = false
console.log(answer.opposite())
```
<details>
  <summary>Correct Answer</summary>
  Booleans are primitive. And primitive values are immutable. We can’t change them — and setting a property on a value is a change.

 If our code runs in the strict mode, assigning a property on a primitive value would lead to an error. Otherwise, it will silently do nothing. In either case, we can’t set a property on a boolean value like true.
</details>


###################################################################
## References types [(code examples)](https://github.com/julia-dizhak/code-examples/blob/master/concepts/references-types.md)
```
  References types are Objects and Functions
  Object.create()
  Object.assign()
```


###################################################################
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

### Assignament
```
 null = 10
 console.log(null)
```

<details>
  <summary>Explanation</summary>

  This code produce an error `Uncaught SyntaxError: Invalid left-hand side in assignment`.
  It is error because the left side of assignament must always be 'wire'.
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




###################################################################
## Operator '+' (concatenation)

### What will be in console?
```
[] + {}
[] + []
```
<details>
  <summary>Explanation</summary>
  You can only add numbers and strings, all other values will be converted to either one of those types.
  The plus operator performs three kinds of conversion: It converts values to primitives, numbers and strings.

  <pre>
   > [] + [] -> ''
    [].toString() -> ''

   > [] + {}
     '[object Object]'
     String({}) -> '[object Object]'
  </pre>

  Objects are converted to either string (if the other operand is a string) or number (otherwise). If you want to concatenate   arrays, you need to use a method Array.prototype.concat(), for example.
  There is no built-in way in JS to 'concatenate' (merge) objects -lodash
</details>


###################################################################
## Function declaration vs function expression

### What happens? What you will see in console?
```
 test1();
 test2();

 function test1() {
   console.log('test1');
 }

 var test2 = function() {
   console.log('test2');
 }
```
<details>
  <summary>Correct answer</summary>

   first case, test1() - function declaration. JS interpreter moves function declaration to the top of their containing scope
 (hoisting). That's why you can use function declaration before you declare it.
  <pre>
    in console -> test1
  </pre>

   in the second case, test2 declared as function expression. The variable name will be hoisted, but you can't access until JS
   execution encounters its definition. You can't use before define them -> function doesn't exist
   <pre>
     var - test2 is not a function
     const/let - cannot access 'test2' before initialization
   </pre>
</details>


###################################################################
## Arrow functions

### What happens after running obj.test3(), obj.test4() ?
```
  const  obj = {};

  const test3 = () => {
    console.log(this);
  }

  function test4() {
    console.log(this);
  }

  obj.test3 = test3;
  obj.test4 = test4;

  obj.test3() // ?
  obj.test4() //  ?
```
<details>
  <summary>Correct answer</summary>

   Unlike regular functions, arrows functions do not have their own `this` (does not bind its own this).
   The value of `this` inside arrow functions is not dependent on how they are invoked.
   It depends only on its `enclosing context` (literal scope).
  <pre>
    in console // -> Window {parent: Window, ...}
  </pre>
  But if test3 will be define as obj method, then `this` will be `obj` itself.
  <pre>
   const obj = {
     test3: () => {
      console.log(this);
     }
   }
   // -> obj {test3: ƒ}
  </pre>

   In the second case, `test4()` is function declaration. Regular function defines its own this or context depending on their invocation, in our case, `this = object itself`.

   <pre>
     -> // {test3: ƒ, test4: ƒ}
   </pre>
</details>


###################################################################
## By references vs by value

### What will be value a?
```
 let a = {};

 (function b(a) {
   a.a = 10;
   a = null;
 })(a);
 console.log('a', a);
```

<details>
  <summary>Correct answer</summary>
  Function argument is local variable.
  When we overwrite a local variable for IIFE or function expression, it doesn't reflect on an outer scope.

   <pre>
    let a = {};

    (function b(a) {
      a.a = 10; // -> {a: 10} because a is object - reference type
      a = null; // overwrite a local variable
      console.log('a', a); // local a is null, but not the outside
    })(a);
    console.log('a', a); -> {a: 10}
   </pre>

   Example with function expression
   <pre>
     var a = 5;
     function b(a) {
      a = 9;
      console.log('a local', a) -> 9
    }
    b(a);
    console.log('a outer', a) -> 5
   </pre>

</details>


###################################################################
## Loop

### You need to update for loop and get brr as equal to [1,2,3]
```
 let arr = [1, 2, 42, 3];
 let brr = [];

 for (let i = 0; i < arr.length; i++) {
  if (arr[i] === 42) {}
  brr.push(arr[i]);
}
```

<details>
  <summary>Correct answer</summary>
  Can check operator `continue` or left one cycle iteration.

   <pre>
    for (let i = 0; i < arr.length; i++) {
     // if (arr[i] === 42) continue;
     if (arr[i] === 42) i++;

     brr.push(arr[i]);
    }
   </pre>
</details>


###################################################################
## Array methods [(code examples)](https://github.com/julia-dizhak/code-examples/blob/master/concepts/array-methods.md)

### Array.prototype.map()

```
  const arr = [1, 4, 9, 16];
  const map1 = arr.map(x => x * 2);
  console.log(map1);  // expected output: Array [2, 8, 18, 32]
```

### Array.prototype.forEach()
```
const arr = ['a', 'b', 'c'];

arr.forEach(element => console.log(element));

// expected output: "a"
// expected output: "b"
// expected output: "c"
```


 ## Closure [(see code examples)](https://github.com/julia-dizhak/code-examples/blob/master/concepts/closure.md)



 ## .bind, .call, .apply [(code examples)](https://github.com/julia-dizhak/code-examples/blob/master/concepts/bind.md)

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

## Class [(code examples)](https://github.com/julia-dizhak/code-examples/blob/master/concepts/class.md)

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
