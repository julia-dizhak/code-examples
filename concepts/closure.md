 [<< return back](https://github.com/julia-dizhak/code-examples)

### Array with callback function
```
    var funcs = [];
    // create a bunch of functions
    for (var i = 0; i < 10; i++) {
        funcs.push(function() {
            console.log(i)
        })
    }

    //  call them
    for (var j = 0; j < 3; j++) {
        funcs[j]();
    }
 ```
<details>
    <summary>
        What will be value for i?
        Could you edit a code and have i as 0, 1, 2?
    </summary>
    The array funcs has a push callback function.
    funcs[j]() will call this function to print the i in the console.
    function() { console.log(i) } is an expression which evaluates to a value that is function that logs i.
    funcs.push is a function that adds a value to an array.
    Putting () after a function will call that function.
    In this case closure would be created and i always would be last iteration in array, so i=10.
    You can use let, that's why each iteration new variable i would be created.

    <pre>
        ...
        for (let i = 0; i < 10; i++) {
            funcs.push(function() {
                console.log('i', i)
            })
        }
        ...
    </pre>
</details>


### What you will see in console? Could you change code and display i equals to 0 1 2 ... 10 every sec in console ?
```
for (var i = 0; i < 10; i++) {
    setTimeout(function() {
        console.log('i', i)
    }, i*1000)
}
```
<details>
    <summary>Explanation</summary>
    After running fist sample in console will be displayed `i 10` and then every next 1 sec will be appear `i 10`.
    Because setTimeout is async function and it goes to stack event and run after timeout which is 1 sec.
    setTimeout will invoke after loop already finish and i will be equal to 10.

    To be able to display i from 0 1 2 ... 9 in console, you can use let in for loop.

    You can use IIFE (will be closure inside) as well:
<pre>
for (var i = 0; i < 10; i++) {
    (function(i) {
        setTimeout(function() {
            console.log('i', i)
        }, i*1000)
    })(i)
}
</pre>

    Or second variant:
<pre>
for (var i = 0; i < 10; i++) {
    setTimeout((function(i) {
        return function() {
            console.log('i', i)
    }
    })(i), i*1000)
}
</pre>
    You can use .bind() as well
<pre>
for (var i = 0; i < 10; i++) {
  setTimeout((function(i) {
    console.log('i', i)
  }).bind(null, i) , i*1000)
}
</pre>
</details>


### What will be in console?
```
for (var i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log('i', i)
  }, 1000)
}
```
<details>
    <summary>Explanation</summary>
    In console will appear be i 10 after 1 sec
</details>
