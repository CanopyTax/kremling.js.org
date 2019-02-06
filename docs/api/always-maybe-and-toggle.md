# Always, Maybe, and Toggle
`always`, `maybe`, and `toggle` are functions exported from kremling to help you
implement the [className prop](https://reactjs.org/docs/faq-styling.html#how-do-i-add-css-classes-to-components).
They are how kremling helps you implement [conditional css](/walkthrough/conditional-css.md).

They are also exported in shorthand form: `a`, `m`, and `t`.

You can chain calls to always, maybe and toggle: `always('foo').maybe('bar', isBar).toggle('class1', 'class2', showClass1)`

## Always
```jsx
import {always, a} from 'kremling'

always(className)
<div className={always('hi')} />
// Shorthand
<div className={a('hi')} />
```

Accepts a string `className` and returns a string that can be chained with more calls to always, maybe, or toggle.

## Maybe
```jsx
import {maybe, m} from 'kremling'

maybe(className, condition)
<div className={maybe('bye', isBye)} />
// Shorthand
<div className={m('bye', isBye)} />
```

Accepts a string `className` as the first argument, and a boolean `condition` as the second argument. Returns a string that
will only have `className` in it if the `condition` is truthy.

## Toggle
```jsx
import {toggle, t} from 'kremling'

toggle(truthyClass, falsyClass, condition)
<div className={toggle('visible', 'hidden', isVisible)}>
// Shorthand
<div className={t('visible', 'hidden', isVisible)}>
```

Returns a string that will have the `truthyClass` if `condition` is truthy, or the `falsyClass` if the `condition` is falsy.

## How these functions work

Each of these function returns a javascript `String` object (sometimes called a "boxed String"). The String object
has the always, maybe, and toggle methods on it, allowing you to chain calls: `always('foo').maybe('bar', props.bar)`.
Chaining is the reason why we're using boxed strings -- you cannot add methods to primitive strings.

Boxed Strings for the className prop work in React, the DOM, and Enzyme. If you ever run into a situation where
the boxed string is causing issues, you can always call `.toString()` to get a primitive string: `maybe('hi', hi).toString()`.
