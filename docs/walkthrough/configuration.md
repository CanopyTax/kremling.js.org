# Configuration
By default, kremling requires zero configuration. There is no need to change or eject your webpack config. And no need to configure anything inside of your source code.

## Webpack
You don't need to change your webpack config to use kremling, unless you'd like to use [kremling-loader](kremling-loader.md).

## Kremling attributes in DOM
If you'd like to change the kremling attributes in the dom (such as in `<div kremling="0">`), you can do so by changing the kremling "namespace".
You can read more about why these attributes exist in [these docs](/concept/scoped-css.md).

#### Without kremling-loader
For all css strings that are embedded into javascript files and not preprocessed with kremling-loader, you can
configure the kremling dom attributes by modifying `Scoped.defaultNamespace`.

```js
import {Scoped} from 'kremling'

Scoped.defaultNamespace = 'name-of-my-project'
```

#### With kremling-loader
For css that is preprocessed by kremling-loader, you can configure the kremling dom attributes in your webpack config.
See [kremling-loader docs](https://github.com/CanopyTax/kremling-loader) for more information.
