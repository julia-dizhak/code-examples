# Learning to code by JavaScript 
I use this repo to track examples of tricky JS code, which will help me to imrove my knowledges.

## See examples below 

### Read this code:
What are the values of `a` and `b` after it runs?
```
 let a = 10; // declare a variable called a -> set it to 10
 let b = a; // declare a variable called b -> set it to a; a is 10; so b is 10 too
 a = 0 // set the a variable to 0
```
<details>
  <summary>Correct Answer</summary>
  a is 0 now, and b is 10.
</details>

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

### Read next code
```
const obj = {
 a: 1, 
 b: 1
}
```
<details>
  <summary>What will return obj.c?</summary>
  undefined
</details>

### Read next code
```
What will be in console?
[] + {} 
[] + []
```
<details>
  <summary>Explanation</summary>
  You can only add numbers and strings, all other values will be converted to either one of those types.
  The plus operator performs three kinds of conversion: It converts values to primitives, numbers and strings.
  
  <pre>
   > [] + [] -> ''
    [].toString() -> ''

   > [] + {}
     '[object Object]'
     String({}) -> '[object Object]'
  </pre> 
  
  Objects are converted to either string (if the other operand is a string) or number (otherwise). If you want to concatenate   arrays, you need to use a method Array.prototype.concat(), for example.
  There is no built-in way in JS to 'concatenate' (merge) objects -lodash
</details>
