# `.setProps(nextProps) => Self`

A method that sets the props of the root component, and re-renders. Useful for when you are
wanting to test how the component behaves over time with changing props. Calling this, for
instance, will call the `componentWillReceiveProps` lifecycle method.

Similar to `setState`, this method accepts a props object and will merge it in with the already
existing props.

NOTE: can only be called on a wrapper instance that is also the root instance.


#### Arguments

1. `nextProps` (`Object`): An object containing new props to merge in with the current props



#### Returns

`ShallowWrapper`: Returns itself.



#### Example

```jsx
import React from 'react';
import PropTypes from 'prop-types';

function Foo({ name }) {
  return (
    <div className={name} />
  );
}
Foo.propTypes = {
  name: PropTypes.string.isRequired,
};
```
```jsx
const wrapper = shallow(<Foo name="foo" />);
expect(wrapper.find('.foo')).to.have.lengthOf(1);
expect(wrapper.find('.bar')).to.have.lengthOf(0);
wrapper.setProps({ name: 'bar' });
expect(wrapper.find('.foo')).to.have.lengthOf(0);
expect(wrapper.find('.bar')).to.have.lengthOf(1);
```

```jsx
import sinon from 'sinon';

const spy = sinon.spy(MyComponent.prototype, 'componentWillReceiveProps');

const wrapper = shallow(<MyComponent foo="bar" />);
expect(spy).to.have.property('callCount', 0);
wrapper.setProps({ foo: 'foo' });
expect(spy).to.have.property('callCount', 1);
```


#### Related Methods

- [`.setState(state) => Self`](setState.md)
- [`.setContext(context) => Self`](setContext.md)


