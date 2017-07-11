# Functional Components

## propTypes

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

## Destructuring Props and defaultProps

Destructure your props and use default arguments as defaultProps.

```js
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

## 



