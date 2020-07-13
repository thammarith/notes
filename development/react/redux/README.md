# Redux

Redux is a state management for React. The concepts are quite similar to Vuex that I'm more familiar with. So in this note, I'm going to use Vuex to compare and contrast the similarities and differences to get more understanding.

## Concepts

There are three crucial components that make up Redux, namely **store**, **action**, **reducer**.

### Components

#### Store

Like Vuex, **store** is the single soruce of truth for Redux. It's simply a JavaScript object that contains all the states. Treat the store like a snapshot of the application like a commit in *git*. The only way to change the data inside the store is to create another snapshot using **actions**.

#### Actions

**Actions** should be the only way to mutate the states. Imagine the store is a hotel. You should not patch anything yourself. Instead, you should call the service to do it for you and you don't have to know *how* (what steps) the service worker have to take to achieve what you want. You just tell them what you want and they'll do it for you.

#### Reducers

Having to be pure functions, **reducers** are the functions that take the whole state and return the new state accordingly to the given action. Going back to the previous hotel analogy, once you have asked the service to do something (that's an *action*), the service goes through steps to get what you want done. The process of patching is described in the reducer.

This is what a normal reducer looks like

```javascript
function counter(state, action) {
    // [Convention] If the reducer receives `undefined`, it should return what it considers to be the initial value of the state
    if (typeof state === 'undefined') return 0;

    // [Convention] People tend to use `type` as the key for the action type. It could be something else but why would you do that?
    // Checks the action type
    if (action.type === 'INCREMENT') return state + 1;
    if (action.type === 'DECREMENT') return state - 1;

    // [Convention] If the action is not legal, return the current state
    return state;
}
```

This can later be refactored to

```javascript
// [Convention] Sets the default value here
function counter(state = 0, action) {
    switch (action.type) {
        case 'INCREMENT': return state + 1;
        case 'DECREMENT': return state - 1;
        default: return state;
    }
}
```

As you can see, the reducer function is pure. Given the same input, it will always return the same output regardless of any other states of the application.

## Using Redux

To begin using Redux, we have to create a new store using `createStore(reducer)`

```javascript
import { createStore } from 'redux';

// Takes a reducer from anywhere
// const reducer = ...;
const store = createStore(reducer);
```

There are three functions that can be accessed from the `store` object

### `store.getState()`

This will return the state of the store. If we use `counter` above as our reducer (`const store = createStore(counter);`), we'll get `0` (default value) when we call `store.getStore();`

### `store.dispatch(action)`

We can use this function to *dispatch* an action. For example, if we want to use the `'INCREMENT'` action with the counter, we can call `store.dispatch({ type: 'INCREMENT' });`.

### `store.subscribe(callback)`

If we want to do something after an action has been dispatched, we can use `store.subscribe()` with a callback function as an argument to achieve that.

```javascript
store.subscribe(render);
// Calls to init the initial state value
render();

// Can be named something else
function render() {
    console.log('The action is called!');
}

function onButtonClick() {
    store.dispatch({ type: 'INCREMENT' });
}
```

## Using with React

Let's assum we have a counter application. Here is how to dispatch an action with React.

```jsx
const Counter = ({ value, onIncrement, onDecrement }) => (
    <>
        <h1>{value}</h1>
        <button onClick={onIncrement}>+</button>
        <button onClick={onDecrement}>-</button>
    </>
);
```

```jsx
<Counter
    value={store.getState()}
    onIncrement={() => store.dispatch({ type: 'INCREMENT' })}
    onDecrement={() => store.dispatch({ type: 'DECREMENT' })}
/>
```

## Miscellaneous

Basically, store implementation is a really simple function.

```javascript
function createStore(reducer) {
    let state;
    let listeners = [];

    // Init state by getting reducer to initiate the store
    dispatch({});

    function getState() { return state; }

    function dispatch(action) {
        state = reducer(state, action);
        // Calls every registered listeners after the action has been dispatched
        listeners.forEach(listener => listener());
    }

    function subscribe(listener) {
        // Keeps track of listeners since it can be called many times
        listeners.push(listener);
        // Provide the way to unsubscribe
        return function () {
            listeners = listners.filter(l => l !== listener);
        }
    }

    return { getState, dispatch, subscribe }
}
```
