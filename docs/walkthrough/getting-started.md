# Getting started with Kremling
This tutorial will help you write css for your React components with kremling.

## Installation

To start, first install kremling.

```sh
npm install --save kremling # if you use npm
yarn add kremling # if you use yarn
```

## Write a component
Now, write a component using kremling. To do so, we'll use the `useCss` hook from kremling
and write some css as a javascript string.

```js
import {useCss, always, maybe} from 'kremling'

function MyComponent(props) {
  const scope = useCss(css)

  return (
    <div className="container" {...scope}>
      Hello world
    </div>
  )
}

const css = `
& .container {
  border: 1px solid black;
}
`
```

That's it! You can now render your component and the container div will have a 1px black border. There is no configuration
to get kremling to work -- you don't need to eject or change your webpack configuration.

## What is useCss actually doing?
In the code above, we call `useCss(css)`. But what is that actually doing?

[useCss()](api/use-css.md) is a [React hook](https://reactjs.org/hooks) that you call with a css string.
It returns to you an object of props that you should apply to your container dom element.
This is called ["scoping the css"](concepts/scoped-css.md).

## What about that ampersand in the css string?
You might have noticed that in the code example there is an ampersand (`&`) inside of our css string.

This is how you tell kremling that you're about to write a css rule. It is necessary because kremling uses it to make sure
that it is truly scoped and does not apply to any dom elements outside of our component and its children.
You can read more about how this works in the [scoped css documentation](concepts/scoped-css.md).

## Next steps
[Conditionally apply css](walkthrough/conditional-css.md)

[Usage without hooks](walkthrough/using-components.md)

[Preprocessing with webpack](walkthrough/build-processes.md)
