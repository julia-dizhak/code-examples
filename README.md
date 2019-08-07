# Code-examples
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

#### Testing Forms
```
import renderer from 'react-test-renderer'
import Form, { validate } from '../Form'

jest.mock('redux-form', () => ({
  Field: 'Field',
  reduxForm: options => {
    // Wrap the component and return the new component, just like the real hoc does
    return Form => props => {
      // call the validate error to make sure errors are detected
      options.validate({}, props)
      return <Form {...props} />
    }
  }
}))

it('should render correctly', () => {
  const translate = jest.fn()
  const component = renderer.create(<Form translate={translate} />)
  expect(component.toJSON()).toMatchSnapshot()
})

it('should validate correctly', () => {
  // change the default mock behavior to pass through the provided string
  const translate = jest.fn(str => str)

  validate({}, { translate })
  expect(translate).toHaveBeenLastCalledWith('Required')

  validate(
    { username: 'much much longer than 15 characters buddy' },
    { translate }
  )
  expect(translate).toHaveBeenLastCalledWith('Must be 15 characters or less')

  validate({ username: 'ironman' }, { translate })
  expect(translate).not.toMatch({
    username: expect.any(String)
  })
})

...
FormTest.jsx

import { Field, reduxForm } from 'redux-form'

export const validate = (values, { translate }) => {
  const errors = {}
  if (!values.username) {
    errors.username = translate('Required')
  } else if (values.username.length > 15) {
    errors.username = translate('Must be 15 characters or less')
  }

  return errors
}

const renderField = ({
  input,
  label,
  type,
  meta: { touched, error, warning }
}) =>
  <div>
    <label>{label}</label>
    <div>
      <input {...input} placeholder={label} type={type} />
      {touched && (error && <span>{error}</span>)}
    </div>
  </div>

const Form = props => {
  const { handleSubmit, pristine, reset, submitting } = props
  return (
    <form onSubmit={handleSubmit}>
      <Field
        name="username"
        type="text"
        component={renderField}
        label="Username"
      />
      <div>
        <button type="submit" disabled={submitting}>Submit</button>
        <button type="button" disabled={pristine || submitting} onClick={reset}>
          Clear Values
        </button>
      </div>
    </form>
  )
}

export default reduxForm({
  form: 'example',
  validate
})(Form)
```

#### Testing Lifecycles
```
import renderer from 'react-test-renderer'
import Canvas from '../Canvas'

it('should render correctly', () => {
  const component = renderer.create(<Form x={0} y={0} />)
  expect(component.toJSON()).toMatchSnapshot()

  const instance = component.getInstance()
  const spy = jest.spyOn(instance, 'calculateGrid')

  // shouldComponentUpdate should stop the render and thus calculateGrid shouldn't be called
  component.update(<Form x={0} y={0} />)
  expect(spy).not.toHaveBeenCalled()

  // now the calculateGrid should've be called since x & y have new values
  component.update(<Form x={2} y={2} />)
  expect(spy).toHaveBeenCalled()
})
...
import { Component } from 'react'

export default class Canvas extends Component {
  calculateGrid = () => {
    /* Expensive method called during render */
  }

  shouldComponentUpdate({ x: nextX, y: nextY }) {
    const { x: prevX, y: prevY } = this.props
    return prevX !== nextX || prevY !== nextY
  }

  render() {
    /* some typical render logic here */
  }
}
```
