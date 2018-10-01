# Unstated Compose Suspense Middleware

Add support for middlewares to unstated composed containers.

## Install

```sh
npm install --save unstated-compose-suspense-middleware
```

## Usage

To learn more about composed containers check out [unstated-compose](https://github.com/fabiospampinato/unstated-compose).

```ts
import * as React from 'react';
import {ChildContainer} from 'unstated-compose-suspense-middleware';

class AppContainer extends ChildContainer {
  state = {
    value: 'No value...'
  };
  middlewares () { // This function is called by the constructor, it's just a convenience method where you can define your middlewares
    this.addMiddleware ( this.middlewareValueChanged ); // Add a new middleware via the `addMiddleware` method
  }
  middlewareValueChanged ( prevState ) { // Middlewares are called with the previous state
    if ( prevState.value !== this.state.value ) {
      this.removeMiddleware ( this.middlewareValueChanged ); // Remove a middleware via the `removeMiddleware` method
      return state = { value: 'middleware!' }; // A middleware can either mutate the state (ouch!) or return a new one
    }
  }
  updateValueFoo () {
    this.setState ({ value: 'foo' });
  }
  updateValueBar () {
    this.setState ({ value: 'bar' });
  }
}
```

## Related

- **[unstated-with-containers](https://github.com/fabiospampinato/unstated-with-containers)**: Higher-Order Component for providing unstated containers to a component.
- **[unstated-connect2](https://github.com/fabiospampinato/unstated-connect2)**: Easily connect your containers to components, without sacrificing performance.
- **[unstated-suspense](https://github.com/fabiospampinato/unstated-suspense)**: Unstated container with support for suspending/unsuspending updates propagation.
- **[unstated-compose-suspense](https://github.com/fabiospampinato/unstated-compose-suspense)**: unstated-compose containers with support for suspending/unsuspending updates propagation.

## License

MIT © Fabio Spampinato
