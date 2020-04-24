 [<< return back](https://github.com/julia-dizhak/code-examples)

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


### What will be displayed in modal window after resolving f()?
```
    var value = 0;

    function f() {
        if (1) {
            value = true
        } else {
            var value = false
        }

        alert(value)
    }

    f();
```
<details>
  <summary>Correct Answer</summary>
  Because 1 ist true, first condition is correct.
  In alert we will see true
</details>
