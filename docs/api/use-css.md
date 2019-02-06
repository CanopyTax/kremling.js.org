# useCss hook
Kremling exports a [react hook](https://reactjs.org/hooks) called `useCss`, which you use in your components.
To do so, first make sure that your version of react is at least `react@16.8.0`.

Since hooks only work with function components, you won't be able to call `useCss` in your class components.
Instead, check out [Scoped component](scoped-component.md), which is an alternative
that works great with classes.

## Basic Example
The useCss hook allows you to write css that will only apply to your component and to its children.

```js
import React from 'react'
import {useCss} from 'kremling'

function MyComponent(props) {
  const scope = useCss(css)

  return (
    <div {...scope} className="container">
      <button className="my-button">
        Button
      </button>
    </div>
  )
}

const css = `
& .container {
  border: 1px solid black;
}

& .my-button {
  background-color: lawngreen;
}
`
```

In this example, the `container` and `my-button` classes will work great for MyComponent, but cannot be
accessed by any sibling or parent components. This is what kremling calls [scoped css](/concepts/scoped-css.md).

One thing to note is that we're able to use the `my-button` css class without putting the `{...scope}` props onto the
`<button>`. This is because you only need to be able to put `{...scope}` on your container elements, and the inner elements
will already be in scope. See the [scoped css docs](/concepts/scoped-css.md) for more information.

## Fragments
When you return a fragment from a component, you'll often have two or more elements inside of the fragment. In such cases,
do not try to put the css scope onto the fragment, but instead on each of the elements inside of the fragment:

```js
import React from 'react'
import {useCss} from 'kremling'

function Mario() {
  const scope = useCss(css)

  return (
    <>
      <div {...scope} className="my-div">
        A div
      </div>
      <span {...scope} className="my-span">
        A span
      </span>
    </>
  )
}

const css = `
& .my-div {
  border: 1px solid red;
}

& .my-span {
  border: 1px solid blue;
}
`
```

## Advanced Example
Since css scopes apply to all dom elements in your component *and in children components*, you can define common css
in a parent component that is used by all children.

```js
import React from 'react'
import {useCss} from 'kremling'

function Parent() {
  return (
    <div {...scope}>
      <Child />
    </div>
  )
}

function Child() {
  // The child-button class is "in scope"
  return (
    <button className="child-button">Child</button>
  )
}

const css = `
& .child-button {
  background-color: blue;
}
`
```

## Can I apply a css scope to a React component (instead of a dom element)?
No you cannot. The props in the `scope` object need to be put into the dom. For example,
the following code will not work:

```js
import React from 'react'
import {useCss} from 'kremling'

function DontDoThis() {
  const scope = useCss(css)

  // Scope should only be applied to dom elements, not components
  return (
    <Child {...scope} />
  )
}

function Child(props) {
  // The child-class css class will not be defined in the dom.
  return (
    <div className="child-class">
      Child
    </div>
  )
}

const css = `
& .child-class {
  color: lawngreen;
}
`
```

## API
`const scope = useCss(css)`

The useCss hook is called with one argument and returns an object.

#### Arguments
- `css`: A string of css, or a PostCSS object created through [kremling-loader](/walkthrough/kremling-loader.md).

- 
