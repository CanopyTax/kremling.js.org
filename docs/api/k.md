# k``
The template literal processor `k` was introduced as an export from kremling to enhance the inline CSS editing experience. With it you have

1. The advantage of syntax highlighting (select editors)
2. The option to omit the ampersand prefix with the use of the [kremling-babel-plugin](https://github.com/CanopyTax/kremling-babel-plugin)

## Example
Once you've added [kremling-babel-plugin](https://github.com/CanopyTax/kremling-babel-plugin), here is how you can write components with `k`:

#### yoshi.js
```js
import React from 'react'
import {k} from 'kremling'

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
    padding: 16px;
    border: 1px solid black;
  }

  .yoshi-description {
    color: green;
  }
`
```

## Advantages
The advantages and disadvantages of `k` are very similar to [kremling-loader](/walkthrough/kremling-loader.md). The primary difference is where the CSS is housed. If you prefer CSS to be in a separate file, make use of kremling-loader. Otherwise, consider `k`.
