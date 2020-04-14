 [<< return back](https://github.com/julia-dizhak/code-examples/edit/master/README.md)

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
                console.log(i)
            })
        }
        ...
    </pre>
</details>
