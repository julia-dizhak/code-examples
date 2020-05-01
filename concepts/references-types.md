 [<< return back](https://github.com/julia-dizhak/code-examples)

### Read next code
```
 function duplicateSpreadsheet(original) {
  if (original.hasPendingChanges) {
   throw new Error('you need to save the file before you can duplicate it')
  }

  let copy = {
    created: Date.now(),
    author: original.author,
    cells: original.cells,
    metadata: original.metadata,
  };

  copy.metadata.title = 'Copy of ' + original.metadata.title;

  return copy;
 }
```
Next function duplicates a spreadsheet.
It throws an error if the original spreadsheet isn't saved.
It prepends "Copy of" to the new spreadsheet's title.

<details>
  <summary>What did the function accidentally change as well ?</summary>
  This function also accidentally changes the title of original spreadsheet.
  <pre>
    const original = {
      created: '',
      author: 'Test',
      cells: '',
      metadata: {
        title: 'one test title'
      }
    }

    duplicateSpreadsheet(original)

    {
      created: 1585570108872
      author: "Test"
      cells: ""
      metadata: {title: "Copy of one test title"}
    }
 </pre>
</details>

### Mutability
```
  let object1 = {value: 10};
  let object2 = object1;
  let object3 = {value: 10};

  console.log(object1 == object2); // ?
  console.log(object1 == object3); // ?

  object1.value = 15;
  console.log(object2.value); // ?
  console.log(object3.value); // ?
```

<details>
  <summary>What will be the output of the following code?</summary>
  The object1 and object2 bindings grasp the same object, which is why changing object1 also changes the value of object2. They are said to have the same identity. The binding object3 points to a different object, which initially contains the same properties as object1 but lives a separate life.

  <pre>
    ...
    console.log(object1 == object2); // → true
    console.log(object1 == object3); // → false

    object1.value = 15;
    console.log(object2.value); // → 15
    console.log(object3.value); // → 10
  </pre>
</details>

### What will return obj.c?
```
const obj = {
 a: 1,
 b: 1
}
```
<details>
  <summary>Correct answer</summary>
  It will return undefined.
  Because of prototype inheritance.
  Is `c` own property on `obj`? No, check its prototype.
  Is there a 'c' own property on obj.[[Prototype]]? is null, stop searching
  no property found, return undefined.

  But chain could be obj.[[Prototype]].[[Prototype]]
  and so on obj.[[Prototype]].[[Prototype]].[[Prototype]]
</details>


### What will be displayed in console?
```
 let arr = [1,2]
 let brr = arr;
 brr = [42, 43];
 console.log(arr[0]);
```
<details>
  <summary>Correct answer</summary>
  Because array is reference type
   <pre>
    // arr[0] -> 1
   </pre>

</details>

### Object.create
```
  const a = { val: 5 }
  const b = Object.create(a);
  console.log(b.val);

  a.val = 10;
  console.log(b.val);

  b.val = 15;
  console.log(a.val);
  console.log(b.val);
```

<details>
  <summary>What will be the output for a.val, b.val?</summary>
   The Object.create() method creates a new object, using an existing object as the prototype of the newly created object.

   First log will be display `b.val -> 5` because of inheritance
   <pre>
    b.__proto__ -> {val: 5}
   </pre>
  Because object is reference type, second log will show `10`. And final log is
  <pre>
   a.val = 10
   b.val = 15
  </pre>
</details>

### Object.create and operator delete
```
  var Employee = {
    company: 'xyz'
  }
  var emp1 = Object.create(Employee);
  delete emp1.company
  console.log(emp1.company); // ?
```

<details>
  <summary>What will be the output of the emp1.company?</summary>
  Above code will output `xyz`.
  Here emp1 object got company as prototype property.
  Operator delete doesn’t delete prototype property.

  emp1 object doesn’t have company as its own property.
  You can test it like:
  <pre>
    console.log(emp1.hasOwnProperty('company')); // output : false
  </pre>
</details>


### Object.assign
```
  const obj0 = { };
  const obj1 = {
      prop1: obj0
  };
  const obj2 = Object.assign({}, obj1)
```

<details>
  <summary>If it is correct that obj1.prop1 and obj2.prop1 have the same reference?<summary>
  Yes, the Object.assign() method copies all enumerable own properties from one or more source objects to a target object and it returns the target object.
</details>

