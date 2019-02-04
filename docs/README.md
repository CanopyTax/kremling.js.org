# Kremling
Kremling is an npm library for doing css with React. It uses [React hooks](https://reactjs.org/hooks), is only 4kb gzipped,
and requires no changes to your webpack config or build process.

[Kremling Github page](https://github.com/CanopyTax/kremling)

[Walkthrough](/walkthrough/getting-started.md)

## Hooks example
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

function FancyButton(props) {
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

## Components example
```jsx
import {Scoped} from 'kremling'

function AnotherComponent() {
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

## Motivation
Here are the principles behind Kremling's css.

1. [**Scoped css**](concepts/scoped-css.md). Have css rules apply to a component and its children, but no other components. Allow for cascading rules within a "scope".
2. **Make it easy to [conditionally apply css](walkthrough/conditional-css.md)**. We can do better than ternaries for changing a dom element's css classes.
3. **Remove unused css from the DOM**. When there are no more components that are using a css class, the `<style>` element for those components should be removed from the DOM.
4. **Readable class names**. In your browser dev tools, `<div class="card">` is easier to understand than `<div class="23fgh_es56_card">`.
