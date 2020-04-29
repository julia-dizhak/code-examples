 [<< return back](https://github.com/julia-dizhak/code-examples)

### What will be the output of a?
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

### What will be the output of the following code?
```
let some = {a: 7};

function someFunc(obj) {
 obj.a = 10;
}

someFunc(some);
console.log(some.a);
```

<details>
  <summary>Correct answer</summary>
  Because for objects the value of the variable is a reference, answer will be 10
</details>
