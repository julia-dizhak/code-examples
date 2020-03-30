# JavaScript tricky (and simple) questions

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
</details>


