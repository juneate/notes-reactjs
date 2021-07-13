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
