# Kremling inline loader

[https://github.com/CanopyTax/kremling-loader](https://github.com/CanopyTax/kremling-loader)

The `kremling-inline-loader` is a webpack loader that processes your javascript
that have`k` tagged templates in them. You can learn more about the `k` tag on
the [k tagged template](/api/k-tagged-template.md) page.

Just like the [Kremling loader](/walkthrough/kremling-loader.md), the
`kremling-inline-loader` processes `css` using `postcss` so you don't have to
use ampersands. Unlike the `kremling-loader` though, you can do all of this
inside your js!

Follow the [setup instructions](https://github.com/CanopyTax/kremling-loader)
to get started.


## Example
Once you've set up `kremling-inline-loader` in your webpack config, here is how
you can write components with kremling css:

```js
import React from 'react';
import { useCss, k } from 'kremling';

function Yoshi(props) {
  const scope = useCss(css)

  return (
    <div {...scope} className="container">
      <p className="yoshi-description">
        Yoshi is a fictional dinosaur who, although intelligent,
        is enslaved by a human plumber named Mario.
      </p>
    </div>
  )
}

const css = k`
  .container {
    background-color: red;
  }
`;
```

## Advantages
Using kremling-inline-loader allows you to omit the `&` in your css rules,
since the css will be processed at build time instead of in the browser.

Using the `k` tagged template allows you to capture it for syntax highlighting,
much like how `styled-components` plugins work. More to come on this topic!

## Disavantages
If you're using [create react app](https://facebook.github.io/create-react-app/), you'll have to eject your webpack configuration in order to add kremling-inline-loader to it.
