# Pseudo selectors
[Pseudo selectors and psuedo classes](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Pseudo-classes_and_pseudo-elements),
such as `:hover`, `:focus`, `:first-child`, and `::before`, are all supported with normal css syntax. Since kremling css strings
are raw css that is appended to the DOM, you can expect everything to work like normal.

## Examples
Note that the ampersand is not necessary if you're using [kremling-loader](/walkthrough/kremling-loader.md).
```js
const css = `
& .foo:hover {}

& .foo::before {}
`
```
