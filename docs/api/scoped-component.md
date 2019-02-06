# Scoped component
Kremling exports a component called Scoped that can be used in your class or function components.
The Scoped component appends your css to the dom and modifies its direct children so that they
are containers for the [css scope](/concepts/scoped-css.md).

If you are using function components and/or hooks, it is recommended that you use [`useCss`](use-css.md)
instead of the Scoped component. However, feel free to use the Scoped component however you would like to - it
is a fully supported feature of kremling that is part of kremling's long term future.

## Example
To use the Scoped component, you should import it from kremling and render it around whichever
dom elements you want your css to apply to:

```js
import React from 'react'
import {Scoped} from 'kremling'

class ShoppingCart extends React.Component {
  render() {
    return (
      <Scoped css={css}>
        <div className="container">
          <button className="my-button">
            My button
          </button>
        </div>
      </Scoped>
    )
  }
}

const css = `
& .container {
  border: 1px solid black;
}

& .my-button {
  background-color: brown;
}
`
```

## Advanced example
Scoped css is applicable to all dom elements inside of the Scoped component. This means that css rules defined in parent components
are available in children components. This can be desireable sometimes, and a double edged sword if it's unexpected. Here is how
to use it to your advantage:

```js
import React from 'react'
import {Scoped} from 'kremling'

class Parent extends React.Component {
  render() {
    return (
      <Scoped css={css}>
        <div>
          <Child />
        </div>
      </Scoped>
    )
  }
}

const css = `
& .child-button {
  background-color: orange;
}
`

class Child extends React.Component {
  render() {
    // Child can use the child-button class because it is "in the css scope."
    return (
      <button className="child-button">
        Child button
      </button>
    )
  }
}
```

## Gotchas
The Scoped component modifies its direct children by adding dom attributes to them. Because of this, only direct children of Scoped
that are dom elements will actually be part of the css scope.

It is easy to forget this and can be difficult to debug. If you find yourself getting frustrated with this gotcha, try out the
[useCss hook](use-css.md), whose syntax is more explicit in showing which dom elements are in the CSS scope.

```js
import React from 'react'
import {Scoped} from 'kremling'

class Parent extends React.Component {
  render() {
    // Since Child is a direct child of Scoped and is not a dom element, the "gotcha" applies.
    // This means that Child will not be able to use the css classes defined in Parent.
    return (
      <Scoped css={css}>
        <Child />
      </Scoped>
    )
  }
}

const css = `
& .child-span {
  border: 1px solid black;
}
`

class Child extends React.Component {
  render() {
    // The child-span css class won't be "in scope" and won't work.
    return (
      <span className="child-span">
        Child span
      </span>
    )
  }
}
```

## API
#### Props
- `css`: A css string that has ampersands (`&`) in it before each css selector. The rules in this css string will
  apply to dom elements that are children of the Scoped component.
- `postcss`: A PostCSS object created by [kremling-loader](/walkthrough/kremling-loader.md).
- `children`: The direct children provided to Scoped will be modified to have extra dom attributes to do the
  [css scoping](/concepts/scoped-css.md). Direct children to Scoped should usually be dom elements, not React components.
  See the Gotcha section above.
