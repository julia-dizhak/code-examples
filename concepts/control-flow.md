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

### What will be value for secondVar after next code execution?
```
    var firstVar = 'foo';
    var secondVar;

    switch(firstVar) {
        case 'foo':
            secondVar = 'bar';

        case 'bar':
            secondVar = 'foo';

        case 'foobar':
            secondVar = 'barfoo';
            break;

        default:
            secondVar = 'foobar';
        }
```

<details>
  <summary>Correct answer</summary>
  secondVar equal to 'barfoo', because there is no operator break
</details>
