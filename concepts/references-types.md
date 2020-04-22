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
  <summary>What did the function accidentaly change as well ?</summary>
  This function also accidentely changes the title of original spreadsheet.
  <code>
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
 </code>
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

### Object.create: read next code
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
  <summary>What console will display a.val, b.val?</summary>
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


### If it is correct that obj1.prop1 and obj2.prop1 will have the same reference?
```
  const obj0 = { };
  const obj1 = {
      prop1: obj0
  };
  const obj2 = Object.assign({}, obj1)
```

<details>
  <summary>Explanation</summary>
  Yes, the Object.assign() method copies all enumerable own properties from one or more source objects to a target object and it returns the target object.
</details>
