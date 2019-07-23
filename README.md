# code-examples
Display good code examples

#### with usage of local storage
<pre>
if(!localStorage.getItem('name')) {
  setUserName();
} else {
  let storedName = localStorage.getItem('name');
  myHeading.textContent = 'Mozilla is cool, ' + storedName;
}
</pre>

#### test
<pre>
<TestComponent
  shortTable={true}
  (condition ? {bsStyle: 'success'} : {})
  bsStyle={condition ? 'success' : undefined}
/>
</pre>
