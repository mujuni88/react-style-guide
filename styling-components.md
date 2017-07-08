# Styling Components

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

### 



