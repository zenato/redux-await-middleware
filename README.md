Redux Await(Promise) Middleware
===============================

Await(Promise) [middleware](http://rackt.github.io/redux/docs/advanced/Middleware.html) for Redux.

Await middleware supprorts [FSA](https://github.com/acdlite/flux-standard-action) actions.


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

Create plain action function:

```js
function getData(params) {
  return {
    type: 'GET_DATA',
    payload: request.get('http://some_api'), // return Promise.
  }
}
```

or use [`redux-actions`](https://github.com/acdlite/redux-actions):

```js
var getData = createAction('GET_DATA', request.get('http://some_api'));
```

Then, use resolved data on Reducer:

```js
function someReducer(state = defaultState, action) {
  switch (action.type) {
    case 'GET_DATA':
      // can access result using payload property.
      return state.concat(action.payload);
    default:
      return state;
  }
}
```

## License

MIT
