Redux Await(Promise) Middleware
===============================

Await(Promise) [middleware](http://rackt.github.io/redux/docs/advanced/Middleware.html)
for Redux.

## Installation

```
npm install --save redux-await-middleware
```

Then, to enable Redux Await(Promise) Middleware, use [`applyMiddleware()`](http://rackt.github.io/redux/docs/api/applyMiddleware.html):

```js
import { applyMiddleware, createStore } from 'redux';
import awaitMiddleware from 'redux-await-middleware';
import reducers from './reducers/index';

const createStoreWithMiddleware = applyMiddleware(awaitMiddleware)(createStore);
const store = createStoreWithMiddleware(reducers);
```

## Usage

Create action with `promise` property:

```js
function getData(params) {
  return {
    type: 'GET_DATA',
    promise: request.get('url'), // Return `promise`.
    otherParams: 'someParam'
  }
}
```

Then, use resolved data on Reducer:

```js
function someReducer(state = defaultState, action) {
  switch (action.type) {
    case 'GET_DATA':
      return state.concat(action.res.data); // Accessable `res` property.
    default:
      return state;
  }
}
```

## License

MIT
