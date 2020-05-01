 [<< return back](https://github.com/julia-dizhak/code-examples)

### There is an array [1, 2, 3, 4, 5]. Does calculated sum is correct?
```
    const arr = [1, 2, 3, 4, 5]
    var i = 0;
    var sum = 0;
    while (i++ < arr.length - 1) {
        sum += arr[i]
    }
```

<details>
  <summary>Correct answer</summary>
  No. By using while loop result will be equal to 14.
  Because during first iteration i = 1 and value for first element arr[0]
  will be absent.
  The correct sum is 15.
</details>
