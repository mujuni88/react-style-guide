# Class Components

## css

Use [styled-components](https://www.styled-components.com/docs/basics).

Why?

* write actual css to style your components.
* supports all css features including:
  * `@media` queries
  * `:pseudo-elements, :pseudo-classes, :hover`, etc
* Compatible with both React and React Native.

```jsx
import styled from 'styled-components'

// Create a Title component that'll render an <h1> tag with some styles
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

// Create a Wrapper component that'll render a <section> tag with some styles
const Wrapper = styled.section`
  padding: 4em;
  background: papayawhip;
`;

// Use Title and Wrapper like any other React component – except they're styled!
const Page = () => (
<Wrapper>
  <Title>
    Hello World, this is my first styled component!
  </Title>
</Wrapper>
);
```

### imports

Separate third party dependencies from local imports. following zeit's format [here](https://github.com/zeit/now-desktop/blob/31229be9280fd13616bf2b4bc7334a8338e28747/src/renderer/index.jsx).

```js
// Packages
import React, {Component} from 'react'
import {observer} from 'mobx-react'

// Ours
import ExpandableForm from './ExpandableForm'
import './styles/ProfileContainer.css'
```

### Initializing State

Should be at the top of the class

```js
export default class ProfileContainer extends Component {
  state = { expanded: false }
```

### propTypes and defaultProps

propTypes and defaultProps are static properties, declared right after initialization.

**All Components** should have propTypes

```js
export default class ProfileContainer extends Component {
  state = { expanded: false }

  static propTypes = {
    model: React.PropTypes.object.isRequired,
    title: React.PropTypes.string
  }

  static defaultProps = {
    model: {
      id: 0
    },
    title: 'Your Name'
  }
```

### Methods

Ensure the methods have the right context `this`.  
Use ES6 arrow functions instead of `this.handleSubmit.bind(this)`.

```js
export default class ProfileContainer extends Component {
  state = { expanded: false }

  static propTypes = {
    model: React.PropTypes.object.isRequired,
    title: React.PropTypes.string
  }

  static defaultProps = {
    model: {
      id: 0
    },
    title: 'Your Name'
  }
  handleSubmit = (e) => {
    e.preventDefault()
    this.props.model.save()
  }

  handleNameChange = (e) => {
    this.props.model.name = e.target.value
  }

  handleExpand = (e) => {
    e.preventDefault()
    this.setState( expanded: !this.state.expanded })
  }
```

### Destructuring props

```js
render() {
    const {
      model,
      title
    } = this.props
    return ( 
      <ExpandableForm 
        onSubmit={this.handleSubmit} 
        expanded={this.state.expanded} 
        onExpand={this.handleExpand}>
        <div>
          <h1>{title}</h1>
          <input
            type="text"
            value={model.name}
            onChange={this.handleChange}
            placeholder="Your Name"/>
        </div>
      </ExpandableForm>
    )
  }
```

Components with many props should have each prop on a newline

### Closures

Avoid closures like below because every time the parent component renders, a new function is created and passed to the input. Instead, create a method in your class and pass it in.

```js
<input
  type="text"
  value={model.name}
  // onChange={(e) => { model.name = e.target.value }}
  // ^ Not this. Use the below:
  onChange={this.handleChange}
  placeholder="Your Name"/>
```