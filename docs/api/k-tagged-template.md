# `k` tagged template

The `k` tag is a required function when using the `kremling-inline-loader`.
You can learn more about it on the
[kremling-inline-loader](/walkthrough/kremling-inline-loader.md) page.

### Separaters (returns an object)

The `k` tag takes in processed strings (from `kremling-inline-loader`)
with `||KREMLING||` separators:

```js
const css = k`k0||KREMLING||kremling||KREMLING||
  [kremling=k0] .test, [kremling=k0].test {background-color: red;}
`;
```

The separaters divide the pieces needed to make a styles object:
`id`, `namespace` and `styles`.

If the separaters are there, the `k` tag outputs an object:

```js
const css = {
  id: 'k0',
  namespace: 'kremling',
  styles: '[kremling=k0] .test, [kremling=k0].test {background-color: red;}',
}
```

### Return string

If you're not using the `kremling-inline-loader` (no separaters), then
the `k` tag returns the same string. This is helpful if you still want to have
syntax highlighting (captured with the `k` tag), but you don't want to pre-process
stuff with the loader:

```js
const css = k`
  & .test {background-color: red;}
`;
``` 