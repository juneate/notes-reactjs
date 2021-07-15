# React JS Notes


## Lifecycle Methods

Lifecycle methods written with hooks can be [tested here](https://codepen.io/roccop/pen/gOgLGLv)

### Only after the first render (mount)
This replaces the tranditional lifecycle method `componentDidMount`

```js
useEffect(() => {
   // Code in here will run only after the first render (mount)
}, [])
```


### Before every render, other than the first (update)
This replaces the *deprecated* tranditional lifecycle method `componentWillUpdate`

```js
const isAlreadyMounted = useRef(false)
useEffect(() => {
   isAlreadyMounted.current = true
}, [])

if (isAlreadyMounted.current) {
   // Code in here will run every time other than the mount
}
```

### After every render, other than the first (update)
This replaces the tranditional lifecycle method `componentDidUpdate`

```js
const isAlreadyMounted = useRef(false)
useEffect(() => {
   if (isAlreadyMounted.current) {
      // Code in here will run every time other than the mount
   }
})
useEffect(() => {
   isAlreadyMounted.current = true
}, [])
```


### After every render, including the first (mount & update)
Combines the traditional lifecycle methods `componentDidMount` and `componentDidUpdate`

```js
useEffect(() => {
   // Code in here will run with every render of the view
})
```


### After a render triggered by a state variable update

```js
useEffect(() => {
   // Code in here will run when a state variable (`stateVar`) is set
}, [stateVar])
```



### Before the component is mounted (willmount)
This replaces the *depricated* traditional lifecycle method `componentWillMount`

```js
const useConstructor = (callback) => {
   const hasBeenCalled = useRef(false)
   if (hasBeenCalled.current) return
   callback()
   hasBeenCalled.current = true
}
useConstructor(() => {
   // Code in here will run before the render, and only on the mount (first call)
})
```


### Before the component is removed (unmount)
This replaces the traditional lifecycle method `componentWillUnmount`

```js
useEffect(() => {
   return(() => {
      // Code in here will run when the component is removed from the UI
   })
}, [])
```


## Context

To create context:

### 1. Create the context

1. Create a folder named `contexts` in the `src` folder
   - If applicable, add the path to `src/contexts` to your config alias (remember to restart the dev server)
2. Create a file within `src/contexts` to represent the Context
3. In the new file: `import {createContext} from 'react'`
4. Return `createContext()` to a variable
   - The argument passed to `createContext()` is the start value for the Context variable
   - Best practice is to name the variable with a capital letter, and end with `Context`, for example: `UserContext`
5. Export the Context object, for example: `export default UserContext`

### 2. Provide the context

1. In the Component that will provide the context, import the Context object, for example: `import UserContext from 'contexts/user'`
2. Wrap the Component(s) that will use the Context data with a provider component, for example: `<UserContext.Provider>...</UserContext.Provider>`
3. If applicable, set the `value` attribute (property) to the Provider, with the desired data, for example: `<UserContext.Provider value={userData}>...</UserContext.Provider>`

### 3. Consume the context

1. In any of the Provider's descendant components, `import` the Context object, for example: `import UserContext from 'contexts/user'`
2. Import the `useContext` hook from the React library: `import {useContext} from 'react'`
3. Within the Component, query the context using `useContext`, which will return the `value` data stored in the Provider, for example: `const userData = useContext(UserContext)`