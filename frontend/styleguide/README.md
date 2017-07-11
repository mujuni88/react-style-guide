# Style Guide

## Table Of Contents

* [SDD Process](#sdd-process)
  * [Storybook](#storybook)
  * [Knobs](#knobs)
* [React Code](#react-code)
  * [Styling Components](styling-components.md)
  * [Class Components](class-components.md)
  * [Functional Components](functional-components.md)
  * [Conditional Jsx](conditional-jsx.md)

## SDD Processs

We follow Style-guide driven development using React Storybook. Storybook allows us to write visual test cases for our Components. You can mock states, props and render a Component in isolation in a browser. For more information checkout this [article](https://medium.com/nulogy/storybook-driven-development-a3c517276c07).

* Get a UI design 
* Create a component in Storybook first.
* List all the states and props that you think your component will need.
* Write a story for each of those states or use [Knobs](https://github.com/storybooks/storybook/tree/master/addons/knobs) to edit props dynamically. 
* Implement component. You will be going back and forth between browser andcode untill your stories work.  

### Storybook
![Storybook Gif](/assets/storybook.gif)

### Knobs
[Knobs playground](http://alturl.com/bi8vc)
![Knobs](/assets/storybook-knobs-example.png)


## React Code

For how to structure your React code, checkout the following resources. Borrowed some of the patterns from [here](https://engineering.musefind.com/our-best-practices-for-writing-react-components-dec3eb5c3fc8).

  * [Styling Components](styling-components.md)
  * [Class Components](class-components.md)
  * [Functional Components](functional-components.md)
  * [Conditional Jsx](conditional-jsx.md)