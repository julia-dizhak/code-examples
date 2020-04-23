 [<< return back](https://github.com/julia-dizhak/code-examples)

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

### There is an array [1, 2, 3, 4, 5]. Does calculated sum is correct?
```
    const arr = [1, 2, 3, 4, 5]
    var i = 0;
    var result = 0;
    while (i++ < arr.length - 1) {
        result += arr[i]
    }
```

<details>
  <summary>Correct answer</summary>
  No. By using while loop result will be equal to 14.
  Because during first iteration i = 1 and value for first element arr[0]
  will be absent.
  The correct sum is 15.
</details>
