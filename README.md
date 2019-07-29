# code-examples
Display good code examples

#### with usage of local storage
```
if(!localStorage.getItem('name')) {
  setUserName();
} else {
  let storedName = localStorage.getItem('name');
  myHeading.textContent = 'Mozilla is cool, ' + storedName;
}
```

#### test
```
<TestComponent
  shortTable={true}
  (condition ? {bsStyle: 'success'} : {})
  bsStyle={condition ? 'success' : undefined}
/>
```

### Unit testing
#### example
```
describe('App', () => {
  let wrapper;
  
  describe('componentWillReceiveProps', () => {
      it('should call loadData when shouldLoadData is true', () =>  {
        wrapper = Shallow(<App />);

        const getSomethingSpy = jest.spyOn(wrapper.instance(), 'getSomething');
      // 1.) call via instance() 
      wrapper.instance().componentWillReceiveProps({shouldLoadData: true});
      // 2.) call via prototype
      App.prototype.componentWillReceiveProps({shouldLoadData: true});
       expect(getSomethingSpy).toHaveBeenCalled();
      });
    });
});
```
