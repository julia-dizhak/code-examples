 [<< return back](https://github.com/julia-dizhak/code-examples)

### How did array transfer after .map() method?
```
  const arr = [2,2,2,2].map(parseInt)
```

<details>
  <summary>Correct answer</summary>
  It is common to use the callback with one argument.
  The parseInt() function parses a string argument and takes 2 arguments and returns an integer of the specified radix (the base in mathematical numeral systems).
  ```parseInt(x, base)```

  The map() method creates a new array populated with the results of calling a provided function on every element in calling array. Array.prototype.map passes 3 arguments: element and index, the array.

   <pre>
    [2,2,2,2].map(parseInt) ->

    [2,2,2,2].map((item, index) => {
        parseInt(item, index)
      })
    }

    parseInt(2, 0) - 10th numeral system => equal 2
    parseInt(2, 1) - 1th numeral system => equal NaN
    parseInt(2, 2) - 2th numeral system => equal NaN
    parseInt(2, 3) - 3th numeral system => equal 2

    Answer is [2, NaN, NaN, 2]
   </pre>
</details>

### Why arr2 is equal to undefined?
```
  const arr1 = [1, 3, 5, 7, 9];
  const arr2 = arr1.forEach(number => ++number);
  console.log(arr2); // = undefined
```

<details>
  <summary>Correct answer</summary>
  Because method .forEach() returns undefined
</details>


### Give a value for num1, num2 to have result1 and result2 as true?
```
  const arr1 = [1,3,5,7];
  const arr2 = [2,4,6,8];

  const result1 = arr1.every(currentValue=> currentValue % num1 == 1);
  const result2 = arr2.every(currentValue=> currentValue % num2 == 0);
```

<details>
  <summary>Correct answer</summary>
  Method every return boolean, the answer is num1 (odd) = num2 (even) = 2
</details>
