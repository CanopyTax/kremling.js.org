# Conditionally applying css
Sometimes we need to change the css that we apply to a dom element, depending on the situation.
For example, we might have a `loading` css class that we only apply to a div when we're waiting for
some data.

In situations like that, kremling has some built in functions to make our code easy to write and to understand.

## Example
```jsx
import {useCss, always, maybe} from 'kremling'

function LoadingData(props) {
  const scope = useCss(css)

  // We want the 'loading' css class to only be on the div when we're loading data.
  return (
    <div className={always("data").maybe("loading", props.isLoadingData)}>
      Here is your data
    </div>
  )
}

const css = `
& .data {
  background-color: white;
}

& .loading {
  background-color: lightgray;
}
`
```

## How this works
Check out the [these docs](api/always-maybe-and-toggle.md) for more detailed information
on how this works.
