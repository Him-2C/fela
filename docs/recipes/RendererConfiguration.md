# Renderer Configuration

We already learned that the renderer is configurable with e.g. [plugins](../Plugins.md). Yet there are some more options.

In general, our renderer accepts a config object. The following table shows each configuration option, its expected values, its default value and what it is used for.

> We might introduce more configuration options with future releases, so be sure to frequently check for updates.

| Option | Value | Default |Description |
| ------ | ------ | ---------|---|
|`plugins` | `function[]` |  | [plugins](../Plugins.md) to process styles before rendering |
|`keyframePrefixes` |`string[]` |`['-webkit', '-moz-']` |which `@keyframes` prefixes are rendered |

## Example
```javascript
import { createRenderer } from 'fela'

import prefixer from 'fela-plugin-prefixer'
import unit from 'fela-plugin-unit'
import fallbackValue from 'fela-plugin-fallback-value'

const config = {
  plugins: [ unit('em'), prefixer(), fallbackValue() ],
  keyframePrefixes: ['-webkit-']
}


const renderer = createRenderer(config)

const keyframe = props => ({
  from: {
    width: 'calc(100% - 50px)',
    height: props.height *  2
  },
  to: {
    width: 'calc(50% - 50px)',
    height: props.height
  }
})

renderer.renderKeyframe(keyframe, { height: 100 })

console.log(renderer.renderToString())
```
```CSS
@-webkit-keyframes k0--qp8wpi {
  from {
    width: -webkit-calc(100% - 50px);
    width: -moz-calc(100% - 50px);
    width: calc(100% - 50px);
    height: 200em
  }

  to {
    width: -webkit-calc(50% - 50px);
    width: -moz-calc(50% - 50px);
    width: calc(50% - 50px);
    height: 100em
  }
}

@keyframes k0--qp8wpi {
  from {
    width: -webkit-calc(100% - 50px);
    width: -moz-calc(100% - 50px);
    width: calc(100% - 50px);
    height: 200em
  }

  to {
    width: -webkit-calc(50% - 50px);
    width: -moz-calc(50% - 50px);
    width: calc(50% - 50px);
    height: 100em
  }
}
```