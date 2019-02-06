# Kremling
Kremling is an npm library for writing CSS with React. It is only 4kb gzipped, and requires no changes to your webpack config or build process.

[Kremling Github page](https://github.com/CanopyTax/kremling)

[Walkthrough](/walkthrough/getting-started.md)

## Motivation
Why use Kremling over say, CSS Modules?

1. **Option to use [React hooks](https://reactjs.org/hooks)**. Kremling is bleeding edge. :)
2. **Readable class names**. In your browser dev tools, `<div class="card">` is easier to understand than `<div class="23fgh_es56_card">`.
3. **Make it easy to [conditionally apply css](walkthrough/conditional-css.md)**. We can do better than ternaries for changing a DOM element's CSS classes.
4. **Remove unused CSS from the DOM**. When there are no more components that are using a CSS class, the `<style>` element for those components should be removed from the DOM.
5. [**Scoped css**](concepts/scoped-css.md). Have CSS rules apply to a component and its children, but no other components. Allow for cascading rules within a "scope".


## Hooks
Hooks are a part of React and Kremling likes them because it makes code extremely functional. (Joel help)

### Example with hooks
```jsx
import {useCss} from 'kremling'

function MyComponent() {
  const scope = useCss(css)

  return (
    <div className="container" {...scope}>
      <button className="big-button">
        A big button
      </button>
    </div>
  )
}

const css = `
/* your css classes are scoped for this component and its children components */
& .container {
  border: 1px solid lightgray;
}

& .big-button {
  width: 40px;
  height: 60px;
}
`
```

### Example without hooks
```jsx
import {Scoped} from 'kremling'

class AnotherComponent extends React.Component {
  render() {
    return (
      <Scoped css={css}>
        <div className="container">
          <button className="big-button">
            A big button
          </button>
        </div>
      </Scoped>
    )
  }
}

const css = `
& .container {
  border: 1px solid lightgray;
}

& .big-button {
  width: 40px;
  height: 60px;
}
`
```

## Conditional css
```jsx
import {always, maybe} from 'kremling'

function ClickHere(props) {
  return (
    <button
      className={always('click-here').maybe('already-clicked', props.wasClicked)}
      onClick={() => props.setWasClicked(true)}
    >
      Click here
    </button>
  )
}
```

## Separate CSS file
```js
// foo.js
import {useCss} from 'bandicoot'
import css from './foo.css'

function Foo(props) {
  const scope = useCss(css)

  return (
    <span {...scope} className="foo">
      Hello
    </span>
  )
}
```

```css
/* foo.css */
.foo {
  color: lawngreen;
}
```