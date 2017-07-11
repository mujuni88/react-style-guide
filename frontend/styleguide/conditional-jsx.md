# Conditionals in jsx

## What are the approaches right now?

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

## Other solution: [renderIf](https://atticuswhite.com/blog/render-if-conditionally-render-react-components/)

## Why?

* Light weight. literally 4 lines of code
* Takes a predicate and returns a function accepting an element that will only be returned if the predicate is satisfied

## As an in-line condition

```js
render() {
  return (
    {renderIf(1 + 2 === 3)(
      <span>Hello World!</span>
    )}
  );
}
```

## As a named conditional function

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

## As a composed conditional function

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