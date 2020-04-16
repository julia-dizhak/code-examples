 [<< return back](https://github.com/julia-dizhak/code-examples)

### Could you write bind realisation?

```
    function fn(a, b, c) {
        console.log(a, b, c, this)
    }

    function bound(?) { ... }

    let magicFn = bound(fn, {});
    magicFn(2,3,4) // -> should return 2,3,4 and {}
 ```
<details>
    <summary>
        Explanation: Let's assume that's call and apply already exists.
    </summary>
    The solution below will not cover specifir to browser realisation
    but it covers main concept.

    ```
    function bound(callBack, context) {
        return function() {
            callBack.apply(context, arguments)
        }
    }
    ```
</details>
