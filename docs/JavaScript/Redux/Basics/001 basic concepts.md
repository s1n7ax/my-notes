# Basic Concepts

## Main components

- Store
- Reducers
- Actions

## Redux provides

- `createStore(reducers, middleware)` - to create a new Store
- `combineReducers({ key: reducer })` - collect multiple reducers into one root reducer
- `useStore` - to get the store
- `store.dispatch({action: 'dosomething'})` - do dispatch an action
- `store.subscribe(()-> {})` - to listen to the changes
- `unsubscribe()` - to stop listening to the changes

## Redux-thunk

### Why redux-thunk?

React hooks make redux-thunk a bit more useless because you no longer need to pass `dispach` or `useState` as parameters
to the action creators. But in old school class components, having to pass `dispatch` & `state` is a valid reason.

- Convenient

**without redux-thunk**, an action would look like this.

```javascript
() -> {
    let dispatch = useDispatch();

    // this is async
    createUser(dispatch, username, age)

    // this is sync
    dispatch(setDarkTheme())
}
```

Here, we have to pass the `dispatch` to the action creator to do dispatches. However, if it is
synchronous, then the action object can be directly passed. So, basically, redux-thunk makes the
above example, look like below.

```javascript
() -> {
    let dispatch = useDispatch();

    // this is async
    dispatch(createUser(username, age))

    // this is sync
    dispatch(setDarkTheme())
}
```

- Can access the current state without having to pass the state to the action creator

```javascript
let getUser = (userId) -> (dispatch, useState) -> {}
```

## Issues with Redux

- How to use it with Suspense?
- Decoupling Actions with REST APIs
