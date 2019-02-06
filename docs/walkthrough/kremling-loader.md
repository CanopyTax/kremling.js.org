# Kremling loader
If you'd like to preprocess your css with [PostCSS](https://postcss.org/) (for [autoprefixer](https://github.com/postcss/autoprefixer) or anything else),
you'll need to add [kremling-loader](https://github.com/CanopyTax/kremling-loader) to your
wepback config. To do so, follow the [kremling-loader instructions](https://github.com/CanopyTax/kremling-loader).

## Example
Once you've set up kremling-loader, here is how you can write components with kremling css:

#### yoshi.js
```js
import React from 'react'
import css from './yoshi.css'

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
```

#### yoshi.css
```css
.container {
  padding: 16px;
  border: 1px solid black;
}

.yoshi-description {
  color: green;
}
```

## Advantages
Using kremling-loader allows you to omit the `&` in your css rules, since the css will be processed at build time instead of in the browser.

Additionally, since kremling-loader requires your css to be in a different file than your javascript code, you'll get nicer syntax highlighting in
your IDE.

## Disavantages
If you're using [create react app](https://facebook.github.io/create-react-app/), you'll have to eject your webpack configuration in order to add kremling-loader to it.

Additionally, you'll have to create a separate css file for each of your react components, instead of having everything the entire component encapsulated in one file.
