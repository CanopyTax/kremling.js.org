# Media queries
[Media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries) are supported by kremling with the normal
css syntax. Since kremling css is raw css, you can expect everything to work like normal:

## Examples
Note that ampersand in this example is not necessary if you're using [kremling-loader](/walkthrough/kremling-loader.md).

```js
const css = `
@media (max-width: 1024px) {
  & .foo {
    color: red;
  }
}
`
```
