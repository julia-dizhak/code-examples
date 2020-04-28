 [<< return back](https://github.com/julia-dizhak/code-examples)

### Operator typeof
```
 typeof(typeof(value))
```
<details>
  <summary>What will return this line of code?</summary>

  `typeof(typeof(value))` is always "string".

  We know `typeof(value)` always gives us one of the predetermined strings: "undefined", "boolean", "number", and so on.
  So typeof any of them is "string". Because they’re strings!
</details>


### Operator '+'. What will be in console?
```
[] + {}
[] + []
{} + []
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

   > {} + []
     0
  </pre>

  Objects are converted to either string (if the other operand is a string) or number (otherwise). If you want to concatenate   arrays, you need to use a method Array.prototype.concat(), for example.
  There is no built-in way in JS to 'concatenate' (merge) objects -lodash
</details>


### What will be the output of the following code?
```
var output = (function(x) {
  delete x;
  return x;
})(0);

console.log(output);
```
<details>
  <summary>Explanation</summary>

  Above code will output 0 as output.
  delete operator is used to delete a property from an object.
  Here x is not an object it’s local variable.
  delete operator doesn’t affect local variable.
</details>
