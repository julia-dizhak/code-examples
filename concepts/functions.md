 [<< return back](https://github.com/julia-dizhak/code-examples)

### Functions parameters and scope. Localness of variables.
```
    var x = 'outside'

    var f1 = function() {
        var x = 'inside';
        console.log('x inside f1 ->', x) ?
    }
    f1();
    console.log('x after f1 ->', x) ?

    var f2 = function() {
        x = 'inside f2'
    }
    f2();
    console.log('x after f2->', x) ?
 ```
<details>
    <summary>What will be value of x in each console?</summary>
    Because of localness for variables inside functions,
    the first console display 'inside',
    second - x is global variable - 'outside',
    and after running f2 x is equal to 'inside f2'.
</details>



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


### Arrow functions
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
  <summary>What happens after running obj.test3(), obj.test4()?</summary>

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

