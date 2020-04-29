 [<< return back](https://github.com/julia-dizhak/code-examples)

### What will be the output of the comparison?
```
var a = "42";
var b = 42;

a == b -> ?
a === b -> ?
```

<details>
  <summary>Correct answer</summary>
  <pre>
    a == b -> true
    a === b -> false
  </pre>
</details>


### Comparison with and without coercion
```
0 == false -> ?
0 === false -> ?
```

<details>
  <summary>Explanation</summary>
  false is compared with Number type, false is equal to 0, than 0 == 0 is equal to true.
  In second case, comparison without coercion, 0 and false have different types.
  <pre>
    0 == false -> true
    0 === false -> false
  </pre>
</details>


### Comparison references types
```
let cat = {name: 'Bob'}
let evil = {name: 'Bob'}

cat == evil -> ?
cat === evil -> ?

let member = cat;
member == cat -> ?
member === cat -> ?

```

<details>
  <summary>During comparison what will be Boolean values?</summary>
  Because we compare objects and it is a reference type, cat and evil don't have the same references
  <pre>
    cat == evil -> false
    cat === evil -> false
  </pre>
  But member == cat (member === cat ) is equal true, because `let member = cat`
</details>


### What will be the output of the result?
```
let cars1 = ["Mercedes", "Volkswagen", "Ford"];
let cars2 = ["Mercedes", "Volkswagen", "Ford"];

let result = (cars1 === cars2) +" "+ (cars1 == cars2);
console.log(result);
```

<details>
  <summary>Correct answer</summary>
  When we compare 2 arrays (which is reference type) we compare not value but references.

  When we check `cars1 === cars2` without coercion, they have same type, but different references -> false.

  When we check `cars1 == cars2` with coercion, types are the same, but
  references are different -> false.

  Output is 'false false'
</details>
