# React Styleguide

## Resources:

* Copied a lot of the examples from [here](https://medium.com/code-life/our-best-practices-for-writing-react-components-dec3eb5c3fc8#.w7ifawno4)
* renderIf library for complicated conditionals [here](https://atticuswhite.com/blog/render-if-conditionally-render-react-components/) 

## Class Components:

### css

Use the `glamor` library [here](https://github.com/threepointone/glamor).

Why?

* adds vendor prefixes / fallback values 
* supports all the pseudo :classes/::elements
* `@media` queries
* `@supports` statements
* `@font-face` / `@keyframes`
* dev helper to simulate pseudo classes like `:hover`, etc

```jsx
import { css } from 'glamor'

// make css rules 
let rule = css({ 
  color: 'red',
  ':hover': {
    color: 'pink'
  },
  '@media(min-width: 300px)': {
    color: 'green',
    ':hover': {
      color: 'yellow'
    }
  }
})

// add as data attributes
<div {...rule} {...another}>
  zomg
</div>

// or as classes 
<div className={`${rule} ${another}`}>
  zomg
</div>

// merge rules for great justice 
let mono = css({
  fontFamily: 'monospace'
})

let bolder = css({
  fontWeight: 'bolder'
})

<div {...css(mono, bolder)}>
  bold code!
</div>
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

## Functional Components

Use these types of components as often as possible. They have no state or methods.

### propTypes

Assign the propTypes variable at the top of the file so it's easily viewable to the developer.

```js
import React from 'react'
import {observer} from 'mobx-react'
import './styles/Form.css'
const expandableFormRequiredProps = {
  onSubmit: React.PropTypes.func.isRequired,
  expanded: React.PropTypes.bool
}
// Component declaration
ExpandableForm.propTypes = expandableFormRequiredProps
```

### Destructuring Props and defaultProps

Destructure your props and use default arguments as defaultProps.

```js
import React from 'react'
import {observer} from 'mobx-react'
import './styles/Form.css'
const expandableFormRequiredProps = {
  onSubmit: React.PropTypes.func.isRequired,
  expanded: React.PropTypes.bool
}
function ExpandableForm({ onSubmit, expanded = false, children }) {
  return (
    <form style={ expanded ? { height: 'auto' } : { height: 0 } }>
      {children}
      <button onClick={onExpand}>Expand</button>
    </form>
  )
}
```

## Conditionals in jsx

Solution using renderIf [here](https://atticuswhite.com/blog/render-if-conditionally-render-react-components/)

Why?

* Light weight. literally 4 lines of code
* Takes a predicate and returns a function accepting an element that will only be returned if the predicate is satisfied

## Examples

### As an in-line condition

```js
render() {
  return (
    {renderIf(1 + 2 === 3)(
      <span>Hello World!</span>
    )}
  );
}
```

### As a named conditional function

```
render() {
  const ifUniverseIsWorking = renderIf(1 + 2 === 3)
  return (
    {ifUniverseIsWorking(
      <span>Everything is okay in the world</span>
    )}
  );
}
```

### As a composed conditional function

```
const ifEven = count => renderIf(count % 2 === 0);
const ifOdd = count => renderIf(count % 2 !== 0);
render() {
  return (
    {ifEven(this.props.count)(
      <span>{this.props.count} is an even number!</span>
    )}
    {ifOdd(this.props.count)(
      <span>{this.props.count} is an odd number!</span>
    )}
  );
}
```

### What are the approaches right now?

* Lazy evaluation or short circuit evaluation
  ```js
  {true && <span/>}
  ```

* Variable assignment. mostly used when dealing with if-else scenario

  ```js
  class MyComponent extends Component {
  render() {
    var component;
    if (1 + 2 === 3) {
      component = <span>I show up only when this condition is true</span>
    } else {
      component = <span>I show up when the condition is false</span>
    }
    return (
      {component}
    );
  }
  }
  ```

* Function encapsulation   
  frequently used when dealing with complicated conditionals

  ```js
  class MyComponent extends Component {
  render() {
    return (
      {this.renderConditionalComponent()}
    )
  }
  renderConditionalComponent() {
    if (1 + 2 === 3) {
      return <span>I only show up when this condition is true</span>
    } else {
      return <span>I only show up when this condition is false</span>
    }
  }
  }
  ```



