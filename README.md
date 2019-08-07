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

#### Jest test-setup configuration
```
{
  "jest": {
    "setupFiles": [
      "<rootDir>/test-setup.js"
    ]
  }
}

// eslint-disable-next-line no-console
const error = console.error
// eslint-disable-next-line no-console
console.error = (warning, ...args) => {
  if (/(Invalid prop|Failed prop type)/gi.test(warning)) {
    throw new Error(warning)
  }
  error.apply(console, [warning, ...args])
}
```

#### getInstance
```
import renderer from 'react-test-renderer'
import Input from '../Input'

it('should render correctly', () => {
  const component = renderer.create(<Input />)
  expect(component.toJSON()).toMatchSnapshot()

  // getInstance is returning the `this` object you have in your component
  // meaning anything accessible on `this` inside your component
  // can be accessed on getInstance, including props!
  const instance = component.getInstance()
  expect(instance.state).toMatchSnapshot('initial state')

  instance.handleChange({ target: { value: 'tony@stark.industries' } })
  expect(instance.state).toMatchSnapshot('updated state')
}

...
import { Component } from 'react'

export default class Input extends Component {
  state = { value: '' }

  handleChange = event => this.setState({ value: event.target.value })

  render() {
    return (
      <div>
        <label>Email</label>
        <input
          type="email"
          onChange={this.handleChange}
          value={this.state.value}
        />
      </div>
    )
  }
}

```

#### Mocking HOC
```
import renderer from 'react-test-renderer'
import NotificationsContainer from '../NotificationsContainer'

// we can just pass through the component since we pass dispatch prop directly
jest.mock('react-redux', () => component => component)

it('should render correctly', () => {
  const dispatch = jest.fn()
  const component = renderer.create(
    <NotificationsContainer dispatch={dispatch} />
  )
  expect(component.toJSON()).toMatchSnapshot()

  expect(dispatch).toHaveBeenCalled()
  expect(dispatch.mock.calls).toMatchSnapshot('dispatch was called correctly')
})

...

import { Component } from 'react'
import PropTypes from 'prop-types'
import { connect } from 'react-redux'
import Notifications from './Notifications'

class NotificationsContainer extends Component {
  static propTypes = {
    dispatch: PropTypes.func.isRequired
  }

  componentDidMount() {
    this.props.dispatch({ type: 'REQUEST_NOTIFICATIONS' })
  }

  render() {
    return <Notifications />
  }
}

export default connect()(NotificationsContainer)
```
